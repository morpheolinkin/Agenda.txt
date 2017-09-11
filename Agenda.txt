# Agenda.txt
Testando algoritmo para criar uma agenda funcional

#include<stdio.h>
#include<stdlib.h>
#include<locale.h>

FILE* AbreArquivo(char modo, char caminho[30]){
    FILE *arquivoAgenda;

    switch (modo){
    case 'g': //g = Gravação
        arquivoAgenda = fopen(caminho, "wt"); break;
    case 'l': // r = Leitura
        arquivoAgenda = fopen(caminho, "rt"); break;
    case 'a':
        arquivoAgenda = fopen(caminho, "a"); break;

    if (arquivoAgenda == NULL){
        printf("Arquivo não encontrado!");
        exit(0);
    }
    return arquivoAgenda;
}
}

void FechaArquivo (FILE *arquivoAgenda){
    fclose(arquivoAgenda);
}



void Cadastra(char nome[30], int telefone){
    FILE *arquivoAgenda;
    arquivoAgenda = AbreArquivo('a', "agenda.txt");
    fprintf(arquivoAgenda, "%s %d\n", nome, telefone);
    FechaArquivo(arquivoAgenda);
}

void Listar (){
    FILE *arquivoAgenda;
    char nome [30];
    int telefone;

    arquivoAgenda = AbreArquivo('l', "agenda.txt");
    while(!feof(arquivoAgenda)){ //feof = Siginifica fim do arquivo, no caso, enquanto não for o fim do arquivo ele faz.
        fscanf(arquivoAgenda, "%s %d", &nome, &telefone);
        printf("Nome > %s - Telefone > %d\n", nome, telefone);

    }
    FechaArquivo(arquivoAgenda);
}

int menu(){
    int opcao; char nome[30]; int telefone;
    do {
    system("cls");
        printf("\n\n\t\tBem Vindo ao programa AGENDA\n");
        printf("\nMENU");
        printf("\n 01 - Cadastrar Nome e telefone");
        printf("\n 02 - Listar todos os Nomes e telefones");
        printf("\n 03 - Sair");

        printf("\nDigite uma opcao: ");
        scanf("%d", &opcao);
        system("cls");

        switch(opcao){
            case 1:
                printf("\nDigite o nome: ");
                setbuf(stdin,NULL);
                gets(nome);
                printf("\nDigite o telefone: ");
                scanf("%d", &telefone);
                Cadastra(nome, telefone);
                system("pause");
                break;
            case 2:
                Listar();
                system("pause");
                break;
            case 3:
                printf("\n\nFinalizando...\n\n");
                system("pause");
                exit(0);
                break;

            default:
                printf("\n\nOpcao invalida! Tente Novamente!\n\n");
                system("pause");

        }
    }while(opcao!=3);

return opcao;
}


int main (){
setlocale(LC_ALL,"");



    menu();


return 0;
}
