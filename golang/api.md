# Golang API 사용

## 나이 예측

```go
package main

import (
	"encoding/json"
	"fmt"
	"io"
	"io/ioutil"
	"log"
	"net/http"
)

type Persons []struct {
	Name  string `json:"name"`
	Age   int    `json:"age"`
	Count int    `json:"count"`
}


func main() {
	names := []string{"tak", "tony", "eric", "musk"}

	url := "https://api.agify.io?"

	for _, name := range names {
		url += fmt.Sprintf("name[]=%s&", name)
	}

	response, err := http.Get(url)
	if err != nil {
		log.Fatal(err)
	}
	defer func(Body io.ReadCloser) {
		err := Body.Close()
		if err != nil {
			log.Fatal(err)
		}
	}(response.Body)

	jsonData, err := ioutil.ReadAll(response.Body)
	if err != nil {
		log.Fatal(err)
	}

	var persons Persons
	err = json.Unmarshal(jsonData, &persons)

	for _, person := range persons {
		age := person.Age
		name := person.Name
		fmt.Println(name, age)
	}

}

```

## 나이 예측 - Concurrency

```go
package main

import (
	"encoding/json"
	"fmt"
	"io"
	"io/ioutil"
	"log"
	"net/http"
	"sync"
)

type Person struct {
	Name  string `json:"name"`
	Age   int    `json:"age"`
	Count int    `json:"count"`
}

func fetchAge(name string, url string, ch chan Person){

	defer wg.Done()

	url += fmt.Sprintf("name=%s", name)
	response, err := http.Get(url)
	if err != nil {
		log.Fatal(err)
	}
	defer func(Body io.ReadCloser) {
		err := Body.Close()
		if err != nil {
			log.Fatal(err)
		}
	}(response.Body)

	jsonData, err := ioutil.ReadAll(response.Body)
	if err != nil {
		log.Fatal(err)
	}

	var person Person
	err = json.Unmarshal(jsonData, &person)

	ch <- person
	close(ch)
}

var wg sync.WaitGroup

func main() {
	names := []string{"tak", "tony", "eric", "musk"}

	url := "https://api.agify.io?"

	ch := make(chan Person)

	wg.Add(len(names))
	for _, name := range names{
		go fetchAge(name, url, ch)
	}

	go func() {
		wg.Wait()
		close(ch)
	}()

	for person := range ch {
		age := person.Age
		name := person.Name
		fmt.Println(name, age)
	}
}

```

