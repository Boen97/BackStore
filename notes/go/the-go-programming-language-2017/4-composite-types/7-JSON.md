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
