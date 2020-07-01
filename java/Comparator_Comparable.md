# Comparator e Comparable (Interfaces)

São utilizados para comparar dois objetos diferentes. Comparam objetos que não são diretamente comparáveis, ou seja, de tipos diferentes, em que o método Collections.sort() não funcionaria.

Erro ao tentar utilizar o Collections.sort() em uma classe que não é nativamente implementada:

```
The method sort(List<T>) in the type Collections
  is not applicable for the arguments (ArrayList<Player>)

```

São úteis para ordenar dados pertencentes à classes criadas pelo usuário, por exemplo, sem ter que re-implementar todo o código de ordenação para adaptá-lo aos critérios desejados. Desta forma, fica mais fácil atender ao princípio Open Closed do [S.O.L.I.D.](https://github.com/LucasPepper/TIL/blob/master/java/S.O.L.I.D.md) (Objetos devem estar **abertos para extensão**, mas **fechados para modificação**)

## Comparable

Comparable é uma interface que define uma estratégia para comparar um objeto com outros objetos do mesmo tipo. Ela é conhecida como "Ordenação Natural" da classe.

Importante notar o uso do método compareTo(), que compara o objeto original a outro passado pelo argumento, **retornando menor (-1), igual (0) ou maior(1).**

```java
public class Player implements Comparable<Player> {
    //...
    @Override
    public int compareTo(Player otherPlayer) {
        return (this.getRanking() - otherPlayer.getRanking());
    }
}
```

Repare que o método compareTo() está sendo implementado dentro da classe Player.

## Comparator

Semelhante ao *Comparable*, porém exige dois argumentos (os dois objetos) para realizar a comparação. A grande vantagem é que com ele não é preciso modificar o código-fonte original. Basta criar uma classe que implementa o Comparator e passar como argumento os objetos que serão comparados.

Ele também é mais flexível quanto ao critério de comparação. É possível definir múltiplas estratégias, o que não é possível utilizando o *Comparable*.

```java
// Ranking Comparator
public class PlayerRankingComparator implements Comparator<Player> {
  
    @Override
    public int compare(Player firstPlayer, Player secondPlayer) {
       return (firstPlayer.getRanking() - secondPlayer.getRanking());
    }
}

// Age Comparator
public class PlayerAgeComparator implements Comparator<Player> {
    @Override
    public int compare(Player firstPlayer, Player secondPlayer) {
       return (firstPlayer.getAge() - secondPlayer.getAge());
    }
}
```

## Java 8 Comparators

Com o Java 8, surgiram novos jeitos de definição dos Comparators utilizando **expressões lambda**:

```java
Comparator<Player> byRanking
  = (Player player1, Player player2) -> player1.getRanking() - player2.getRanking();
```

O método *Comparator.comparing* exige um método relacionado à propriedade que irá ser comparada e retorna uma instância do *Comparator*:

```java
Comparator<Player> byRanking = Comparator
  .comparing(Player::getRanking);
Comparator<Player> byAge = Comparator
  .comparing(Player::getAge);

```

[GeeksForGeeks - Comparator Interface in Java](https://www.geeksforgeeks.org/comparator-interface-java/)
[Baeldung - Comparator and Comparable in Java](https://www.baeldung.com/java-comparator-comparable)
[Baeldung - Comparator.comparing()](https://www.baeldung.com/java-8-comparator-comparing)
