# HATEOAS

"*Hypermedia as the Engine of Application State (HATEOAS)* is a component of the REST application architecture that distinguishes it from other network application architectures.

With HATEOAS, a client interacts with a network application whose application servers provide information dynamically through hypermedia. A REST client needs little to no prior knowledge about how to interact with an application or server beyond a generic understanding of hypermedia."

Uma API HATEOAS provê informações que permitem navegar entre seus endpoints de forma dinâmica incluindo links junto às respostas.

Com isso deixamos a responsabilidade de acessos e de ações para o backend da aplicação.

Exemplo prático: imaginar um web-commerce de livros. Tem-se a lista de livros disponíveis para a venda, logo haverá botões *"Comprar"* e *"Adicionar à lista de desejo"* (**Frontend**) para os livros que possuem estoque (**Backend**). Para os que não tem estoque, gerar somente o botão *"Adicionar à lista de desejo"*.

```java
    public SoldadoListResponse criarLink(SoldadoEntity soldadoEntity) {

        SoldadoListResponse soldadoListResponse = objectMapper.convertValue(soldadoEntity, SoldadoListResponse.class);

        Link link = linkTo(methodOn(SoldadoController.class).buscarSoldado(soldadoEntity.getId())).withSelfRel();

        soldadoListResponse.add(link);

        return soldadoListResponse;

    }
```
