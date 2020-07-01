# Queue

Garante ordem de inserção. Permite adição, leitura e remoção considerando a regra básica de uma fila: Primeiro que entra, primeiro que sai (FIFO).

Não permite mudança de ordenação! O método .set(index, value) por exemplo não existe nas queues.

Ex:

```java
import java.util.Iterator;
import java.util.LinkedList;
import java.util.Queue;

public class TesteQueue {
    public static void main(String[] args) {

        // A LinkedList implementa a interface Queue, que por sua vez, extende Collection
        Queue<String> filaBanco = new LinkedList<>();

        filaBanco.add("Lucas");
        filaBanco.add("Patrícia");
        filaBanco.add("Flávio");
        filaBanco.add("Pâmela");
        filaBanco.add("Anderson");

        System.out.println(filaBanco);

        // Poll: retorna o 1º elemento e o remove da fila
        String clienteASerAtendido = filaBanco.poll();

        System.out.println("Cliente sendo atendido: " + clienteASerAtendido);

        System.out.println(filaBanco);

        // Peek: retorna o 1º elemento. Caso a fila estiver vazia, retorna null
        String primeiroCliente = filaBanco.peek();

        // Element: retorna o 1º elemento. Caso a fila estiver vazia, retorna uma exceção: NoSuchElementException
        String primeiroClienteOuErro = filaBanco.element();

        Iterator<String> iteratorFilaBanco = filaBanco.iterator();

        while (iteratorFilaBanco.hasNext()) {
            System.out.println(iteratorFilaBanco.next());
        }

        System.out.println(filaBanco.size());

        System.out.println(filaBanco.isEmpty());

    }
}
```
