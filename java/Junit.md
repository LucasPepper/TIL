# JUnit - Unit Tests

O JUnit é um framework para testes unitários no Java, muito importante principalmente no processo de TDD. Para entender a importância dos testes unitários, basta imaginar um projeto de missão crítica, como os de engenharia aeronáutica. Durante a construção e montagem de um avião, **todos os seus componentes são testados isoladamente até a exaustão**(Testes Unitários), e depois cada etapa de integração também é devidamente testada e homolagada (Testes de Integração e Aceitação/Homologação).

Recomenda-se utilizar os testes unitários em duas situações principais: no Começo do projeto, projetando e escrevendo as classes de teste, e depois as classes com regras de negócios, e diariamente, em menor escala, onde cria-se "confiança" para fazer mudanças (os testes cobrirão possíveis erros), além de ser melhor a divisão de um grande problema, no final do projeto, em vários pequenos.

## Como adicionar o JUnit ao seu Projeto

Em casos de Projetos criados com o Maven/Gradle, geralmente são criados pacotes separados de código-fonte (produção) e Teste. 

Essa separação, além de deixar o projeto mais organizado, também permite que quando ocorra alguma build, toda a bateria de testes seja executada. Além do mais, são gerados relatórios dos testes permitindo uma análise posterior.

Classe a ser testada:

```java
package com.teste;

public class Calculadora {

    public int somar(String expressao) {
        int soma = 0;
        for (String valorSomar : expressao.split("\\+")) {
            soma += Integer.valueOf(valorSomar);
        }

        System.out.println(soma);
        return soma;
    }
}
```

No caso do IntelliJ, basta clicar com o botão direito na classe a ser testada e clicar em 'Run class with coverage', que determina também a porcentagem do quanto o código está coberto por testes. (Observar a anotação *@Test*)

```java
import org.junit.Test;

import static org.junit.Assert.*;

public class CalculadoraTest {
    @Test
    public void testSomar() {
        var calc = new Calculadora();
        int soma = calc.somar("1+1+3");
        // Asserts: suportam tipos primitivos, Objetos e Arrays
        assertEquals(5, soma);  // (valor esperado, valor real)

    }
}

```

Exemplos de Asserts:

```java
package com.teste;

import org.junit.Test;

import static org.junit.Assert.*;

public class AssertTest {
    @Test
    public void testAsserArrayEquals() {
        byte[] esperado = "teste".getBytes();
        byte[] atual = "teste".getBytes();
        assertArrayEquals(esperado, atual);
    }

    @Test
    public void testAssertEquals() {
        assertEquals("text", "text");
    }

    @Test
    public void testAssertFalse() {
        assertFalse(false);
    }

    @Test
    public void testAssertFNotNull() {
        assertNotNull(new Object());
    }

    @Test
    public void testAssertNotSame() {
        assertNotSame(new Object(), new Object());
    }

    @Test
    public void testAssertNull() {
        assertNull(null);
    }

    @Test
    public void testAssertSame() {
        Integer aNumber = Integer.valueOf(765);
        assertSame(aNumber, aNumber);
    }

    // Outro Assertion muito utilizado por sua flexibilidade: assertThat() 
}
```

## Rules

São argumentos que implementam a interface TestRule, usados para fazer o pré/pós processamento de testes. Exemplo: criação de pastas temporárias, registros em BD, antes ou depois de fazer algum tipo de teste em um módulo, por exemplo. Observar a anotação *@Rule*

```java
public class RuleTest {

    // Será criada uma pasta temporária, antes do teste, que será deletada após ele ser executado
    @Rule
    public TemporaryFolder tmpFolder = new TemporaryFolder();

    @Test
    public void shouldCreateNewFileInTemporaryFolder() throws IOException {
        File created = tmpFolder.newFile("file.txt");

        assertTrue(created.isFile());
        assertEquals(tmpFolder.getRoot(), created.getParentFile());
    }
}
```

## Expected Exceptions

Casos de try/catch ou exceptions que são esperadas por alguns tipos de teste (ex: *expected = NullPointerException.class*). Também é possível combinar Rules com Expected Exceptions.

Obs: caso ocorra alguma exceção que não foi esperada pelo teste, ele irá falhar.

```java
public class ExceptionTest {

    @Rule
    public ExpectedException thrown = ExpectedException.none();

    @Test(expected = IndexOutOfBoundsException.class)
    public void shouldTestExceptionMessage() throws IndexOutOfBoundsException {
        List<String> lista = new ArrayList<String>();

        thrown.expect(IndexOutOfBoundsException.class);
        thrown.expectMessage("Array vazio");
        lista.get(0);
    }
}

```

## Try/Catch Idiom

Semelhante à estrutura das Expected Exceptions, com a adição de Try/catch

```java
    @Test
    public void testExceptionMessage() {
        try {
            new ArrayList<Object>().get(0);
            fail("Esperado que IndexOutOfBoundsException seja lançada");
        } catch (IndexOutOfBoundsException ex) {
            assertThat(ex.getMessage(), is("Index: 0, Size: 0"));
        }
    }
```

[Add testing libraries - IntelliJ](https://www.jetbrains.com/help/idea/configuring-testing-libraries.html)
[JUnit Tutorial - DevMedia](https://www.devmedia.com.br/junit-tutorial/1432)
