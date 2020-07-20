# Default

Os métodos *default* introduzidos no Java 8 são uma nova forma de fazer implementações de métodos dentro de *interfaces*, o que permite mais flexibilidade aos API designers do Java. Esta é uma forma de contornar a limitação de não ser possível a Herança Múltipla no Java, mas sim a implementação de múltiplas interfaces.

Exemplos [DevMedia](https://www.devmedia.com.br/metodos-default-no-java/33012):

```java

interface TV {
    void ligar();
    default void desligar() { System.out.println(“desligar”); }
}

class LG implements TV {
    @Override
    public void ligar() { }
}
  
class Sony implements TV {
    @Override
    public void ligar() { }
}
  
public class Teste {
    public static void main(String[] args) {
        new LG();
        new Sony();
    }
}
```

Observação: as classes LG e Sony herdam automaticamente o comportamento *default* de desligar da interface TV e **podem ou não sobrescrever esse comportamento**. Essa característica ajuda na questão da retrocompatibilidade entre diferentes versões do Java (legadas - recentes).

Por exemplo, o método *forEach* da interface *Iterable* é um método *default* que recebe a *interface funcional* *Consumer*, permitindo que utilizemos lambdas, conforme mostra a Listagem 4.

```java
import java.util.ArrayList;
import java.util.List;
  
public class Exemplo {

    public static void main(String[] args) {

        List<String> strings = new ArrayList<>();
        for(int i = 0; i < 10; i++) strings.add(String.valueOf(i));

        // Sem lambda
        for (String string : strings) {
            System.out.println("Valor: " + string);
        }
  
        // Com lambda
        strings.forEach((string) -> {
            System.out.println("Valor: " + string);
        });
    }
}
```

Obs: caso haja conflito de assinaturas de métodos (uma classe implementando duas ou mais interfaces que possuem a mesma assinatura de um método) é necessário implementar o método na classe que está implementando as interfaces OU escolher explicitamente uma das implementações herdadas através de *super*.

Ex:

```java
  
interface Carro {
    default void acelerar() {
        System.out.println("Carro acelerando");
    }
}
  
interface Barco {
    default void acelerar() {
        System.out.println("Barco acelerando");
    }
}
  
class BarcoMovel implements Carro, Barco {

}

// ERRO: “class BarcoMovel inherits unrelated defaults for acelerar() from types Carro and Barco“
public class Exemplo {
    public static void main(String[] args) {
        new BarcoMovel().acelerar();
    }  
}
```

Solução 1: Implementando o método na classe que está herdando as interfaces

```java
class BarcoMovel implements Carro, Barco {
    @Override
    public void acelerar() {
        System.out.println("BarcoMovel acelerando");
    }
}
```

Solução 2: Escolhendo uma das implementações com o *super*

```java
class BarcoMovel implements Carro, Barco {
    @Override
    public void acelerar() {
        Barco.super.acelerar();
        //Carro.super.acelerar();
    }
}
```
