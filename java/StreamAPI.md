# Stream API

Alguns trechos da [documentação do pacote java.util.stream](https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html):

" Classes to support functional-style operations on streams of elements, such as map-reduce transformations on collections. "

" Collections and streams, while bearing some superficial similarities,
have different goals.  Collections are primarily concerned with the efficient management of, and access to, their elements.  By contrast, streams do not provide a means to directly access or manipulate their elements, and are instead concerned with declaratively describing their source and the computational operations which will be performed in aggregate on that source. "

``` java
int sum = widgets.stream()
                 .filter(w -> w.getColor() == RED)
                 .mapToInt(w -> w.getWeight())
                 .sum();
```

" Here we use widgets, a Collection<Widget>, as a source for a stream, and then perform a filter-map-reduce on the stream to obtain the sum of the weights of the red widgets. (Summation is an example of a reduction operation.)

The key abstraction introduced in this package is stream. The classes Stream, IntStream, LongStream, and DoubleStream are streams over objects and the primitive int, long and double types. Streams differ from collections in several ways:

* **No storage**. A stream is not a data structure that stores elements; instead, it conveys elements from a source such as a data structure, an array, a generator function, or an I/O channel, through a pipeline of computational operations.
* **Functional in nature**. An operation on a stream produces a result, but does not modify its source. For example, filtering a Stream obtained from a collection produces a new Stream without the filtered elements, rather than removing elements from the source collection.
* **Laziness-seeking**. Many stream operations, such as filtering, mapping, or duplicate removal, can be implemented lazily, exposing opportunities for optimization. For example, "find the first String with three consecutive vowels" need not examine all the input strings. Stream operations are divided into intermediate (Stream-producing) operations and terminal (value- or side-effect-producing) operations. Intermediate operations are always lazy.
* **Possibly unbounded**. While collections have a finite size, streams need not. Short-circuiting operations such as limit(n) or findFirst() can allow computations on infinite streams to complete in finite time.
* **Consumable**. The elements of a stream are only visited once during the life of a stream. Like an Iterator, a new stream must be generated to revisit the same elements of the source.

"Most stream operations accept parameters that describe user-specified behavior, such as the lambda expression *w -> w.getWeight()* passed to
*mapToInt* in the example above.  To preserve correct behavior, these behavioral parameters must be **NonInterference**(they do not modify the stream source) and in most cases must be **Stateless** (their result should not depend on any state that might change during execution of the stream pipeline). "

Manipulação de coleções com o paradigma funcional de forma paralela, objetivando performance maior e códigos mais enxutos e intuitivos.

**Imutável** - Não altera a coleção origem, sempre cria uma nova coleção.

Principais funcionalidades:

* **Mapping** - Retorna uma coleção com mesmo tamanho da origem com os tamanhos alterados.

* **Filtering** - Retorna uma coleção igual ou menor que a coleção origem, com os elementos intactos.

* **ForEach** - Executa uma determinada lógica para cada elemento, retornando nada.

* **Peek** - Executa uma determinada lógica para cada elemento, retornando a própria coleção.

* **Counting** - Retorna um inteiro que representa a contagem de elementos.

* **Grouping** - Retorna uma coleção agrupada de acordo com a regra definida.

Exemplo com vários métodos da Stream API:

```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;
import java.util.stream.Collectors;

public class TesteStream {
    public static void main(String[] args) {

        List<String> estudantes = new ArrayList<>();

        estudantes.add("Marcelo");
        estudantes.add("Carla");
        estudantes.add("Juliana");
        estudantes.add("Thiago");
        estudantes.add("Rafael");

        List<String> vazio = new ArrayList<>();

        // Retorna a contagem de elementos do stream
        System.out.println("Contagem: " + estudantes.stream().count());

        // Retorna o elemento com maior número de letras
        System.out.println(vazio.stream().max(Comparator.comparingInt(String::length)));

        // Retorna o elemento com maior número de letras
        System.out.println(estudantes.stream().max(Comparator.comparingInt(String::length)));

        // Retorna o elemento com menor número de letras
        System.out.println(estudantes.stream().min(Comparator.comparingInt(String::length)));

        // Retorna os elementos que tem a letra R no nome
        System.out.println("Com a letra R no nome: " + estudantes.stream().filter((estudante) ->
                            estudante.toLowerCase().contains("r")).collect(Collectors.toList()));

        // Retorna uma nova coleção, com os nomes concatenados a quantidade de letras de cada nome
        System.out.println("Retorna uma nova coleção com a quantidade de letras: " + estudantes.stream().map(estudante ->
                            estudante.concat(" - ").concat(String.valueOf(estudante.length()))).collect(Collectors.toList()));

        // Retorna somente os 3 primeiros elementos da coleção
        System.out.println("Retorna os 3 primeiros elementos: " + estudantes.stream().limit(3).collect(Collectors.toList()));

        // Exibe cada elemento no console, e depois retorna a mesma coleção
        System.out.println("Retorna os elementos: " + estudantes.stream().peek(System.out::println).collect(Collectors.toList()));

        // Exibe cada elemento no console sem retornar outra coleção. Isso significa que não é possível aplicar nada após a stream
        // (ela foi consumida, só é possível passar por ela uma vez). Somente se for repassada.
        System.out.print("Retorna os elementos novamente: ");
        estudantes.stream().forEach(System.out::println);

        // Retorna true se TODOS os elementos atendem ao método passado (retorna boolean)
        System.out.println("Todos elementos tem A no nome?" + estudantes.stream().allMatch((elemento) -> elemento.contains("A")));

        // Retorna true se ALGUM dos elementos possuem a letra A minúscula no nome
        System.out.println("Tem algum elemento com 'a' minúsculo no nome?" + estudantes.stream().anyMatch((elemento) -> elemento.contains("a")));

        // Retorna true se NENHUM elemento possui a letra 'a' minúscula no nome
        System.out.println("Não tem nenhum elemento com 'a' minúsculo no nome?" + estudantes.stream().noneMatch((elemento) -> elemento.contains(("a"))));

        // Retorna o primeiro elemento da coleção, se existir exibe no console
        System.out.println("Retorna o primeiro elemento da coleção: ");
        estudantes.stream().findFirst().ifPresent(System.out::println);

        // Exemplo de operações encadeadas: perceber que os métodos estão trabalhando de forma assíncrona, concorrentemente
        System.out.println("Operação encadeada: ");
        System.out.println(estudantes.stream()
                                     .peek(System.out::println)
                                     .map(estudante ->
                                            estudante.concat(" - ").concat(String.valueOf(estudante.length())))
                                     .peek(System.out::println)
                                     .filter((estudante) ->
                                            estudante.toLowerCase().contains("r"))
                                     //.collect(Collectors.toList()));

        // Algumas outras formas de coletar
        //                           .collect(Collectors.toList());
        //                           .collect(Collectors.joining(", "));
        //                           .collect(Collectors.toSet());
                                     .collect(Collectors.groupingBy(estudante -> estudante.substring(estudante.indexOf("-") + 1))));
    }
}
```
