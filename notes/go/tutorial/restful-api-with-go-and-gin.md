# Developing a RESTful API with Go and Gin

- Gin simplifies many coding tasks associated with building web applications, including web services.

## Design API endpoints

- when developing an API, you typically begin by designing the `endpoints`

- here are the endpoints you'll create in this tutorial
1. /albums
   - `GET` - Get a list of all albums, returned as JSON.
   - `POST` - Add a new album from request data sent as JSON.

2. /albums/:id
   - `GET` - Get an album by its ID, returning the album data as JSON.

## Create the data

- design data structures for handing data.
- this tutorial store data in memory.

```go
type album struct {
	ID string `json:"id"`
	Title string `json:"title"`
	Artist string `json:"artist"`
	Price float64 `json:"price"`
}
```

- `json:"artist"` specify what a field's name should be used when serialized into JSON.
- without them, the JSON would use the struct's capitalized filed names, a style not as common in JSON.

## write a hanler to return all items.

```go
func getAlbums(c *gin.Context) {
	c.IndentedJSON(http.StatusOK, albums)
}
```

- `Context.IndentedJSON` to serialize the struct into JSON and add it to the response

```go
func main() {
	router := gin.Default()
	router.GET("/albums", getAlbums)

	if err := router.Run("localhost:8080"); err != nil {
		fmt.Println("err")
	}
}
```

`$ curl http://localhost:8080/albums`

## write a handler to add a new item.

```go
func postAlbums(c *gin.Context) {
	var newAlbum album

	if err := c.BindJSON(&newAlbum); err != nil {
		return
	}

	albums = append(albums, newAlbum)
	c.IndentedJSON(http.StatusCreated, newAlbum)
}
```

```
curl http://localhost:8080/albums \
    --include \
    --header "Content-Type: application/json" \
    --request "POST" \
    --data '{"id": "4","title": "The Modern Sound of Betty Carter","artist": "Betty Carter","price": 49.99}'
```

- `--include` Include the HTTP response headers in the output.

```
$ curl http://localhost:8080/albums \
    --header "Content-Type: application/json" \
    --request "GET"
```

## write a handler to return a specific item.

```go
func getAlbumByID(c *gin.Context) {
	id := c.Param("id")

	for _, a := range albums {
		if a.ID == id {
			c.IndentedJSON(http.StatusOK, a)
			return
		}
	}

	c.IndentedJSON(http.StatusNotFound, gin.H{"message": "album not found"})
}
```

```go
func main() {
	router := gin.Default()
	router.GET("/albums", getAlbums)
	router.POST("/albums", postAlbums)
	router.GET("/albums/:id", getAlbumByID)

	if err := router.Run("localhost:9999"); err != nil {
		fmt.Println("err")
	}
}
```

- `/albums/:id`
- in Gin, the colon preceding an item in the path signifies that the item is a `path parameter`

```shell
$ curl http://localhost:8080/albums/2
```

```go
type any = interface{}
```
