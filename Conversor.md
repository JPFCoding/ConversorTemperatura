#include <stdio.h>
#include <math.h>
#include <locale.h>
#include <string.h>

int main()
{
    setlocale(LC_ALL, "portuguese");
    float C=0,F=0,z=0,a,x;
    char linha[100],temperatura[100];
    FILE*f;
    do{
        printf("Olá, tudo bem?\nBem vinda(o) ao conversor de temperaturas do João Paulo!\n\tPara converter de célcius para farenheit, pressione 1.\n\tPara converter de farenheit para célcius pressione 2.\n\tPara acessar o histórico de conversões, pressione 3.\n\t");
        scanf("%f",&x);
        if(x==1){
            strcpy(temperatura,"Farenheit");
            printf("\nVocê quer converter de célcius para farenheit.\nDigite a temperatura, por favor:\n\t");
            scanf("%f",&C);
            z=(9.0/5.0)*C+32;
            printf("\nEsse é o resultado: %5f",z);
        }
        if(x==2){
            strcpy(temperatura,"Célcius");
            printf("\nVocê escolheu converter de farenheit para célcius.\nPor favor, digite a temperatura:\n\t");
            scanf("%f",&F);
            z=(F-32)/1.8;
            printf("\nEsse é o resultado: %5f",z);
        }
        f=fopen("Historico de temperaturas.txt","a");
        fprintf(f,"Temperatura escolhida é %s,%f\t",temperatura,z);
        fprintf(f,"\n\n");
        fclose(f);
        if(x==3){
            f=fopen("Historico de temperaturas.txt","r");
            if(f==NULL){
                printf("\n\nARQUIVO VAZIO!");
            }
            while(fgets(linha,sizeof(linha),f)!=NULL){
                printf("%s",linha);
            }
            fclose(f);
        }
        printf("\nPara sair, pressione 0.\nDeseja repetir o processo, precione qualquer numero que não seja 0.\n");
        scanf("%f",&a);
    }while(a!=0);
    return(0);
}