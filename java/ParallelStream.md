# ParallelStream

Possui processamento semelhante ao das Streams introduzidas no Java 8, porém se beneficia de Concorrência ou Paralelismo utilizando threads, aumentando a eficiência.

Ex: comparação de tempo de cálculo de fatoriais utilizando Parallel Streams

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.IntStream;

public class ParallelStreams {
    public static void main(String[] args) {
        
        long inicio = System.currentTimeMillis();
        IntStream.range(1, 150000).forEach(num -> fatorial(num));   // Serial Stream
        long fim = System.currentTimeMillis();
        System.out.println("Tempo de execução Serial: " + (fim - inicio));  // 10090ms

        inicio = System.currentTimeMillis();
        // .parallel() : retorna uma stream parallel equivalente
        IntStream.range(1, 150000).parallel().forEach(num -> fatorial(num));   // Parallel Stream
        fim = System.currentTimeMillis();
        System.out.println("Tempo de execução Parallel: " + (fim - inicio));    // 3327ms

        /* Obs: é importante lembrar que o processamento concorrente não segue uma ordem padrão ou linear (Processamento das Threads).
        ** Então não é recomendado utilizar Parallel Streams em casos onde a ORDEM é importante.
        */

        List<String> nomes = Arrays.asList("Lucas", "Pimenta", "de", "Souza");
        // Uma collection pode ser associada a um Parallel Stream diretamente
        nomes.parallelStream().forEach(System.out::println);    // Print: de Lucas Souza Pimenta
    }

    public static long fatorial(long num) {
        long fat = 1;

        for (long i = 2; i <= num; i++) {
            fat *= i;
        }

        return fat;
    }
}
