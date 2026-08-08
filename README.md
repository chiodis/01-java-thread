# 01-java-thread

## Compilação:
javac *.java

## Execução:
java Main


# Exercícios:

Em Java, implemente as aplicações abaixo.
Em Markdown, explique suas soluções.

## 1) Thread calculadora

Altere Tarefa para receber dois números e uma operação (+, -, *, /).
Em cada passo do laço, calcule um valor diferente (por exemplo, n1 + i, n2 * i, etc.).
Mostre o resultado parcial no console em vez de apenas “processando passo”.

public class TarefaCalculadora implements Runnable {
    private int n1, n2;
    private char operacao;

    public TarefaCalculadora(int n1, int n2, char operacao) {
        this.n1 = n1;
        this.n2 = n2;
        this.operacao = operacao;
    }

    @Override
    public void run() {
        for (int i = 1; i <= 3; i++) {
            
            int valorAtual = n1 + i; 
            int resultado = 0;

            
            if (operacao == '+') resultado = valorAtual + n2;
            else if (operacao == '-') resultado = valorAtual - n2;
            else if (operacao == '*') resultado = valorAtual * n2;
            else if (operacao == '/') resultado = valorAtual / n2;

            
            System.out.println("[Calc] Passo " + i + ": " + valorAtual + " " + operacao + " " + n2 + " = " + resultado);
        }
    }
}

### dai podemos colocar isso no main: 

public class Main {

    public static void main(String[] args) {
            
        Thread t1 = new Thread(new TarefaCalculadora(10, 5, '+'));
        
        t1.start();
    
    }
}


## 2) Thread jogo de adivinhação

Faça cada Tarefa gerar um número secreto ao iniciar.
No laço, execute tentativas de adivinhação aleatórias até trocar 3 palpites.
Exiba se cada palpite foi “maior”, “menor” ou “acertou” e finalize quando acertar.

import java.util.Random;
 
class Tarefa extends Thread {
@Override
    public void run() {
 
        Random random = new Random();
 
        
        int numeroSecreto = random.nextInt(10) + 1;
 
        System.out.println(getName() + " - Número secreto gerado!");
 
        for (int i = 1; i <= 3; i++) {
 
            int palpite = random.nextInt(10) + 1;
 
            System.out.println(getName() + " - Palpite: " + palpite);
 
            if (palpite > numeroSecreto) {
                System.out.println(getName() + " - maior");
            }
            else if (palpite < numeroSecreto) {
                System.out.println(getName() + " - menor");
            }
            else {
                System.out.println(getName() + " - acertou!");
                return;
            }
        }
 
        System.out.println(getName() + " - Não acertou em 3 tentativas.");
    }
}
### na main
Thread t2 = new Thread(new TarefaAdivinhacao());

t2.start();


## 3) Thread contador de caracteres

Modifique Tarefa para receber uma string.
Conte e exiba a quantidade de caracteres da string.

private String texto;
 
public Tarefa(String texto) {
    this.texto = texto;
}
 
@Override
public void run() {
    int quantidade = texto.length();
 
    System.out.println("Texto: " + texto);
    System.out.println("Quantidade de caracteres: " + quantidade);
}

### na main: 

Tarefa tarefa3 = new Tarefa("LucasVitorBeatrizSamuel");
 
tarefa3.start();


## 4) Thread soma de vetores

Faça Tarefa receber dois vetores de inteiros.
Some elemento a elemento e imprima o resultado parcial de cada índice.
Explique como essa tarefa pode ser paralelizada com várias threads para vetores grandes.

public class TarefaSomaVetor implements Runnable {
    private int[] v1, v2;

    public TarefaSomaVetor(int[] v1, int[] v2) {
        this.v1 = v1;
        this.v2 = v2;
    }

    @Override
    public void run() {
        for (int i = 0; i < v1.length; i++) {
            int soma = v1[i] + v2[i];
            System.out.println("[Vetor] Índice [" + i + "]: " + v1[i] + " + " + v2[i] + " = " + soma);
        }
    }
}
### na main
int[] v1 = {1, 2, 3};
        int[] v2 = {4, 5, 6};
        Thread t4 = new Thread(new TarefaSomaVetor(v1, v2));

t4.start();    


## 5) Thread soma de matrizes

Faça Tarefa receber duas matrizes de inteiros.
Some elemento a elemento e imprima o resultado parcial de cada índice.
Explique como essa tarefa pode ser paralelizada com várias threads para matrizes grandes.

public class TarefaSomaMatriz implements Runnable {
    private int[][] m1, m2;

    public TarefaSomaMatriz(int[][] m1, int[][] m2) {
        this.m1 = m1;
        this.m2 = m2;
    }

    @Override
    public void run() {
        for (int i = 0; i < m1.length; i++) {
            for (int j = 0; j < m1[i].length; j++) {
                int soma = m1[i][j] + m2[i][j];
                System.out.println("[Matriz] Índice [" + i + "][" + j + "]: " + m1[i][j] + " + " + m2[i][j] + " = " + soma);
            }
        }
    }
}

nt[][] m1 = {{1, 2}, {3, 4}};
        int[][] m2 = {{5, 6}, {7, 8}};
        Thread t5 = new Thread(new TarefaSomaMatriz(m1, m2));

t5.start();

