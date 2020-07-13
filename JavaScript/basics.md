# Estrutura de dados e tipos

O mais recente padrão ECMAScript define sete tipos de dados:

Seis tipos de dados são os chamados primitivos:

* Boolean. true e false.
* null. Uma palavra-chave que indica valor nulo. Devido JavaScript ser case-sensitive, null não é o mesmo que Null, NULL, ou ainda outra variação.
* undefined. Uma propriedade superior cujo valor é indefinido.
* Number. 42 ou 3.14159.
* String. "Howdy"
* Symbol (novo em ECMAScript 6). Um tipo de dado cuja as instâncias são únicas e imutáveis.
* e Object

Embora esses tipos de dados sejam uma quantidade relativamente pequena, eles permitem realizar funções úteis em suas aplicações.  
Objetos e funções são outros elementos fundamentais na linguagem. Você pode pensar em objetos como recipientes para os valores,
e funções como métodos que suas aplicações podem executar.

## Conversão de Tipos de Dados

JavaScript é uma linguagem dinamicamente tipada. Isso significa que você não precisa especificar o tipo de dado de uma variável quando declará-la, e tipos de dados são convertidos automaticamente conforme a necessidade durante a execução do script. Então, por exemplo, você pode definir uma variável da seguinte forma:

*var answer = 42;*

E depois, você pode atribuir uma string para a mesma variável, por exemplo:

*answer = "Obrigado pelos peixes...";*

Devido JavaScript ser dinamicamente tipado, essa declaração não gera uma mensagem de erro.

Em expressões envolvendo valores numérico e string com o operador +, JavaScript converte valores numérico para strings. Nas declarações envolvendo outros operadores, JavaScript não converte valores numéricos para strings. Por exemplo:

```javascript
"37" - 7 // 30
"37" + 7 // "377"
```

### Convertendo Strings para números

* parseInt()
* parseFloat()

*parseInt* irá retornar apenas números inteiros, então seu uso é restrito para a casa dos decimais. Além disso, é uma boa prática ao usar *parseInt* incluir o parâmetro da base. O parâmetro da base é usado para especificar qual sistema númerico deve ser usado.

Uma método alternativo de conversão de um número em forma de string é com o operador + (operador soma):

```javascript
"1.1" + "1.1" = "1.11.1"
(+"1.1") + (+"1.1") = 2.2
// Nota: Os parênteses foram usados para deixar mais legível o código, ele não é requirido.
```

## Literais

Você usa literais para representar valores em JavaScript. Estes são valores fixados, não variáveis, que você literalmente insere em seu script:

* Array literal
* Literais boolean
* Literais de ponto flutuante
* Inteiros
* Objeto literal
* String literal

### Objeto Literal

Um objeto literal é uma lista de zero ou mais pares de nomes de propriedades e valores associados de um objeto, colocado entre chaves ({}). Você não deve usar um objeto literal no início de uma declaração. Isso levará a um erro ou não se comportará conforme o esperado, porque o { será interpretado como início de um bloco.

Segue um exemplo de um objeto literal. O primeiro elemento do objeto carro define uma propriedade, meuCarro, e atribui para ele uma nova string, "Punto"; o segundo elemento, a propriedade getCarro, é imediatamente atribuído o resultado de chamar uma função *(tipoCarro("Fiat"));* o terceiro elemento, a propriedade especial, usa uma variável existente (vendas).

```javascript
var vendas = "Toyota";

function tipoCarro(nome) {
  if (nome == "Fiat") {
    return nome;
  } else {
    return "Desculpa, não vendemos carros " + nome + ".";
  }
}

var carro = { meuCarro: "Punto", getCarro: tipoCarro("Fiat"), especial: vendas };

console.log(carro.meuCarro);   // Punto
console.log(carro.getCarro);  // Fiat
console.log(carro.especial); // Toyota 
```

Além disso, você pode usar um literal numérico ou string para o nome de uma propriedade ou aninhar um objeto dentro do outro. O exemplo a seguir usar essas opções.

```javascript
var carro = { carros: {a: "Saab", "b": "Jeep"}, 7: "Mazda" };

console.log(carro.carros.b); // Jeep
console.log(carro[7]); // Mazda

```
