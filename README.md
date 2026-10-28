# Atividade-Algoritmo-e-Pensamento-Computacional
Controle de estoque

#include <stdio.h>

char nomes[10][50];
float precos[10];
int estoque[10];
int total = 0;

void cadastrar() {
    if (total == 10) {
        printf("Limite de produtos atingido.\n");
        return;
    }

    printf("Nome: ");
    scanf(" %49[^\n]", nomes[total]);

    printf("Preco: ");
    scanf("%f", &precos[total]);

    printf("Quantidade: ");
    scanf("%d", &estoque[total]);

    if (precos[total] < 0 || estoque[total] < 0) {
        printf("Preco ou quantidade invalida.\n");
        return;
    }

    total++;
    printf("Produto cadastrado com codigo %d.\n", total);
}

void consultar() {
    int i;

    if (total == 0)
        printf("Nenhum produto cadastrado.\n");

    for (i = 0; i < total; i++) {
        printf("%d - %s | R$ %.2f | %d unidades\n",
               i + 1, nomes[i], precos[i], estoque[i]);
    }
}

float faturamento(float preco, int quantidade) {
    return preco * quantidade;
}

void vender(int codigo, int quantidade) {
    if (codigo < 1 || codigo > total || quantidade <= 0) {
        printf("Codigo ou quantidade invalida.\n");
        return;
    }

    codigo--;

    if (quantidade > estoque[codigo]) {
        printf("Estoque insuficiente.\n");
        return;
    }

    estoque[codigo] -= quantidade;
    printf("Valor da venda: R$ %.2f\n",
           faturamento(precos[codigo], quantidade));
}

void reposicao() {
    int i, encontrou = 0;

    for (i = 0; i < total; i++) {
        if (estoque[i] < 5) {
            printf("%s: %d unidades\n", nomes[i], estoque[i]);
            encontrou = 1;
        }
    }

    if (encontrou == 0)
        printf("Nenhum produto precisa de reposicao.\n");
}

void entrada(int codigo, int quantidade) {
    if (codigo < 1 || codigo > total || quantidade <= 0) {
        printf("Codigo ou quantidade invalida.\n");
        return;
    }

    estoque[codigo - 1] += quantidade;
    printf("Entrada registrada.\n");
}

float valorEstoque() {
    int i;
    float valor = 0;

    for (i = 0; i < total; i++)
        valor += precos[i] * estoque[i];

    return valor;
}

int main() {
    int opcao, codigo, quantidade;

    do {
        printf("\n1 - Cadastrar produto\n");
        printf("2 - Consultar estoque\n");
        printf("3 - Registrar venda\n");
        printf("4 - Consultar reposicao\n");
        printf("5 - Entrada de mercadorias\n");
        printf("6 - Encerrar\n");
        printf("Opcao: ");
        scanf("%d", &opcao);

     
