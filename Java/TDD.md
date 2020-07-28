# TDD

O TDD(Test Driven Development) é uma metodologia muito utilizada para se atingir grande qualidade de software, visto que os testes são tão importantes quanto o código em si nesta abordagem.

![TDD](https://miro.medium.com/max/384/1*ieVWcSsJmeBbZFo6a_dL5g.png)

Primeiro escreve-se o teste, onde ele irá falhar. Logo após, escreve-se um código com o **nº mínimo de passos (*baby steps*) para fazê-lo passar**. A ideia é que cada teste escrito cubra todo o código que está sendo escrito. Como último passo, é feita a refatoração.

OBS: tomar cuidado ao escrever o código que irá passar no teste. Ele deve conter o mínimo de passos para passar **somente naquele** teste, e não em todos os outros que já existem ou virão a existir! Essa é uma regra básica do TDD!

Repetir esse ciclo ao adicionar uma feature nova. Deste modo, o código irá evoluindo com a garantia de já estar sendo acobertado pelos testes.

No Java, usualmente utiliza-se o [JUnit](https://github.com/LucasPepper/TIL/blob/master/java/Junit.md) para auxiliar na escrita dos testes. Segue um exemplo (Calculadora - Soma):

```java
public class CalculadoraNovaTest {

    @Test
    public void deveSomarDoisValores() {
        int valorA = 1;
        int valorB = 2;

        int soma = 0;

        // Obviamente este teste irá falhar (soma == 0)
        assertEquals(3, soma);
    }
}

```

Então, escrevemos um código mínimo para fazê-lo passar no teste:

```java
public class CalculadoraNovaTest {

    @Test
    public void deveSomarDoisValores() {
        int valorA = 1;
        int valorB = 2;

        int soma = valorA + valorB;

        // Teste OK!
        assertEquals(3, soma);
    }
}

```

Próximo passo/teste: somar 3 ou mais valores. Será necessário passar um *array* como parâmetro neste caso.

Para maior organização (refatoração), foi criada uma nova Classe *CalculadoraNova*:

```java
public class CalculadoraNova {

    public int somar(int ...valores) {

        int soma = 0;

        for (var valor : valores) {
            soma += valor;
        }

        return soma;
    }
}
```

Novo teste para 3 valores:

```java

    @Test
    public void deveSomarTresValores() {

        int valorA = 1;
        int valorB = 2;
        int valorC = 3;

        var calc = new CalculadoraNova();
        int soma = calc.somar(valorA, valorB, valorC);

        assertEquals(6, soma);  // OK!
    }

```
