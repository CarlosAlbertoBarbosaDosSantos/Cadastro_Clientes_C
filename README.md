# Cadastro_Clientes_C
Cadastro de clientes TXT em C

#include <stdio.h>
#include <stdlib.h>
#include <locale.h>
#include <conio.h>
#define ARQUIVO_ESCOLHIDO 1
#define LINHA_DO_ARQUIVO 2

char nome[100], endereco [150], email[50], telefone[20], nascimento[15], dados[2000], busca[3], lista[50000];
int id, tamanho, x;
int local, selecao, contador=1;
int identificador, menu;
char status[4], nome2[100], endereco2[150], email2[50], nascimento2[15], telefone2[20], concatenar1[2000];




char* clearN(char* line){

    for(int i=0; i<150; i++){
        if( line[i]== '\n'){
            line[i]=0;
            break;
        }
    }
    return line;
}

int buscar_id() {

	FILE *pont_arq;
    pont_arq = fopen("cadastro_cliente.txt", "r");//	Abre o arquivo
    contador=1;
    system("cls");
        printf("\n-------Cadastro de contatos-------\n\n");
        printf(" Digite o identificador do contato: ");
        scanf("%d", &x);

	if(pont_arq == NULL) {
		printf("Erro na criacao do arquivo");
		exit(1);
	}
	 while( fgets(dados, 2000, pont_arq)!= NULL){

            if(contador == x){

                printf("\n %s \n", dados);
            }
            contador = contador + 1;
        }
        printf("---------Alterar arquivo---------\n\n");
            printf(" 1 para modificar arquivo. \n");
            printf(" 2 para deletar arquivo. \n");
            printf(" 3 para sair. \n");

            printf("\n Digite valor: ");
            scanf("%d", &selecao);

             switch(selecao){

         case 1:
             modificar();
             printf("\n Arquivo alterado!\n");
             system ("pause");
            break;

         case 2:

            excluir();
            printf(" Arquivo excluido!\n");
            system ("pause");
            break;

         case 3:
             printf(" Retornando ao menu.");
            break;

             }
             x = 0;

//	Fecha o arquivo
	fclose(pont_arq);
}

int modificar(){

    fflush(stdin);
    setlocale(LC_ALL, "portuguese-brazilian");
    FILE *arq;
    int i = 0;
    int numPalavras = 0;
    char* palavras[1000];
    char line[1000], letra;


    int w = 1;

    FILE *arquivo;
    arquivo = fopen("cadastro_cliente.txt", "r");

    if (arquivo == NULL)
    {
        printf(" Erro na abertura do arquivo.");
        return 1;
    }

    while(fgets(line, sizeof line, arquivo) != NULL){

        if( i+1!= x){
            palavras[i] = strdup(line);
        }
        else{

        printf("\n Digite seu Nome: ");
        fgets(clearN(nome2),100,stdin);

        printf("\n Digite seu Endereço: ");
        fgets(clearN(endereco2),150,stdin);

        printf("\n Digite seu Email: ");
        fgets(clearN(email2),50,stdin);

        printf("\n Digite sua data de nascimento: ");
        fgets(clearN(nascimento2),15,stdin);

        printf("\n Digite seu telefone: ");
        fgets(clearN(telefone2),20,stdin);

        //fgets(clearN(id),100,stdin);


        sprintf( concatenar1,"%d, %s, %s, %s, %s, %s, %s \n",x ,clearN(nome2),clearN(nome2), clearN(endereco2), clearN(email2), clearN(nascimento2), clearN(telefone2) );

        palavras[i] = concatenar1;

        printf("%s", palavras[i]);

    }
        i++;
        numPalavras++;//Conta a quantidade de palavras
    }
   int j;
    FILE *pont_arq;//ponteiro para o arquivo FILE
    pont_arq = fopen("cadastro_cliente.txt", "w");
    fputs("", pont_arq);
    fclose(arquivo);
    pont_arq = fopen("cadastro_cliente.txt", "a");//abrindo arquivo com tipo de abertura a


    for (j = 0; j < numPalavras; j++)
    {
        fputs(palavras[j], pont_arq);
    }
    fclose(arquivo);
}

