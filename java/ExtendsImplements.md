# Extends
Usa-se extends quando você deseja aplicar herança á sua classe.

Quando falamos que a classe A estende a classe B, significa que A herda alguns (ou todos) métodos e atributos da classe B.

Os únicos métodos e atributos que não são herdados são os que possuem o modificador de acesso private.

Pode-se aplicar diversos níveis de herança. Por exemplo:

```
class A extends B { }
class B extends C { }
class C extends D { }
```

Ao fazer isso, os membros com modificador de acesso public das classes D, C e B são acessíveis na classe A. Os membros com modificador de acesso protected da classe B também são acessíveis na classe A.

Em Java é possível herdar apenas de uma classe. Não existe herança múltipla.

## Implements
Usa-se implements quando você deseja implementar uma interface.

Não implementa-se classes. Implementa-se apenas interfaces.

Uma interface "firma um contrato" entre classes em que define comportamentos (métodos) que devem ser sobrescritos pela classe que os herda (se essa for uma classe concreta).

Uma interface pode conter métodos e constantes. Constantes em Java são definidas pelas palavras static e final. Ex: *public static final String NOME = "xpto";*.

**Os métodos de uma interface não tem corpo. Eles tem apenas a sua definição.** Ex:

```
public interface Imprimivel {
    public void imprime();
}
```
Pode-se também aplicar herança entre interfaces (exclusivamente):

```
public interface Monstro {
    public void ameacar();
}

public interface MonstroPerigoso extends Monstro {
    public void destruir();
}

public class Godzilla implements MonstroPerigoso {
    @Override
    public void ameacar() {
        //implementação
    }
    
    @Override
    public void destruir() {
        //implementação
    }
}
```

Adendo: a keyword extends é usada para quando um tipo (classe ou interface) é derivado do seu mesmo tipo, e o implements é sempre que deseja fazer uma implementação, no caso uma classe implementa uma interface.

Possibilidades de uso das keywords:

```
class Classe {}
class SubClasse extends Classe {}

interface Interface {}
interface SubInterface extends Interface {}

class SubClasse2 implements Interface {}
class SubClasse3 extends SubClasse implements Interface {}
``` 

Por a interface nunca possuir implementação não faria sentido que ela em alguma hipótese tenha um método ou atributo que somente ela use (privado), pois tudo que a interface faz é declarar métodos e atributos para que seja implementados por classes.

[Fonte](https://pt.stackoverflow.com/questions/193193/qual-%C3%A9-a-diferen%C3%A7a-entre-as-keywords-extends-e-implements-em-java)