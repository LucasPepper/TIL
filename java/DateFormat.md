# DateFormat

Disponível no pacote java.text, veio para facilitar o processo de formatação de datas.

Duas principais classes: **DateFormat** e a **SimpleDateFormat**.

Ambas oferecem maneiras de formatar e parsear a saída das datas.

O DateFormat é mais limitado, ele somente flexibiliza em relação a SHORT ou LONG.

Ex:

```java

import java.util.Date;
import java.text.DateFormat;

public class TesteFormat {
    public static void main(String[] args) {

        Date dataAgora = new Date();

        String dateToStr = DateFormat.getInstance().format(dataAgora);

        System.out.println(dateToStr);  // 29/06/2020 15:05

        // Date em um padrão LONG, Time em um padrão SHORT
        dateToStr = DateFormat.getDateTimeInstance(DateFormat.LONG, DateFormat.SHORT).format(dataAgora);

        System.out.println(dateToStr);  // 29 de Junho de 2020 15:05
    }
}

```

## SimpleDateFormat

Consegue-se obter a exata formatação desejada.

Exemplo extenso:

```java

import java.text.SimpleDateFormat;  
import java.util.Date;

public class TesteSimpleDateFormat {  
   public static void main(String[] args) {
       //Getting the current date
       Date date = new Date();  

       //Specifying the format of the date using SimpleDateFormat
       SimpleDateFormat sdf = new SimpleDateFormat("MM-dd-yyyy");

       //Formatting the date to the specified format
       String dateString = sdf.format(date);  
       System.out.println("Date in the format of MM-dd-yyyy : " + dateString);  
  
       sdf = new SimpleDateFormat("dd/MM/yyyy hh:mm:ss");  
       dateString = sdf.format(date);  
       System.out.println("Date in the format of dd/MM/yyyy hh:mm:ss : " + dateString);  
  
       sdf = new SimpleDateFormat("dd, MMMM, yyyy");  
       dateString = sdf.format(date);  
       System.out.println("Date in the format of dd, MMMM, yyyy : " + dateString);  
  
       //Format with time zone
       sdf = new SimpleDateFormat("dd, MMMM, yyyy zzzz");  
       dateString = sdf.format(date);  
       System.out.println("Date in the format of dd, MMMM, yyyy zzzz : " + dateString);  
  
       //DateFormat day, date, time and time zone
       sdf = new SimpleDateFormat("E, dd/MMM/yyyy HH:mm:ss z");  
       dateString = sdf.format(date);  
       System.out.println("Date in the format of E, dd/MMM/yyyy HH:mm:ss z : " + dateString);  

       //DateFormat date and time zone
       sdf = new SimpleDateFormat("dd MMM yyyy z");  
       dateString = sdf.format(date);  
       System.out.println("Date in the format of dd MMM yyyy z : " + dateString);
   }  
}

```

[Doc DateFormat](https://docs.oracle.com/javase/8/docs/api/java/text/DateFormat.html)

[Doc SimpleDateFormat](https://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html)

[Exemplos](https://beginnersbook.com/2013/05/simple-date-format-java/)