int sequencial(){

        FILE *pont_arq;
        pont_arq = fopen("cadastro_cliente.txt", "r");
        identificador= 1;

        if(pont_arq == NULL)
    {
        printf(" Erro na abertura do arquivo.");
        return 1;
    }
    else
    {
        while( fgets(dados, 2000, pont_arq)!= NULL) {
            identificador = identificador + 1;

        }

    }
    return identificador;
}

int excluir(){

    setlocale(LC_ALL, "portuguese-brazilian");
    FILE *arq;


    int i = 0;
    int numPalavras = 0;
    char* palavras[1000];
    char line[1000];


    int w = 1;

    FILE *arquivo;
    arquivo = fopen("cadastro_cliente.txt", "r");

    if (arquivo == NULL)
    {
        return EXIT_FAILURE;
    }


    while(fgets(line, sizeof line, arquivo) != NULL)
    {


        if( i+1!= x)
        {

            palavras[i] = strdup(line);

        }
        else
        {
            //Adiciona cada palavra no vetor
            palavras[i] = strcat(strdup("Null,"),strdup(line));
        };
        i++;
        //Conta a quantidade de palavras
        numPalavras++;
    };

    int j;
    FILE *pont_arq;//ponteiro para o arquivo FILE
    pont_arq = fopen("cadastro_cliente.txt", "w");
    fputs("", pont_arq);
    fclose(arquivo);
    pont_arq = fopen("cadastro_cliente.txt", "a");//abrindo arquivo com tipo de abertura a


    for (j = 0; j < numPalavras; j++)
    {
        fputs(palavras[j], pont_arq);
    }
    fclose(arquivo);
}

int ler_arquivo(){
    setlocale(LC_ALL, "Portuguese");

    FILE *pont_arq;//ponteiro para o arquivo FILE
    pont_arq = fopen("cadastro_cliente.txt", "r");//abrindo arquivo com tipo de abertura r para ler o arquivo

    system("cls");
    printf("\n-----Cadastro de contato-----\n\n");

    if(pont_arq == NULL){
        printf(" Erro na abertura do arquivo.");
        return 1;
    }else{


        while( fgets(dados, 2000, pont_arq)!= NULL){

            printf(" %s \n", dados);
        }

        fclose(pont_arq);
        system("pause");

    }

    return 0;

}

int inserir(){

    fflush(stdin);
    setlocale(LC_ALL, "Portuguese");

    FILE *pont_arq;//ponteiro para o arquivo FILE
    pont_arq = fopen("cadastro_cliente.txt", "a");//abrindo arquivo com tipo de abertura a

    if(pont_arq == NULL)
    {
        printf(" Erro na abertura do arquivo.");
        return 1;
    }
    else
    {
        system("cls");
        printf("\n-----Cadastro de contato-----\n\n");

        id = sequencial();
        fprintf (pont_arq, "%d",id);

        fputs(",", pont_arq);

        printf("\n Digite seu Nome: ");
        fgets(nome,100,stdin);
        fputs(clearN(nome), pont_arq);
        fputs(",", pont_arq);

        printf("\n Digite seu Endereço: ");
        fgets(endereco,150,stdin);
        fputs(clearN(endereco), pont_arq);
        fputs(",", pont_arq);

        printf("\n Digite seu Email: ");
        fgets(email,50,stdin);
        fputs(clearN(email), pont_arq);
        fputs(",", pont_arq);

        printf("\n Digite sua data de nascimento: ");
        fgets(nascimento,15,stdin);
        fputs(clearN(nascimento), pont_arq);
        fputs(",", pont_arq);

        printf("\n Digite seu telefone: ");
        fgets(clearN(telefone),20,stdin);
        fputs(telefone, pont_arq);


        fclose(pont_arq);

        printf("Dados gravados.");
        getch();
    }


}

int main(){
    setlocale(LC_ALL, "Portuguese");


    do{
        system("cls");
        
        printf("\n------Lista de Contatos------\n\n");
        printf("-------------Menu------------\n");
        printf("1 - Inserir novo contato \n");
        printf("2 - Visualizar cadastro \n");
        printf("3 - Busca  de Registro \n");
        printf("4 - Sair. \n\n");

        printf("-----------------------------\n");

        printf("Valor digitado: ");
        scanf("%d",&menu);

        switch(menu){

            case 1:
                    inserir();
            break;

            case 2:
                    ler_arquivo();
            break;

            case 3:
                    buscar_id();
            break;

        };

    }while(menu!=4);

    return 0;
}
