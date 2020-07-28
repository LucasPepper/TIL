# Jackson - JSON

Jackson é responsável por efetuar a **Serialização e Desserialização de nossos objetos**. Ele transforma estruturas JSON em Objetos Java, e vice-versa.

Baeldung: "*...Jackson ObjectMapper class – and how to serialize Java objects into JSON and deserialize JSON string into Java objects.*"

O JSON é muito utilizado para auxiliar na comunicação entre diferentes aplicações escritas em diferentes linguagens, ex: Java, Ruby, NodeJS, etc. Ele trabalha como uma espécie de parser, o que pode evitar erros 400 (Bad request).

Outra alternativa é o GSON da Google.

Algumas propriedades bastante usadas:

* ObjectMapper

* @JsonProperty("id") - Para mapeamento

* @JsonFormat(pattern = "yyyy-MM-dd'T'HH:mm:ss")

* @JsonIgnore

* @JsonGetter

* @JsonSetter

## Binder

Custom Data Binder é fazer um mapper de uma propriedade que o mapper (neste caso, o Jackson) não reconhece naturalmente. Ex: ENUMs, Date.

[Baeldung - Jackson Tutorial](https://www.baeldung.com/jackson-object-mapper-tutorial)
