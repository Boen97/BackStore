# JSON

- `Javascript Object Notation(JSON)` is a standard notation for sending and receiving `structured information`
- JSON is not the only such notation, `XML` and `Google's Protocol Buffers` serve similar purposes

- `encoding/json`, `encoding/xml`, `encoding/asn1` packages are the the standard library support these formates

- `JSON` is an encoding of Javascript values-strings, numbers, booleans, arrays, and objects-as `Unicode text`

## JSON.Marshal / JSON.MarshalIndent

- Go data structure to JSON is `Marshaling`
```go
data, err := json.Marshal(movies)
```

- `JSON.MarshalIndent` are for human consumption.

> only `exported` fields are `marshaled`

## field tags

> a field tag is a string of `metadata` associated at compile time with the field of a struct:

```go
type Movie struct {
    Year int `json:"released"`
    Color bool `json:"color, omitempty"`
}
```
- since they contain `double quotation` marks, field tags are usually written with raw string literals
- the `json` key controls the behavior of the `encoding/json` package, and other `encoding/...` packages follow this convention.
- the first part of the `json` field tag specifies an `alternative JSON name` for the Go field
- field tags are often used to specify an `idiomatic JSON name` like `total_count` for a Go field named `TotalCount`
- the tag for `Color` has an `additional option`, `omitempty`, which indicates that no JSON output should be produced
- if the field has the zero value for its type or tis otherwise emtpy.


## unmarshaling

- decoding JSON to a Go data structure
- `json.Unmarshal`
- other unmatched names in the JSON are `ignored`

- `streaming decoder`, `json.Decoder`
- which allows several JSON entites to be decoded in sequence from the same stream
- `streaming encoder`, `json.Encoder`

```go
package github

import (
	"encoding/json"
	"fmt"
	"net/http"
	"net/url"
	"strings"
	"time"
)

const IssueUrl = "https://api.github.com/search/issues"

type User struct {
	Login   string
	HTMLURL string `json:"html_url"`
}

type Issue struct {
	Number   int
	HTMLURL  string `json:"html_url"`
	Title    string
	State    string
	User     *User
	CreateAt time.Time `json:"create_at"`
	Body     string
}

type IssuesSearchResult struct {
	TotalCount int `json:"total_count"`
	Items      []*Issue
}

func SearchIssues(terms []string) (*IssuesSearchResult, error) {
	q := url.QueryEscape(strings.Join(terms, " "))
	resp, err := http.Get(IssueUrl + "?q=" + q)
	if err != nil {
		return nil, err
	}
	if resp.StatusCode != http.StatusOK {
		resp.Body.Close()
		return nil, fmt.Errorf("search query failed: %s", resp.Status)
	}

	var result IssuesSearchResult

	if err := json.NewDecoder(resp.Body).Decode(&result); err != nil {
		resp.Body.Close()
		return nil, err
	}
	resp.Body.Close()
	return &result, nil
}
```
```go
package main

import (
	"example/hello/github"
	"fmt"
	"log"
	"os"
)

func main() {
	result, err := github.SearchIssues(os.Args[1:])
	if err != nil {
		log.Fatal(err)
	}
	fmt.Printf("%d issues:\n", result.TotalCount)
	for _, item := range result.Items {
		fmt.Printf("#%-5d %9.9s %.55s\n", item.Number, item.User.Login, item.Title)
	}
}
```
