# Dates

java.util.date : desde Java 1.0

Existem vários construtores, mas que foram depreciados. Os que ainda são válidos, da classe Date, são somente esses dois a seguir:

Date(): este construtor vai alocar um objeto da classe Date e o inicializará com o milissegundo mais próximo do período da sua execução.

Date(long date): exige como parâmetro os milissegundos com base padrão de tempo (epoch) que usa como referência **1 de janeiro de 1970 00:00:00**

***Epoch**: o epoch timestamp é um padrão para representar uma data como um inteiro 32-bits a partir do início do Unix Epoch...*

Dica: utilizar em conjunto com *System.currentTimeMillis()*

Ex:

```

import java.util.Date;

public class Exemplo001 {
    public static void main(String[] args) {

        Date novaData = new Date();
        System.out.println(novaData);
    }
}

```

![Métodos Date](https://imgur.com/a/HFnBrAs)

Ex:

```

import java.util.Date;

public class TesteDate {
    public static void main(String[] args) {
        
        Date dataPassado = new Date(1513648741200L);

        System.out.println(dataPassado);
        // Mon Dec 18 23:59:01 BRST 2017

        Date dataFuturo = new Date(1783648741200L);

        System.out.println(dataFuturo);
        // Thu Jul 09 22:59:01 BRT 2026

        boolean isAfter = dataPassado.after(dataFuturo);

        System.out.println(isAfter);

        boolean isBefore = dataPassado.before(dataFuturo);

        System.out.println(isBefore);
    }
}

```

## Instant

Modela um ponto instantâneo de uma linha do tempo. Útil para gravar marcações tempoaris em eventos da sua aplicação.

Instanciar a classe Instant:

*Instant instant = dataInicio.toInstant();*

*System.out.println(instant);*
