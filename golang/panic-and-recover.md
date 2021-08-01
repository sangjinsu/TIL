# Panic and Recover

- 폴더 이름은 cmd에서 인자로 받아 사용합니다

  ```bash
  $ go run files.go /my_directory
  ```

  ```bash
  $ ./files.exe /my_directory
  ```

- my_directory 폴더의 내부 파일이나 폴더는 접근 권한을 제한해야 패닉이 발생합니다

## panic 을 사용하지 않는 경우

```go
func scanDirectory(path string) error {
	fmt.Println(path)

	files, err := ioutil.ReadDir(path)
	if err != nil {
		// 호출에서 발생한 에러의 디버깅 정보 출력
		fmt.Printf("Returning error from scanDirectory(\"%s\") call\n", path)
	}

	for _, file := range files {
		filePath := filepath.Join(path, file.Name())
		if file.IsDir(){
			err := scanDirectory(filePath)
			scanDirectory(filePath)
			if err != nil {
				fmt.Printf("Returning error from scanDirectory(\"%s\") call\n", path)
			}
		} else {
			fmt.Println(filePath)
		}
	}
	return nil
}

func main() {

	if len(os.Args) <= 1 {
		log.Println("Need directory name as 1 argument")
		return
	}

	defer fmt.Println("Directory Scanning is finished")
	directoryName := os.Args[1]

	err := scanDirectory(directoryName)
	if err != nil {
		log.Fatalln(err)
	}

	scanDirectory(directoryName)
}
```

- 파일 및 폴더에 접근하는 재귀 호출 중 에러가 발생하면 main 함수에 도달할 대가지 모든 재인 체인에 걸쳐 반환되어야 한다.

  ```bash
  Returning error from scanDirectory("my_directory\first\second\protected") call
  Returning error from scanDirectory("my_directory\first\second") call
  Returning error from scanDirectory("my_directory\first") call
  Returning error from scanDirectory("my_directory/") call
  ```

## panic을 사용하는 경우

 ```go
 func scanDirectory(path string) {
 	fmt.Println(path)
 
 	files, err := ioutil.ReadDir(path)
 	if err != nil {
 		panic(err)
 	}
 
 	for _, file := range files {
 		filePath := filepath.Join(path, file.Name())
 		if file.IsDir(){
 			scanDirectory(filePath)
 		} else {
 			fmt.Println(filePath)
 		}
 	}
 }
 
 func main() {
 
 	if len(os.Args) <= 1 {
 		log.Println("Need directory name as 1 argument")
 		return
 	}
 
 	defer fmt.Println("Directory Scanning is finished")
 	directoryName := os.Args[1]
 
 	scanDirectory(directoryName)
 }
 ```

- panic 이 발생해도 모든 지연된 함수 호출은 계속해서 실행된다

- `defer` 호출이 두 개 이상이면 지연된 순서의 역순으로 stack 형식으로 실행된다

- 패닉이 발생하면 `scanDirectory` 모든 재귀 호출이 종료된다

  ```go
  defer fmt.Println("Directory Scanning is finished")
  ```

  ```bash
  panic: open my_directory\first\second\protected: Access is denied.
  
  goroutine 1 [running]:
  main.scanDirectory(0xc0001201e0, 0x23)
          C:/goworkspace/src/panic-and-recover/files.go:49 +0x2a6
  main.scanDirectory(0xc00013e0c0, 0x19)
          C:/goworkspace/src/panic-and-recover/files.go:56 +0x1ec
  main.scanDirectory(0xc000106180, 0x12)
          C:/goworkspace/src/panic-and-recover/files.go:56 +0x1ec
  main.scanDirectory(0xc000102080, 0xd)
          C:/goworkspace/src/panic-and-recover/files.go:56 +0x1ec
  main.main()
          C:/goworkspace/src/panic-and-recover/files.go:83 +0xc5
  exit status 2
  
  ```

## panic 과 recover 사용하기

- `recover`를 정상적인 프로그램 실행 중에 호출하면 `nil`만 반환하고 아무 일도 수행하지 않는다
- `recover` 를 별도 함수에서 호출하게 한 뒤 패닉을 발생시키는 코드 앞에 해당 함수를 `defer` 지연 시키면 된다
- 패닉 상태가 계속 이어지기 때문에 `panic` 을 호출하는 함수와 동일한 함수에서 `recover` 을 호출하는 것은 의미가 없다
- 패닉이 발생하면 `recover` 는 `panic` 이 보낸 값을 반환한다

```go
func reportPanic(){
	p := recover()
	if p == nil {
		return
	}
	err, ok := p.(error)
	if ok {
		log.Fatalln(err)
	} else {
		// 패닉 값이 에러 타입이 아니면 같은 값으로 다시 패닉을 발생시킨다
		panic(p)
	}
}

func scanDirectory(path string) {
	fmt.Println(path)

	files, err := ioutil.ReadDir(path)
	if err != nil {
		panic(err)
	}

	for _, file := range files {
		filePath := filepath.Join(path, file.Name())
		if file.IsDir(){
			scanDirectory(filePath)
		} else {
			fmt.Println(filePath)
		}
	}
}

func main() {

	if len(os.Args) <= 1 {
		log.Println("Need directory name as 1 argument")
		return
	}

	defer fmt.Println("Directory Scanning is finished")
	directoryName := os.Args[1]

	defer reportPanic()
	scanDirectory(directoryName)
}
```

## 추가

- 패닉 값이 에러가 아니면 같은 값으로 다시 패닉을 발생시킵니다
- 다른 예상치 못한 패닉을 처리할 수 있습니다

```go
func reportPanic(){
	p := recover()
	if p == nil {
		return
	}
	err, ok := p.(error)
	if ok {
		log.Fatalln(err)
	} else {
		// 패닉 값이 에러 타입이 아니면 같은 값으로 다시 패닉을 발생시킨다
		panic(p)
	}
}
```

