# Set

Interfaces que serão abordadas:

*java.util.HashSet*

*java.util.TreeSet*

*java.util.LinkedHashSet*

![Diferenças entre HashSet, LinkedHashSet e TreeSet](https://i.imgur.com/iCCDCe3.png)

Por padrão, não garantem ordem. Caso seja necessária a utilização de ED que precisam ser ordenadas, outras alternativas devem ser considerada, visto que isto penaliza bastante a performance do Set.

A razão disto é que o Set foi pensado para grandes conjuntos de dados. A ordenação deste é custosa, o que penaliza a ED.

Permitem adição e remoção normalmente. Não possui busca por item e atualização. Para leitura, apenas navegação.

Não permitem itens repetidos, o que torna a leitura mais performática. Por esta razão, todos os itens adicionados são indexados na estrutura, agilizando a pesquisa.

Curiosidade: o ResultSet (um set!), muito utilizado em bancos de dados relacionais, precisa ter uma alta performance, garantida pela explicação acima.

## Exemplo HashSet

```java
import java.util.HashSet;
import java.util.Iterator;
import java.util.Set;

// Implementação mais usada em produção: HashSet
public class TesteHashSet {
    public static void main(String[] args) {

        Set<Double> notasAlunos = new HashSet<>();

        // Adiciona as notas no set
        notasAlunos.add(10.0);
        notasAlunos.add(5.8);
        notasAlunos.add(2.7);
        notasAlunos.add(9.3);
        notasAlunos.add(3.8);

        // A ordem desejada é DIFERENTE da que foi realmente inserida:   [10.0, 5.8, 9.3, 3.8, 2.7]
        System.out.println(notasAlunos);

    }
}
```

## Exemplo LinkedHashSet

```java
import java.util.LinkedHashSet;
import java.util.Set;

// Utilizada em casos em que a ordem importa. O custo é maior se comparada à HashSet
public class TesteLinkedHashSet {
    public static void main(String[] args) {

        Set<Double> notasAlunos = new LinkedHashSet<>();

        // Adiciona as notas no set
        notasAlunos.add(10.0);
        notasAlunos.add(5.8);
        notasAlunos.add(2.7);
        notasAlunos.add(9.3);
        notasAlunos.add(3.8);

        // A ordem desejada é a mesma da que foi realmente inserida:   [10.0, 5.8, 9.3, 3.8, 2.7]
        System.out.println(notasAlunos);

    }
}
```

## TreeSet

Segue as implementações de uma Árvore binária!

Pontos a ser considerado: a leitura é performática, no entanto, a cada nó ou elemento da árvore que é editado (adicionado/removido), a árvore é ordenada novamente e rebalanceada, aumentando o custo computacional.

Exemplo:

```java
import java.util.TreeSet;

public class TesteTreeSet {
    public static void main(String[] args) {

        TreeSet<String> treeCapitais = new TreeSet<>();

        treeCapitais.add("Porto Alegre");
        treeCapitais.add("Belo Horizonte");
        treeCapitais.add("São Paulo");
        treeCapitais.add("Rio de Janeiro");
        treeCapitais.add("Florianópolis");

        System.out.println(treeCapitais);

        // Retorna a 1ª capital no Topo da árvore
        System.out.println(treeCapitais.first());

        // Retorna a última capital no Final da árvore
        System.out.println(treeCapitais.last());

        // Retorna a 1ª capital abaixo da árvore da capital parametrizada
        System.out.println(treeCapitais.lower("São Paulo"));

        // Retorna a 1ª capital acima da árvore da capital parametrizada
        System.out.println(treeCapitais.higher("Belo Horizonte"));

        // Retorna a 1ª capital no Topo da árvore, removendo do set
        System.out.println(treeCapitais.pollFirst());

        // Retorna a 1ª capital no Final da árvore, removendo do set
        System.out.println(treeCapitais.pollLast());
    }

}
```
