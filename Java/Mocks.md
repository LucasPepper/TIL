# Mock

Mock (mock objects = objetos dublês) é uma estratégia muito utilizada no cenário de testes de aplicações. Ela consiste em simular ou 'fingir' ser uma entidade, como um banco de dados, para agilizar o processamento de testes unitários.

Por exemplo: imaginar um cenário em que existem 100 ou 200 teste unitários em uma aplicação, e que se deseja aplicar uma nova regra de negócio. Para o build de todos estes testes levará um tempo considerável, ainda mais quando se fala em um DAO ou estrutura parecida que tenha acesso ao Banco de Dados. Inclusive a manipulação desenfreada de um BD é perigosa.

Exemplo retirado da [Alura](https://www.alura.com.br/conteudo/mock), relacionado a um cenário de testes de um Leilão:

```java
public class EncerradorDeLeilaoTest {

    @Test
    public void deveEncerrarLeiloesQueComecaramUmaSemanaAtras() {

        Calendar antiga = Calendar.getInstance();
        antiga.set(1999, 1, 20);

        Leilao leilao1 = new CriadorDeLeilao().para("TV de plasma")
            .naData(antiga).constroi();
        Leilao leilao2 = new CriadorDeLeilao().para("Geladeira")
            .naData(antiga).constroi();

        // mas como passo os leiloes criados para o EncerradorDeLeilao,
        // já que ele os busca no DAO?

        EncerradorDeLeilao encerrador = new EncerradorDeLeilao();
        encerrador.encerra();

        // Testes
        assertTrue(leilao1.isEncerrado());
        assertTrue(leilao2.isEncerrado());
    }
}
```

Dada a sensibilidade em manipular um banco de dados, não seria melhor simular um DAO, imitando o seu comportamento?

Uma ideia seria simular o banco de dados. Veja que, para a classe *EncerradorDeLeilao*, não importa como o DAO faz o serviço dela. O encerrador está apenas interessado em alguém que saiba devolver uma lista de leilões e que saiba persistir um leilão. Como isso é feito para o encerrador pouco importa.
Vamos criar uma classe que finge ser um DAO. Ela persistirá as informações em uma simples lista:

```java
public class LeilaoDaoFalso {

    private static List<Leilao> leiloes = new ArrayList<Leilao>();

    public void salva(Leilao leilao) {
        leiloes.add(leilao);
    }

    public List<Leilao> encerrados() {

        List<Leilao> filtrados = new ArrayList<Leilao>();
        for(Leilao leilao : leiloes) {
            if(leilao.isEncerrado()) filtrados.add(leilao);
        }

        return filtrados;
    }

    public List<Leilao> correntes() {

        List<Leilao> filtrados = new ArrayList<Leilao>();
        for(Leilao leilao : leiloes) {
            if(!leilao.isEncerrado()) filtrados.add(leilao);
        }

        return filtrados;
    }

    public void atualiza(Leilao leilao) { /* faz nada! */ }
}
```

Agora vamos fazer com que o *EncerradorDeLeilao* e o *EncerradorDeLeilaoTest* usem o DAO falso. Além disso, vamos pegar o total de encerrados agora pelo próprio *EncerradorDeLeilao*, uma vez que pegar pelo DAO não adianta mais (o DAO é falso!):

```java
public class EncerradorDeLeilaoTest {

    @Test
    public void deveEncerrarLeiloesQueComecaramUmaSemanaAtras() {

        Calendar antiga = Calendar.getInstance();
        antiga.set(1999, 1, 20);

        Leilao leilao1 = new CriadorDeLeilao().para("TV de plasma")
            .naData(antiga).constroi();
        Leilao leilao2 = new CriadorDeLeilao().para("Geladeira")
            .naData(antiga).constroi();

        // dao falso aqui!
        LeilaoDaoFalso daoFalso = new LeilaoDaoFalso();
        daoFalso.salva(leilao1);
        daoFalso.salva(leilao2);

        EncerradorDeLeilao encerrador = new EncerradorDeLeilao();
        encerrador.encerra();

        assertEquals(2, encerrador.getTotalEncerrados());
        assertTrue(leilao1.isEncerrado());
        assertTrue(leilao2.isEncerrado());
    }
}

public class EncerradorDeLeilao {
    public void encerra() {

        // DAO falso aqui!
        LeilaoDaoFalso dao = new LeilaoDaoFalso();
        List<Leilao> todosLeiloesCorrentes = dao.correntes();

        for(Leilao leilao : todosLeiloesCorrentes) {
            if(comecouSemanaPassada(leilao)) {
                leilao.encerra();
                total++;
                dao.atualiza(leilao);
            }
        }
    }

    // classe continua aqui...
}
```

## Mockito

O [Mockito](https://site.mockito.org/) é um framework de Mocks, que auxilia na criação e processamento de Mocks para criação de testes.

import static org.mockito.Mockito.*;

[Exemplo](https://javadoc.io/doc/org.mockito/mockito-core/latest/org/mockito/Mockito.html) de estruturas utilizadas:

```java
// You can mock concrete classes, not just interfaces
LinkedList mockedList = mock(LinkedList.class);

 // stubbing
when(mockedList.get(0)).thenReturn("first");
when(mockedList.get(1)).thenThrow(new RuntimeException());
```

Voltando ao exemplo do leilão... Devolvendo a lista de leilões criados quando o método *correntes()* for invocado:

```java
Calendar antiga = Calendar.getInstance();
    antiga.set(1999, 1, 20);

    Leilao leilao1 = new CriadorDeLeilao().para("TV de plasma")
        .naData(antiga).constroi();
    Leilao leilao2 = new CriadorDeLeilao().para("Geladeira")
        .naData(antiga).constroi();

    List<Leilao> leiloesAntigos = Arrays.asList(leilao1, leilao2);

    // criando o mock!
    LeilaoDao daoFalso = mock(LeilaoDao.class);
    // ensinando o mock a reagir da maneira que esperamos!
    when(daoFalso.correntes()).thenReturn(leiloesAntigos);
```

Veja que o método *when()*, também do Mockito, recebe o método que queremos simular. Em seguida, o método *thenReturn()* recebe o que o método falso deve devolver. Veja que simples! Agora, quando invocarmos *daoFalso.correntes()*, ele devolverá *leiloesAntigos*!

Levemos esse código agora para nosso método de teste:

```java
    @Test
    public void deveEncerrarLeiloesQueComecaramUmaSemanaAtras() {

        Calendar antiga = Calendar.getInstance();
        antiga.set(1999, 1, 20);

        Leilao leilao1 = new CriadorDeLeilao().para("TV de plasma")
            .naData(antiga).constroi();
        Leilao leilao2 = new CriadorDeLeilao().para("Geladeira")
            .naData(antiga).constroi();
        List<Leilao> leiloesAntigos = Arrays.asList(leilao1, leilao2);

        // criamos o mock
        LeilaoDao daoFalso = mock(LeilaoDao.class);
        // ensinamos ele a retornar a lista de leiloes antigos
        when(daoFalso.correntes()).thenReturn(leiloesAntigos);

        EncerradorDeLeilao encerrador = new EncerradorDeLeilao();
        encerrador.encerra();

        assertTrue(leilao1.isEncerrado());
        assertTrue(leilao2.isEncerrado());
        assertEquals(2, encerrador.getQuantidadeDeEncerrados());
    }
```

Finalizando, é preciso lembrar que o cenário de testes não é 100% fiel ao de produção. É preciso diferenciar os construtores (real - teste):

```java
public class EncerradorDeLeilao {

    private int encerrados;
    private final LeilaoDao dao;

    public EncerradorDeLeilao(LeilaoDao dao) {
        this.dao = dao;
    }

    public void encerra() {
        List<Leilao> todosLeiloesCorrentes = dao.correntes();

        for(Leilao leilao : todosLeiloesCorrentes) {
            if(comecouSemanaPassada(leilao)) {
                encerrados++;
                leilao.encerra();
                dao.salva(leilao);
            }
        }
    }

    // codigo continua aqui
}

public class EncerradorDeLeilaoTest {

    @Test
    public void deveEncerrarLeiloesQueComecaramUmaSemanaAtras() {

        Calendar antiga = Calendar.getInstance();
        antiga.set(1999, 1, 20);

        Leilao leilao1 = new CriadorDeLeilao().para("TV de plasma")
            .naData(antiga).constroi();
        Leilao leilao2 = new CriadorDeLeilao().para("Geladeira")
            .naData(antiga).constroi();
        List<Leilao> leiloesAntigos = Arrays.asList(leilao1, leilao2);

        LeilaoDao daoFalso = mock(LeilaoDao.class);
        when(daoFalso.correntes()).thenReturn(leiloesAntigos);

        EncerradorDeLeilao encerrador = new EncerradorDeLeilao(daoFalso);
        encerrador.encerra();

        assertTrue(leilao1.isEncerrado());
        assertTrue(leilao2.isEncerrado());
        assertEquals(2, encerrador.getQuantidadeDeEncerrados());
    }
}
