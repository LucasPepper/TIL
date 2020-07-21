# Lambda Functions

As funções Lambda foram adicionadas no Java 8, que tem como principal objetivo fazer proveito das técnicas de linguagens funcionais, reduzindo a quantidade de código, por exemplo.

Simplificando um pouco a definição, uma função lambda é uma função sem declaração, isto é, não é necessário colocar um nome, um tipo de retorno e o modificador de acesso. A ideia é que o método seja declarado no mesmo lugar em que será usado. As funções lambda em Java tem a sintaxe definida como *(argumento) -> (corpo)*:

```java

(int a, int b) -> {  return a + b; }
() -> System.out.println("Hello World");
(String s) -> { System.out.println(s); }
() -> 42
() -> { return 3.1415 };
a -> a > 10

```

Exemplo de Lambda + Interface funcional:

```java
public class Lambda {
    public static void main(String[] args) {
        Funcao putSrOnString = valor -> "Sr. " + valor;
        System.out.println(putSrOnString.gerar("Lucas"));
    }
}

/* Para usar Lambda, é preciso declarar uma Interface Funcional: uma interface que contém apenas UM método abstrato */
@FunctionalInterface
interface Funcao {
    String gerar(String valor);

    /* A maior motivação para a criação de métodos default (conhecidos também como métodos defender ou virtual extension methods)
    ** foi a necessidade de adicionar novas funcionalidades às interfaces existentes sem quebrar o código que faz uso delas.
    ** Ao contrário dos métodos não-default, é NECESSÁRIA a implementação (corpo) do método.
    */
    default Integer gerarNumero(String valor){
        return null;
    }
}

```

## Regras

* Em caso de um único comando: não é necessário utilizar chaves (Escopo semelhante ao de um Bloco com chaves);

* Caso o retorno for do tipo *void*, não é necessário escrever *return*;

* Se a função possuir mais de uma instrução, DEVEMOS utilizar chaves E explicitar o retorno caso for diferente de *void*.

Ex:

```java

Funcao putPrefixSrOnString = valor -> {
    String valorComPrefixo = "Sr. " + valor;
    String valorComPrefixoEPontoFinal = valorComPrefixo + ".";
    return valorComPrefixoEPontoFinal;
}
```

### Adendos

É possível utilizar Interfaces conhecidas em conjunto com as funções Lambda. Por exemplo, *Predicate*, *IntFunction*, dentre outras.

Essas interfaces possuem como característica principal o recebimento de uma função como parâmetro, ex:

```java
public class LambdaIntFunction {
    public static void main(String[] args) {
        List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        System.out.println("Multiplica elementos por 5:");
        realizaOperacao(list, (n) -> n * 5);

        System.out.println("Soma 3 em todos os elementos:");
        realizaOperacao(list, (n) -> n + 3);

    }

    public static void realizaOperacao(List<Integer> list, IntFunction<Integer> function) {
        list.forEach(n -> {
            n = function.apply(n);
            System.out.println(n + "");
        });

    }
```

Perceba que foi passada a função *function* como parâmetro. Percebe também o método *apply(valor)* que foi implementado.

A interface *Predicate* tem como característica o recebimento de uma expressão lógica, que é avaliada com o método *test*, retornando true ou false.

Diferenças-chave do *Predicate* para *IntFunction* ou outras interfaces (Package function) que são utilizadas em conjunto com Funções Lambda:

* Tipo e número do(s) Parâmetro(s) de entrada;

* Tipo de retorno da função.

Fonte: [DevMedia](https://www.devmedia.com.br/como-usar-funcoes-lambda-em-java/32826)
