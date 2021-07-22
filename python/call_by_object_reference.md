# Call by Object Reference

## [Call by Object Reference](https://foramonth.tistory.com/20)

- immutable : call by value 형식처럼 값을 복사해서 사용

- mutable : call by reference 형식처럼 주소값을 전달해서 사용

- 차이점: 오브젝트를 참조하고 있는 형식으로 오브젝트 내부에서 값을 생성 및 복사해서 사용한다.

  [Call by Object Reference 이미지](https://foramonth.tistory.com/20)

``` python
def func1(li):
    li.append(6)
    
def func2(li):
    li = [1,2,3] # 함수 내부에서 li 리스트 생성

def func3(li):
    li2 = li
    li2.append(6)
    print(li, li2) # [1, 2, 3, 4, 5, 6] [1, 2, 3, 4, 5, 6]

li1 = [1, 2, 3, 4, 5]
li2 = [1, 2, 3, 4, 5]
li3 = [1, 2, 3, 4, 5]

func1(li1)
func2(li2)

print(li1) # [1, 2, 3, 4, 5, 6]
print(li2) # [1, 2, 3, 4, 5]

func3(li3)
```



## Call by Reference

- 주소값을 인수로 전달하는 방식
- 함수 내부에서 변경하면 함수 외부 변수에 영향을 준다

## Call by Value

- 함수에 인수를 전달하는 방식으로 값을 복사하여 전달하기 대문에 함수 외부 변수에 영향을 주지 않는다.



