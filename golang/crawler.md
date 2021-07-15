# Golang Crawler

`https://github.com/PuerkitoBio/goquery`

```bash
$ go get github.com/PuerkitoBio/goquery
```

## 코스피 

```go
package main

import (
	"fmt"
	"github.com/PuerkitoBio/goquery"
	"io"
	"log"
	"net/http"
)

func main() {
	url := "https://finance.naver.com/sise/"
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

	if response.StatusCode != 200 {
		log.Fatalf("status code error: %d %s", response.StatusCode, response.Status)
	}

	doc, err := goquery.NewDocumentFromReader(response.Body)
	if err != nil {
		log.Fatal(err)
	}

	kospi := doc.Find("#KOSPI_now").Text()

	fmt.Println(kospi)
}

```

## 달러 환율

```go
package main

import (
	"fmt"
	"github.com/PuerkitoBio/goquery"
	"io"
	"log"
	"net/http"
)

func main() {
	url := "https://finance.naver.com/marketindex/"
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

	if response.StatusCode != 200 {
		log.Fatalf("status code error: %d %s", response.StatusCode, response.Status)
	}

	doc, err := goquery.NewDocumentFromReader(response.Body)
	if err != nil {
		log.Fatal(err)
	}

	kospi := doc.Find("#exchangeList > li.on > a.head.usd > div > span.value").Text()

	fmt.Println(kospi)
}

```

