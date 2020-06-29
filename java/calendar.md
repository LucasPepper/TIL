# Calendar

Criada com o objetivo de resolver alguns problemas da classe Date. Foram utilizadas antes do Java 8.

É uma classe abstrata que provê métodos para converter data entre um instante específico.

Possui campos específicos como MONTH, YEAH, HOUR, etc.

Uma vantagem é a grande quantidade de informações que essa classe retorna, como DAY_OF_MONTH, HOUR_OF_DAY, dentre muitos outros.

É possível **manipular as datas**, por exemplo, somando ou subtraindo dias, meses, etc.

Ex:

```

import java.util.Calendar;

public class Exemplo001 {
    public static void main(String[] args) {

        Calendar agora = Calendar.getInstance();
        System.out.println("Data corrente: " + agora.getTime());

        agora.add(Calendar.DATE, -15);
        System.out.println("15 dias atrás: " + agora.getTime());

        agora.add(Calendar.MONTH, 4);
        System.out.println("4 meses depois: " + agora.getTime());


    }
}

```

## Formatação de Datas

Dica: é interessante formatar a impressão das datas. Existem vários prefixos, utilizando o printf:

```

import java.util.Calendar;

public class TesteDate {
    public static void main(String[] args) {
        
        Calendar agora = Calendar.getInstance();
        System.out.println("Data corrente: " + agora.getTime());

        // c	Standard date and time string formatted as day month date hh::mm:ss tzone year
        System.out.printf("%tc\n", agora);

        // F	year-month-day
        System.out.printf("%tF\n", agora);

        // D	month/day/year
        System.out.printf("%tD\n", agora);

        // r	hh:mm (12-hour format)
        System.out.printf("%tr\n", agora);

        // T	hh:mm:ss (24-hour format)
        System.out.printf("%tT\n", agora);
    }
}

```

[Prefixos](http://www.java2s.com/Tutorial/Java/0120__Development/FormattingTimeandDateTheTimeandDateFormatSuffixes.htm)