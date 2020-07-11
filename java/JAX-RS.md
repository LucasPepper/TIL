# REST JAX - RS

"Jakarta RESTful Web Services, (JAX-RS) is a Java programming language API spec that provides support in creating web services according to the Representational State Transfer (REST) architectural pattern. JAX-RS uses annotations, introduced in Java SE 5, to simplify the development and deployment of web service clients and endpoints."

Para acessar os recursos do nosso servidor são utilizados diversas anotações correspondentes aos verbos HTTP, onde os mais utilizados são:

* GET: Buscar dados.
* POST: Utilizado para criar novas informações.
* PUT: Utilizado para alterar informações.
* DELETE: Remover dados.

## Extraindo valores

**@PathVariable** Especifica que o valor do parâmetro será indicado na URI. Ex: *meusite.com.br/usuario/{id}*

**@RequestParam** Extrai o valor do parâmetro da URI. Ex: *?idade=10&uf=MG*

**@RequestBody** Recebe os valores no corpo da requisição.

## Response

**ResponseEntity** Representa toda resposta HTTP. Você pode controlar qualquer coisa que aconteça, código de status, cabeçalhos e corpo.