# Text and HTML Templates

- `text/template` and `html/template` package
: which provide a mechanism for substituting the values of variables into a `text` or `HTML template`

- a `template` is a string or file containing one or more portions enclosed in `double braces` `{{...}}`, called `actions`

- a simple template string 

```go
const temp1 = `{{.TotalCount}} issues:
{{range .Items}}------------------------------
Number: {{.Number}}
User: {{.User.Login}}
Title: {{.Title | printf "%.64s"}}
Age: {{.CreateAt | daysAgo}} days
{{end}}
`
```

- `{{range .Items}} and {{end}}` actions create a loop
- within an action, `|` notation makes the result of one operation the argument of another.
- analogous to a Unix shell `pipeline`.

- templates are usually fixed at compile time, failure to parse a template indicates a fatal bug in the program.
- `template.Must` helper function makes `error handling` more convenient

```go
package main

import (
	"example/hello/github"
	"log"
	"os"
	"text/template"
	"time"
)

const temp1 = `{{.TotalCount}} issues:
{{range .Items}}----------------------------------
Number: {{.Number}}
User:   {{.User.Login}}
Title:  {{.Title | printf "%.64s"}}
Age:    {{.CreateAt | daysAgo}} days
{{end}}`

func daysAgo(t time.Time) int {
	return int(time.Since(t).Hours() / 24)
}

var report = template.Must(template.New("issuelist").Funcs(template.FuncMap{"daysAgo": daysAgo}).Parse(temp1))

func main() {
	result, err := github.SearchIssues(os.Args[1:])
	if err != nil {
		log.Fatal(err)
	}
	if err := report.Execute(os.Stdout, result); err != nil {
		log.Fatal(err)
	}
}
```

## `html/template` package
- it uses the same API as `text/template` but adds features for escaping of strings appearing within HTML, Javascript, CSS, or URLs.
- this feature can help avoid `HTML generate security`, an `injection attack`

```go
var issueList = template.Must(template.New("issuelist").Parse(`
     <h1>{{.TotalCount}} issues</h1>
     <table>
     <tr style='text-align: left'>
       <th>#</th>
       <th>State</th>
       <th>User</th>
       <th>Title</th>
     </tr>
     {{range .Items}}
     <tr>
       <td><a href='{{.HTMLURL}}'>{{.Number}}</a></td>
       <td>{{.State}}</td>
       <td><a href='{{.User.HTMLURL}}'>{{.User.Login}}</a></td>
       <td><a href='{{.HTMLURL}}'>{{.Title}}</a></td>
     </tr>
     {{end}}
     </table>
     `))
```
