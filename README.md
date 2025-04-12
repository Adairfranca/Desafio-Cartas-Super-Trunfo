# Desafio-Cartas-Super-Trunfo
Curso TI


#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

// Definindo estrutura da carta
typedef struct {
    char nome[30];
    int populacao;    // em milhares
    int area;         // em km²
    int pib;          // em bilhões
} Cidade;

// Lista de cartas (cidades)
Cidade baralho[] = {
    {"Tóquio",        37400, 2190, 1600},
    {"Nova York",     19200, 783, 1500},
    {"São Paulo",     22300, 1521, 700},
    {"Londres",       9300, 1572, 850},
    {"Paris",         11000, 105, 900},
    {"Xangai",        24800, 6340, 1100},
    {"Mumbai",        20400, 603, 400},
    {"Toronto",       3000, 630, 400},
};

// Função para escolher carta aleatória
Cidade escolherCarta() {
    int indice = rand() % (sizeof(baralho)/sizeof(Cidade));
    return baralho[indice];
}

// Função para escolher atributo aleatório
int escolherAtributo() {
    return rand() % 3; // 0 = população, 1 = área, 2 = PIB
}

// Mostra a carta
void mostrarCarta(Cidade c) {
    printf("Cidade: %s\n", c.nome);
    printf("População: %d mil\n", c.populacao);
    printf("Área: %d km²\n", c.area);
    printf("PIB: %d bilhões\n", c.pib);
}

int main() {
    srand(time(NULL));

    Cidade jogador = escolherCarta();
    Cidade computador = escolherCarta();

    // Impede que seja a mesma cidade
    while (strcmp(jogador.nome, computador.nome) == 0) {
        computador = escolherCarta();
    }

    printf("\nSua carta:\n");
    mostrarCarta(jogador);

    int atributo = escolherAtributo();

    char* nomeAtributo;
    int valorJogador, valorComputador;

    switch (atributo) {
        case 0:
            nomeAtributo = "População";
            valorJogador = jogador.populacao;
            valorComputador = computador.populacao;
            break;
        case 1:
            nomeAtributo = "Área";
            valorJogador = jogador.area;
            valorComputador = computador.area;
            break;
        case 2:
            nomeAtributo = "PIB";
            valorJogador = jogador.pib;
            valorComputador = computador.pib;
            break;
    }

    printf("\nAtributo escolhido: %s\n", nomeAtributo);
    printf("Sua cidade: %s - %d\n", jogador.nome, valorJogador);
    printf("Cidade do computador: %s - %d\n", computador.nome, valorComputador);

    if (valorJogador > valorComputador) {
        printf("\nVocê venceu!\n");
    } else if (valorJogador < valorComputador) {
        printf("\nVocê perdeu!\n");
    } else {
        printf("\nEmpate!\n");
    }

    return 0;
}
