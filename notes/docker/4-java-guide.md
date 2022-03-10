- `CMD ["./mvnw", "spring-boot:run"]`
  - tell Docker what command we want to run when our image is executed inside a container.

```
$ curl --request GET \
--url http://localhost:8080/actuator/health \
--header 'content-type: application/json'
```
