
#include <stdio.h>
#include <stdlib.h>

void aloca(float **ptr, int tam);
void recebe(float *x, float *fx, int tam);
void lagrange(float *x, float *fx, int tam);

int main()
{
	int grau, pontos, i, j;
	float *valorX = NULL;
	float *valorFX = NULL;
	char op;
	
	printf("\nDigite o grau da funcao que deseja obter: ");
	scanf("%d", &grau);
	
	pontos = grau + 1;
	
	aloca(&valorX, pontos);
	aloca(&valorFX, pontos);
	
	recebe(valorX, valorFX, pontos);
	
	lagrange(valorX, valorFX, pontos);
	
	system("pause");
	return 0;
}

void aloca(float **ptr, int tam)
{
	if((*ptr = (float*) malloc(tam * sizeof(float))) == NULL)
	{
		exit(1);
	}
}

void recebe(float *x, float *fx, int tam)
{
	int i = 0;
	for(i = 0; i < tam; i++)
	{
		printf("\nDigite o valor do %do valor de X: ", i + 1);
		scanf("%f", x + i);
	}
	for(i = 0; i < tam; i++)
	{
		printf("\nDigite o valor do %do valor de F(x): ", i + 1);
		scanf("%f", fx + i);
	}
}

void lagrange(float *x, float *fx, int tam)
{
	int i, j;
	float Px, Li, calcularX;
	char op;
	
	do
	{
		printf("\nDigite o valor que deseja calcular: ");
		scanf("%f", &calcularX);
		
		Px = 0;
		
		for(i = 0; i < tam; i++)
		{
			Li = 1;
			for(j = 0; j < tam; j++)
			{
				if(i != j)
				{
					Li = Li * ((calcularX - *(x + j)) / (*(x + i) - *(x + j)));
				}	
			}
			printf("\nO valor de Li(x%d) eh %.2f",i, Li);
			Px = Px + (Li * *(fx + i));
		}
		printf("\nO valor de F(x) eh: %.2f", Px);
		
		printf("\n\nDeseja calcular outro valor? (S/N): ");
		scanf(" %c", &op);
		fflush(stdin);
	}while(op != 'n' && op != 'N');
}
