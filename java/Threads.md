# Threads

Thread é um pequeno programa que trabalha como um subsistema, sendo uma forma de um processo se autodividir em duas ou mais tarefas.

Essas tarefas múltiplas podem ser executadas simultaneamente para rodar mais rápido do que um programa em um único bloco ou praticamente juntas.

A Classe Thread do Java possui vários métodos úteis, como *start, stop, run, isAlive*... Como parâmetro, é possível passar um objeto que implementa a interface *Runnable* (mais especificamente o método *run*) para a thread, onde ela irá executar o *run* deste objeto.

Exemplo prático: uma Thread responsável pela geração de um relatório (PDF) e outra imprime uma barra de Loading, enquanto a primeira thread estiver sendo executada. O ponto chave deste programa é o *while*.

```java
public class Threads {
    public static void main(String[] args) {

        GeradorPDF iniciarGeradorPdf = new GeradorPDF();
        BarraDeCarregamento iniciaBarraDeCarregamento = new BarraDeCarregamento(iniciarGeradorPdf);

        iniciarGeradorPdf.start();
        iniciaBarraDeCarregamento.start();

    }
}

class GeradorPDF extends Thread {

    @Override
    public void run() {

        try {
            System.out.println("Gerando PDF...");
            Thread.sleep(5000);
        } catch (Exception e) {
            e.printStackTrace();
        }
        System.out.println("PDF Gerado!");
    }

}


class BarraDeCarregamento extends Thread {

    private Thread iniciarGeradorPdf;

    // Passando a Thread de GeradorPDF como o construtor da Barra
    public BarraDeCarregamento(Thread iniciarGeradorPdf) {
        this.iniciarGeradorPdf = iniciarGeradorPdf;
    }

    @Override
    public void run() {

        // A barra de loading irá ser executada enquanto a Thread do GeradorPDF estiver executando
        while (true) {

            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            if (!iniciarGeradorPdf.isAlive()) {
                break;
            }

            System.out.println("Loading ...");
        }
    }

}

```
