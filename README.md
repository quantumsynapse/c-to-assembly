# C to Assembly 8086 Compiler

that's all folks ;) 

Este é apenas um exemplo didático de um compilador simplificado, usei como referencia a teoria do Alfred Aho, o codigo é meu. 
Eu criei uma expressão RNP (Notacao Polonesa Reversa - a mesma usada em HP 48 Gx) no main.c para testar o algoritmo

Vamos trocar ideias. 

Julio ! 

Depois de clonar o repositorio execute 

(base) neuron@brain:~/c-to-assembly$ gcc -Iinclude -o build/compiler src/*.c
(base) neuron@brain:~/c-to-assembly$ ./build/compiler

Para rodar em sua máquina ! 

Saída 

(base) neuron@brain:~/c-to-assembly$ gcc -Iinclude -o build/compiler src/*.c
(base) neuron@brain:~/c-to-assembly$ ./build/compiler
mov ax, 3   move para o registrador da CPU Ax, o valor 3
push ax     joga na pilha o conteudo do registrador
mov ax, 4   move para o ax o 4 
pop bx      desempilha e joga o conteudo da pilha no bx
add ax, bx  soma (+) 
push ax     guarda na pilha
mov ax, 2   move para ax 2 
pop bx      desempenha (resultado da soma anterior) 
mul bx       multiplia o que esta no ax (2) pelo resultado desimpilhado (soma anterior)
push ax     joga na pilha o que esta em ax 
mov ax, 7   move para ax o valor 7
pop bx      desepilha (soma multiplicada por dois) 
div bx     divide por por 7 


Em resumo, executa este expressão (3 4 + 2 * 7 / ) 

#include "lexer.h"
#include "parser.h"
#include "code_generator.h"
#include <stdio.h>
#include <stdlib.h>

int main() {
    const char *input = "3 4 + 2 * 7 /";
    int token_count;
    Token **tokens = tokenize(input, &token_count);
    ASTNode *ast = parse(tokens, token_count);
    generate_code(ast);

    for (int i = 0; i < token_count; i++) {
        destroy_token(tokens[i]);
    }
    free(tokens);
    destroy_ast_node(ast);

    return 0;
}
~                     




