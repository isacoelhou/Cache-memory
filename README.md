# Cache-memory

Implementar o algoritmo clássico para multiplicação entre duas matrizes M1l1xc1 e M2l2xc2
◦ Condição de multiplicação: c1 == l2
◦ Mrl1xc2 = M1l1xc1 * M2l2xc2
◦ Requisitos:
▪ Alocação dinâmica das matrizes utilizadas
▪ Tipo de dado Double
▪ Preenchimento de M1 e M2 com números aleatórios
◦ Sugestão (em C) de assinatura de função/método:
void MulM1M2(double **M1, double **M2, double **MR, int l1, int c2)
• Validar a implementação do algoritmo clássico
◦ Use matrizes pequenas e valide manualmente
◦ Use algum programa externo de sua preferência
▪ Para tal, será necessário exportar e importar as matrizes M1, M2 e Mr
• recomendação: arquivo em formato .csv
◦ Após validação, remover todos os “prints” em tela desnecessários, E/S consome muito
tempo e não é objetivo das análises de desempenho
• Implementar uma função de multiplicação de matrizes melhorada
◦ Mrl1xc2 = M1l1xc1 * M2T
c2xl2
void MulM1M2T(double **M1, double **M2T, double **MR, int l1, int c2)
◦ É necessário implementar função/método de transposição, sugestão:
void transpostaM2(double **M2, double **M2T, int l2, int c2)
• Validar implementação melhorada
◦ Utilize as mesmas técnicas de validação do algoritmo clássico
• Funcionamento do programa principal:
◦ Executa apenas uma multiplicação
◦ Tamanho das matrizes é definido via linha de comando de execução
OAC 304 – Memória CACHE – Prática 03 página 1 / 3
◦ Método de multiplicação também é definido via linha de comando de execução
./mulmatriz.x l1 c1 l2 c2 o|t
Onde:
 li: Número de linhas de Mi
 ci: Número de colunas de Mi
 o|t: Método clássico ou M2 transposta
• Após implementações e validações, é hora dos benchmarks de tempo.
◦ Métricas de tempo requeridas:
▪ funções MulM1M2, MulMM2T e traspostaM2
▪ Alocação não é requerido, mas pode ser um extra para enriquecer o relatório
◦ Em C, existe a biblioteca time.h
#include <time.h>
...
float tempo = 0.0;
clock_t inicio, fim;
...
inicio = clock();
// aqui está o código que deseja mensurar tempo
fim = clock();
// cálculo para apresentação em segundos
tempo = (float) (((fim - inicio ) + 0.0) / CLOCKS_PER_SEC);
• Mensurar:
◦ Execuções para matrizes quadradas de tamanhos l1 = l2 = i
▪ 200 <= i <= 2.000; com passos i += 200 (10 variações)
▪ Para cada variação, reexecutar 10 vezes, tomar tempo e calcular a média
• NÃO utilize iterações internas ao programa, isso vicia resultados!
• Toda reexecução deve ser uma NOVA execução!
◦ Linux: utilize algum script que execute o programa principal
• Comparar:
◦ Média de cada variação de execução entre
▪ MulM1M2 e MulM1M2T
▪ MulM1M2 e (MulM1M2T+transpostaM2)
OAC 304 – Memória CACHE – Prática 03 página 2 / 3
• Relatório
◦ Calcular o speedup entre as soluções MulM1M2 e (MulM1M2T+transpostaM2)
▪ speedup indica um índice de melhora com relação ao tempo original
• exemplo: código X melhorado levou 42% do tempo do código sem melhoria.
◦ Apresentar os valores de CACHE HIT e CACHE MISS do último nível de cache da sua
máquina utilizando a ferramenta valgrind apresentado durante a aula prática.
▪ Linha de comando:
valgrind --tool=cachegrind ./<nome.x> <args>
ATENÇÃO: execução será lenta, muito lenta! Evite usar com matrizes grandes.
Recomendação: matrizes quadradas de < 1500 linhas/colunas
