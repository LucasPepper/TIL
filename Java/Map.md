# Map

Disponível em *java.util.Map*, é implementada pelas seguintes interfaces:

*java.util.HashMap*
*java.util.TreeMap*
*java.util.HashTable*

Não extende de *Collections*, diferentemente de *Lists*.

Diferentemente das outras, essa interface armazena dois tipos de objetos: Chave e Valor, assim como valores repetidos, mas não permite repetição de chave.

Permite adição, busca por chave ou valor (esta busca é menos performática), atualização, remoção e navegação.

Também pode ser ordenado.

Exemplo interessante: em uma planilha, uma key seria uma coluna e os values seriam uma Lista de elementos.

## Exemplo HashMap

```java
import java.util.HashMap;
import java.util.Map;

public class TesteHashMap {
    public static void main(String[] args) {

        Map<String, Integer> campeoesMundialFifa = new HashMap<>();

        // Adiciona os campeões mundiais Fifa no mapa
        campeoesMundialFifa.put("Brasil", 5);
        campeoesMundialFifa.put("Alemanha", 4);
        campeoesMundialFifa.put("Itália", 4);
        campeoesMundialFifa.put("Uruguai", 2);
        campeoesMundialFifa.put("Argentina", 2);
        campeoesMundialFifa.put("França", 2);
        campeoesMundialFifa.put("Inglaterra", 1);
        campeoesMundialFifa.put("Espanha", 1);

        System.out.println(campeoesMundialFifa);

        // Atualiza o valor para a chave Brasil
        campeoesMundialFifa.put("Brasil", 6);

        // Busca por um valor
        campeoesMundialFifa.get("Argentina");

        // Retorna se uma Key existe ou não
        System.out.println(campeoesMundialFifa.containsKey("França"));

        // Retorna se um Value existe ou não
        System.out.println(campeoesMundialFifa.containsValue("10"));

        // Remove um par
        campeoesMundialFifa.remove("França");

        // Retorna o tamanho
        System.out.println(campeoesMundialFifa.size());
    }
}
```

Com relação aos *LinkedHashMap* e *TreeMap*, são bem análogos aos *LinkedHashSet* e *TreeSet*, disponíveis na interface [Set](https://github.com/LucasPepper/TIL/blob/master/java/Collections/Set.md).

Reforçando que estas duas interfaces também implementam a interface *Map*, logo possuem os mesmos métodos vistos acima.
