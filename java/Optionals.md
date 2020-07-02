# Optionals

Tratamento com objetos conhecidos como opcionais, que podem ser nulos. Exemplo: data de demissão de um funcionário, que ainda trabalha na empresa.

Possui dois estados: Presente e Vazio.

Permite que você execute operações em valores que podem ser nulos sem preocupação com as famosas NullPointerExceptions.

Exemplo com alguns métodos úteis:

```java
import java.util.Optional;

public class TesteOptional {
    public static void main(String[] args) {

        // Valor do estado Presente
        Optional<String> optionalString = Optional.of("Valor presente");

        // Se presente, retornar o primeiro parâmetro. Se não (vazio), retornar o segundo
        optionalString.ifPresentOrElse(System.out::println, () -> System.out.println("não está presente"));

        // .ofNullable: se nulo, constrói o método (Factory Method) a partir do .empty(). Se não nulo, construir a partir do .of()
        // return value == null ? empty() : of(value);
        Optional<String> optionalNull = Optional.ofNullable(null);
        optionalNull.ifPresentOrElse(System.out::println, () -> System.out.println("null = não está presente"));

        // Casos em que o valor pode ser vazio
        Optional<String> emptyOptional = Optional.empty();
        emptyOptional.ifPresentOrElse(System.out::println, () -> System.out.println("empty = não está presente"));

        // NullPointerException
        Optional<String> optionalNullErro = Optional.of(null);
        optionalNullErro.ifPresentOrElse(System.out::println, () -> System.out.println("erro = não está presente"));

        // Métodos booleanos auxiliares
        System.out.println(optionalString.isPresent());
        System.out.println(optionalString.isEmpty());

        // Se houver valor presente, retorne esse valor
        // o .get() aqui pode retornar NoSuchElementException() caso o valor estiver vazio
        if (optionalString.isPresent()) {
            String valor = optionalString.get();

            System.out.println(valor);
        }

        // Mapping (Funcional): pegar um valor, aplicar algum algoritmo que o transforme em outro valor
        optionalString.map((valor) -> valor.concat("***").ifPresent(System.out::println));

        // Se o valor estiver presente, retorná-lo. Se não, lançar uma nova exceção parametrizada
        System.out.println(optionalString.orElseThrow(IllegalStateException::new));
    }
}
```

Exemplo com Int, Double e Long:

```java
import java.util.OptionalDouble;
import java.util.OptionalInt;
import java.util.OptionalLong;

public class TesteOptionalPrimitivos {
    public static void main(String[] args) {

       System.out.println("***Valor Inteiro opcional***");
       OptionalInt.of(12).ifPresent(System.out::println);

       System.out.println("***Valor Decimal opcional***");
       OptionalDouble.of(55.0).ifPresent(System.out::println);

       System.out.println("***Valor Long opcional***");
       OptionalLong.of(23L).ifPresent(System.out::println);
    }
}
```
