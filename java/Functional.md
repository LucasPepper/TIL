# Functional

Definição de Eric Elliott: Programação funcional é o processo de construir software através de composição de **funções puras**, **evitando compartilhamento de estados, dados mutáveis e efeitos colaterais**. É *declarativa* ao invés de imperativa.

Funcional: é dada uma regra, uma declaração de como queremos que o programa se comporte.

## Conceitos Fundamentais

* Composição de funções: é criar uma nova função através da composição de outras. Ex: filtrar um array, pegando somente os números pares e multiplicando-os por 2.

```java
import java.util.Arrays;

public class ComposicaoDeFuncoes {
    public static void main(String[] args ) {
        int[] valores = {1, 2, 3, 4};

        Arrays.stream(valores)
                .filter(numero -> numero % 2 == 0)
                .map(numero -> numero * 2)
                .forEach(numero -> System.out.println(numero));
    }
}

```

* Funções Puras: São chamadas de pura se caso forem invocadas mais de uma vez e produzirem exatamente o mesmo resultado. 

```java

public class FuncoesPuras {
    public static void main(String[] args ) {

        BiPredicate<Integer, Integer> verificarSeEMaior = (parametro, valorComparacao) -> parametro > valorComparacao;

        System.out.println(verificarSeEMaior.test(13,26));
        System.out.println(verificarSeEMaior.test(13,26));
    }
}

```

* Imutabilidade: Significa que uma vez que uma variável receber um valor, ela vai possuir esse valor para sempre; ou quando criarmos um objeto ele não poderá ser modificado.

```java
import java.util.function.UnaryOperator;

public class Imutabilidade {
    public static void main(String[] args ) {

        int valor = 20;
        UnaryOperator<Integer> retornarDobro = v -> v * 2;

        System.out.println(retornarDobro.apply(valor));
        System.out.println(valor); // Valor não será alterado

    }
}

```

## Lambda no Java

Interfaces funcionais: São interfaces que possuem apenas um método abstrato. Ex:

```java

public interface Funcao {
        String gerar(String valor);
    }

```

Geralmente as interfaces funcionais possuem uma anotação em nível de classe (*@FunctionalInterface*), para forçar o compilador a apontar um erro se a interface não estiver de acordo com as regras de uma interface funcional.

```java
public class Lambda {
    public static void main(String[] args) {
        Funcao1 funcao1 = valor -> valor;
    }
}

@FunctionalInterface
interface Funcao1 {
    String gerar(String valor);
}
```