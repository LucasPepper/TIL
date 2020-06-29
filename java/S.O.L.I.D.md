# S.O.L.I.D

SOLID é um acrônimo dos princípios da POO descritas por Robert C. Martin.

Auxiliam o programador a escrever códigos mais limpos, facilitando a refatoração e estimulando o reaproveitamento de código.

## Single Responsibility Principle

Uma classe deve ter um, e somente um, motivo para mudar.

A classe deve possuir uma única responsabilidade dentro do software.

Ex: imaginar uma classe OrdemDeCompra, que possui métodos para adicionar/remover produtos, que salvam as ordens em um BD e que mandam e-mails para pessoas cadastradas.

Este exemplo está violando o princípio. O certo seria uma classe responsável para add/remover produtos, outra para fazer o CRUD em relação a um BD e outra para enviar e-mails.

## O.C.P Open Closed Principle

"You should be able to extend a class behavior, without modifying it."

Objetos devem estar **abertos para extensão**, mas **fechados para modificação**.

Quando novos comportamentos precisam ser adicionados no software, **devemos estender e não alterar o código fonte original**.

Ex: imagine um controller responsável por descontos em livros infantis e de auto-ajuda. Dado que depois foi preciso adicionar descontos em livros de ação.

Para respeitar o O.C.P, é necessário criar uma interface e implementá-la em uma outra classe, sem que haja necessidade de alterar o código fonte original.

Sem a interface, seria necessário criar um método novo para cada novo tipo de livro no controller, o que viola o princípio O.C.

```java
public interface DescontoLivro {

    // Método geral
    double valorDesconto();
}

public class DescontoLivroAutoAjuda implements DescontoLivro {

    @Override
    public double valorDesconto() {
        return 0.5;
    }
}

public class DescontoLivroAcao implements DescontoLivro {

    @Override
    public double valorDesconto() {
        return 0.2;
    }
}

public class ControladorDeDesconto {

    public void adicionaDescontoLivro(DescontoLivro descontoLivro) {
        descontoLivro.valorDesconto();
    }
}
```

## L.S.P Liskov Substitution Principle

"Derived classes must be substitutable for their base classes."

Classes derivadas devem ser substituíveis por suas classes base.

Um exemplo onde podemos ver a violação desse princípio é uma classe Quadrado herdando de uma classe Retângulo (Todo quadrado É um retângulo).

Imagine que o método calculaArea() do quadrado leve em conta somente a Largura, repetindo esse valor para a sua altura.

O mesmo não acontece para retângulos, o resultado será diferente (ex: 5 * 5 vs 5 * 10).

Para resolver este problema, poderia ser criada uma interface calculaArea, e implementada de maneira correta por cada classe.

## I.S.P Interface Segregation Principle

"Make fine grained interfaces that are client specific."

Faça interfaces refinadas que são específicas do cliente.

Uma classe **não deve** ser forçada a **implementar** interfaces e **métodos** que **não serão utilizados**.

É melhor criar **interfaces** mais **específicas** ao **invés de** termos uma única **interface genérica**.

Ex: caso em que há uma interface para Aves, com os métodos bicar(), chocarOvos() e voar(). Esta interface não é adequada, por exemplo, para o Pinguim.

Logo, é melhor criar uma outra interface mais específica, AvesVoam, que irá implementar a interface Ave, contendo os métodos bicar() e chocarOvos().

```java
public interface Ave {

    void bicar();

    void chocarOvos();
}

public interface AvesVoam extends Ave {

    void voar();
}

```

## D.I.P Dependency Inversion Principle

"Depend on abstractions, not on concretions."

Dependa de abstrações e não de implementações.

Um módulo de alto nível não deve depender de módulos de baixo nível, ambos devem depender da abstração.

OBS: Inversão de Dependência **não é** igual a Injeção de Dependência!

Ex:

```java
public class ProductRepository {

    private MySqlConnection mySqlConnection;

    public ProductRepository() {
        this.mySqlConnection = new MySqlConnection();
    }

    // ...
}
```

Repare que a classe acima está violando o Princípio Dependency Inversion, visto que a conexão ao BD está dependendo de uma CLASSE MySqlConnection, e não de uma abstração geral, por exemplo, de uma interface DbConnection.

Teríamos problemas se fosse alterar de MySQL para Oracle, por exemplo. Isto faria com que seja necessário alterar o código fonte original, violando o princípio Open Closed.

A abordagem a seguir atende aos princípios:

```java

public interface DbConnection {
    // métodos de conexão
}

public class MySqlConnection implements DbConnection {
    // ...
}

public class OracleConnection implements DbConnection {
    // ...
}

public class ProductRepository {

    private DbConnection dbConnection;

    public ProductRepository(DbConnection dbConnection) {
        this.dbConnection = dbConnection;
    }

    // ...
}
