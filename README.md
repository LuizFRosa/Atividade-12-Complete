# Atividade-12-Complete

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h> // Para sistemas UNIX-like, incluindo Linux
#include <locale.h>

#define MAX_ALUNOS 5

// Declaração de funções
void menuPrincipal();
void digitarNotasAluno(float notas[][4], char nomes[][50], int *totalAlunos);
void mostrarNotasAlunos(float notas[][4], char nomes[][50], int totalAlunos);
void editarNotaAluno(float notas[][4], char nomes[][50], int totalAlunos);

int main() {
    setlocale(LC_ALL, ""); // Para imprimir corretamente caracteres acentuados

    printf("\nBem-vindo!\n\n");
    printf("Carregando o Programa... Aguarde um instante");

    sleep(1); // Espera por 1 segundo

    // Variáveis para o menu e armazenamento de dados
    int opcao, totalAlunos = 0;
    float notas[MAX_ALUNOS][4]; // Matriz para armazenar as notas dos alunos
    char nomes[MAX_ALUNOS][50]; // Matriz para armazenar os nomes dos alunos

    do {
        menuPrincipal();
        printf("Digite sua opção: ");
        scanf("%d", &opcao);

        switch (opcao) {
        case 1:
            digitarNotasAluno(notas, nomes, &totalAlunos);
            break;
        case 2:
            mostrarNotasAlunos(notas, nomes, totalAlunos);
            break;
        case 3:
            editarNotaAluno(notas, nomes, totalAlunos);
            break;
        case 4:
            printf("\nSaindo do programa... Aguarde um pouco\n");
            sleep(1);
            break;
        default:
            printf("\nOpção inválida. Tente novamente.\n");
        }
    } while (opcao != 4);

    return 0;
}

// Função para exibir o menu principal
void menuPrincipal() {
    system("clear"); // Limpa a tela
    printf("\nMENU\n");
    printf("1. Digitar notas dos alunos\n");
    printf("2. Mostrar notas dos alunos\n");
    printf("3. Editar nota de aluno\n");
    printf("4. Sair\n");
}

// Função para digitar as notas dos alunos
void digitarNotasAluno(float notas[][4], char nomes[][50], int *totalAlunos) {
    int i;

    system("clear"); // Limpa a tela

    if (*totalAlunos >= MAX_ALUNOS) {
        printf("\nNão é possível cadastrar mais alunos. Limite máximo de %d alunos atingido.\n", MAX_ALUNOS);
        return;
    }

    printf("\nDigite os dados do aluno %d:\n", *totalAlunos + 1);

    printf("Nome: ");
    scanf("%s", nomes[*totalAlunos]); // Melhorar isso usando fgets

    for (i = 0; i < 4; i++) {
        printf("Digite a nota %d: ", i + 1);
        scanf("%f", &notas[*totalAlunos][i]);
    }

    (*totalAlunos)++; // Incrementa o contador de alunos cadastrados
}

// Função para mostrar as notas dos alunos
void mostrarNotasAlunos(float notas[][4], char nomes[][50], int totalAlunos) {
    int i, j;

    if (totalAlunos == 0) {
        printf("\nNenhum aluno cadastrado ainda.\n");
        return;
    }

    system("clear"); // Limpa a tela
    printf("\nNotas dos Alunos:\n");

    for (i = 0; i < totalAlunos; i++) {
        printf("\nAluno: %s\n", nomes[i]);

        for (j = 0; j < 4; j++) {
            printf("Nota %d: %.2f\n", j + 1, notas[i][j]);
        }
    }
}

// Função para editar nota de um aluno
void editarNotaAluno(float notas[][4], char nomes[][50], int totalAlunos) {
    int aluno, nota, novaNota;

    if (totalAlunos == 0) {
        printf("\nNenhum aluno cadastrado ainda.\n");
        return;
    }

    system("clear"); // Limpa a tela
    printf("\nEditar nota de aluno\n");

    printf("Digite o número do aluno: ");
    scanf("%d", &aluno);

    if (aluno <= 0 || aluno > totalAlunos) {
        printf("\nNúmero de aluno inválido.\n");
        return;
    }

    printf("Digite o número da nota a ser editada (1 a 4): ");
    scanf("%d", &nota);

    if (nota < 1 || nota > 4) {
        printf("\nNúmero de nota inválido.\n");
        return;
    }

    printf("Digite a nova nota: ");
    scanf("%d", &novaNota);

    notas[aluno - 1][nota - 1] = novaNota;
}
