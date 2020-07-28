# Java HTTP Native Client

* httpClient.send(HttpRequest, HttpResponse.BodyHandlers)

* HttpRequest.newBuilder()

.uri()
.header()
.GET()  // Tipo do método que vamos fazer a request

## Rest Template - Spring Web

### Get

* GetForObject(URL, ClassRetorno, ?uriVariable) - onde ? indica um campo opcional. A variável é um filtro/query.

* GetForEntity(URL, ClassRetorno, ?uriVariable)

* Exchange(URL, MetodoHttp, ClassRetorno, ?uriVariable) - Usado em todos os métodos HTTP

### Post

* PostForLocation(URL, DATA, ?uriVariable) - Retorna uma URI

* PostForObject(URL, DATA, ClassRetorno, ?uriVariable)

* PostForEntity(URL, DATA, ClassRetorno, ?uriVariable)

* Exchange(URL, MetodoHttp, DATA, ClassRetorno, ?uriVariable)

### Put

* put(URI, DATA)

* put(URL, DATA, ?uriVariable)

* Exchange(URL, MetodoHttp, DATA, ClassRetorno, ?uriVariable)

### Delete

* delete(URI)

* delete(URL, ?uriVariable)

* Exchange(URL, MetodoHttp, ?uriVariable)