# Datas no Java 8+

Antes do Java 8, tínhamos as classes Date e Calendar, que se mostraram confusas e trabalhosas, além de serem mutáveis.

O Java 8 veio com uma série de melhorias, incluindo o pacote java.time que foi herdado do projeto [Joda Time](https://www.joda.org/joda-time/).

Destacam-se três classes:

## LocalDate

Classe imutável para representar uma data.

Seu formato padrão é yyyy-MM-dd

Exemplo com alguns métodos:

```
import java.time.LocalDate;

public class ExLocalDate {
    public static void main(String[] args) {
        
        LocalDate hoje = LocalDate.now();

        System.out.println(hoje);   // 2020-06-29

        LocalDate ontem = hoje.minusDays(1);

        System.out.println(ontem);   // 2020-06-28

    }
}

```

## LocalTime

Classe imutável que representa um padrão de hora-minuto-segundo.

Pode ser representada até o nível de nanosegundos. Possui a utilização similar ao LocalDate.

Ex:

```

import java.time.LocalDate;
import java.time.LocalTime;

public class TesteLocalDateTime {

    public static void main(String[] args) {
        
        LocalDate hoje = LocalDate.now();
        System.out.println(hoje);

        LocalDate ontem = hoje.minusDays(1);
        System.out.println(ontem);
    
        LocalTime agora = LocalTime.now();
        System.out.println(agora);

        LocalTime maisUmaHora = agora.plusHours(1);
        System.out.println(maisUmaHora);
    }
}

```

## LocalDateTime

Junção do LocalDate com o LocalTime. Também é uma classe imutável, em que se pode trabalhar com datas e horários de uma só vez.

Ex:

```

import java.time.LocalDateTime;

public class TesteLocalDateTime {

    public static void main(String[] args) {
        
        LocalDateTime agora = LocalDateTime.now();
        System.out.println(agora);

        LocalDateTime futuro = agora.plusHours(1).plusDays(2).plusSeconds(12);

        System.out.println(futuro);
    }
}

```

[Doc LocalTime](https://docs.oracle.com/javase/8/docs/api/java/time/LocalTime.html)
[Doc LocalDate](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html)
[Doc LocalDateTime](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDateTime.html)