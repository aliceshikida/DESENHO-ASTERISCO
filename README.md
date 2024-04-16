#include <stdio.h>

int main() {
    int sudoku[9][9], 
  escolha,
  linha = 0, 
  coluna = 0, algarismo, 
  contagem = 0, repeticao = 0,
  quadrante;

  
    for (int linha = 0; linha < 9; linha++) {
        for (int coluna = 0; coluna < 9; coluna++) {
            scanf("%d%*c", &sudoku[linha][coluna]);
        }
    }

    do {
        scanf("%d%*c", &escolha);

        switch (escolha) {
            case 0:
     
                break;
            case 2:

            linha = 0;
            repeticao = 0;
            coluna = 0;
            scanf("%d%*c", &linha);
            for (int col = 0; col < 9; col++) {
                contagem = 0;
                for (int c = 0; c < 9; c++) {
                    if (sudoku[linha][coluna] == sudoku[linha][c]) {
                        contagem++;
                    }
                    if (contagem > 1) {
                        repeticao++;
                    }
                }
                coluna++;
            }

            if (repeticao > 1) {
                printf("S\n");
            } else {
                printf("N\n");
            }

            break;
            case 1:
                scanf("%d %d %d", &linha, &coluna, &algarismo);
                sudoku[linha][coluna] = algarismo;
                break;
         

            case 3:
         
                linha = 0;
                repeticao = 0;
                coluna = 0;
                scanf("%d%*c", &coluna);
                for (int l = 0; l < 9; l++) {
                    contagem = 0;
                    for (int c = 0; c < 9; c++) {
                        if (sudoku[linha][coluna] == sudoku[c][coluna]) {
                            contagem++;
                        }
                        if (contagem > 1) {
                            repeticao++;
                        }
                    }
                    linha++;
                }

                if (repeticao > 0) {
                    printf("S\n");
                } else {
                    printf("N\n");
                }
                break;

            case 4:
            
                scanf("%d%*c", &quadrante);

                if (quadrante < 3) {
                    linha = 0;
                } else if (quadrante >= 3 && quadrante <= 5) {
                    linha = 3;
                } else if (quadrante >= 6 && quadrante <= 8) {
                    linha = 6;
                }

                if (quadrante == 0 || quadrante == 3 || quadrante == 6) {
                    coluna = 0;
                } else if (quadrante == 1 || quadrante == 4 || quadrante == 7) {
                    coluna = 3;
                } else if (quadrante == 2 || quadrante == 5 || quadrante == 8) {
                    coluna = 6;
                }

                repeticao = 0;
                for (int l = linha; l < linha + 3; l++) {
                    for (int c = coluna; c < coluna + 3; c++) {
                        contagem = 0;
                        for (int li = linha; li < linha + 3; li++) {
                            for (int co = coluna; co < coluna + 3; co++) {
                                if (sudoku[l][c] == sudoku[li][co] && (l != li || c != co)) {
                                    contagem++;
                                }
                            }
                        }
                        if (contagem > 0) {
                            repeticao++;
                        }
                    }
                }
                if (repeticao > 0) {
                    printf("S\n");
                } else {
                    printf("N\n");
                }

                break;

            case 5:
            
                repeticao = 0;
                for (int l = 0; l < 9; l++) {
                    for (int c = 0; c < 9; c++) {
                        for (int co = c + 1; co < 9; co++) {
                            if (sudoku[l][c] == sudoku[l][co]) {
                                repeticao = 1;
                            }
                        }
                    }
                }

                int repeticao1 = 0;
                for (int l = 0; l < 9; l++) {
                    for (int c = 0; c < 9; c++) {
                        for (int lin = l + 1; lin < 9; lin++) {
                            if (sudoku[l][c] == sudoku[lin][c]) {
                                repeticao1 = 1;
                            }
                        }
                    }
                }

                int repeticao2 = 0;
                linha = 0;
                coluna = 0;
                do {
                    for (int l = linha; l < linha + 3; l++) {
                        for (int c = 0; c < 9; c++) {
                            for (int lin = linha; lin < linha + 3; lin++) {
                                for (int col = 0; col < 9; col++) {
                                    if (l != lin || c != col) { 
                                        if (sudoku[l][c] != 0 && sudoku[l][c] == sudoku[lin][col]) {
                                            repeticao2 = 1;
                                        }
                                    }
                                }
                            }
                        }
                    }
                    linha = linha + 3;
                } while (linha < 9);

                if (repeticao > 0 && repeticao1 > 0 && repeticao2 > 0) {
                    printf("S\n");
                } else {
                    printf("N\n");
                }
                break;

            default:
          
                for (int l = 0; l < 9; l++) {
                    if (l == 3 || l == 6) {
                        printf("\n");
                    }
                    for (int c = 0; c < 9; c++) {
                        if (c == 3 || c == 6) {
                            printf(" ");
                        }
                        printf("%d ", sudoku[l][c]);
                    }
                    printf("\n");
                }
                break;
        }
    } while (escolha != 0);

    return 0;
}
