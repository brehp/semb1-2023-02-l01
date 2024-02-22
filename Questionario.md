# Questionário Sistemas Embarcados I

## 1. Explique brevemente o que é compilação cruzada (***cross-compiling***) e para que ela serve.
Consiste em criar um codigo direcionado para uma plataforma, contudo, o compilador dele será executado em outra,
a mudança descrita pode ser entre sistemas operacionais ou até mesmo outras arquiteturas. Em razão da compilação
cruzada o desenvolvedor consegue criar programas para plataformas as quais não esta trabalhando, principalmente 
para dispositivos embarcados, pois a compilação não precisa ser executada no processador final. Ele é muito
utilizado para criar sofwares destinados a uma ampla gama de plataformas, mas usando um so compilador.



## 2. O que é um código de inicialização ou ***startup*** e qual sua finalidade?
Statup é um código que vem antes da chamada da função main, tendo como objetivo preparar o ambiente de trabalho para execução do programa
principal, bem como, é constituído de rotinas de baixo nível. Quando o executável é carregado na memória o controle vai para uma rotina
intermediaria que é descrita pelo código de inicialização que: inicializa os stacks, prepara os streams, adiciona ao stack os argumentos argc
e argv, copia o conteúdo da seção .data e .fast da memória flash para RAM, inicializa o .bss em zero, inicializa o heap, inicializa alguma
função de preparação do sistema operacional, faz a alocação da tabela de vetores de interrupção na memória e somente depois chama o main(). 
Em suma, ele dita as condições necessárias para que o sistema execute o software de forma adequada.


## 3. Sobre o utilitário **make** e o arquivo **Makefile responda**:

#### (a) Explique com suas palavras o que é e para que serve o **Makefile**.
Ele é um arquivo utilizado para automatizar o processo de compilação e vinculação dos programas escrito pelo programador, dentro dele possui algumas regras
que ditam como o programa deve ser compilado, bem como, as dependências dos arquivos de origem e a maneira de vincula-los ao executável final. Além disso,
só compila arquivos que foram modificados desde a ultima compilação.Para executa-lo basta digitar o comando make no terminal, que ele compila automaticamente
os programas utilizando o arquivo makefile.


#### (b) Descreva brevemente o processo realizado pelo utilitário **make** para compilar um programa.
O utilitario make é um comando feito no terminal, o qual automatiza o processo de compilação dos programas que teriam que ter grande comandos para serem compilados. 
Ao digitar o make ele realiza a leitura das regras e dependencias descritas no arquivo makefile, vê quais arquivos precisam ser compilados novamente ou ser vinculados
ao executavel final, gera arquivos objetos correspondentes, bem como, gera o programa final concluindo o processo de compilação. 


#### (c) Qual é a sintaxe utilizada para criar um novo **target**?
targets: prerequisites
	recipe

 Targets é o arquivo objeto, o arquivo que será gerado no final, como exemplo da aula o statup.o e o main.o
 Prerequisites: são os arquivos originais que serão compilados, por exemplo main.c e startup.c
 recipe: instruções de compilação

#### (d) Como são definidas as dependências de um **target**, para que elas são utilizadas?

#### (e) O que são as regras do **Makefile**, qual a diferença entre regras implícitas e explícitas?

## 4. Sobre a arquitetura **ARM Cortex-M** responda:

### (a) Explique o conjunto de instruções ***Thumb*** e suas principais vantagens na arquitetura ARM. Como o conjunto de instruções ***Thumb*** opera em conjunto com o conjunto de instruções ARM?

### (b) Explique as diferenças entre as arquiteturas ***ARM Load/Store*** e ***Register/Register***.

### (c) Os processadores **ARM Cortex-M** oferecem diversos recursos que podem ser explorados por sistemas baseados em **RTOS** (***Real Time Operating Systems***). Por exemplo, a separação da execução do código em níveis de acesso e diferentes modos de operação. Explique detalhadamente como funciona os níveis de acesso de execução de código e os modos de operação nos processadores **ARM Cortex-M**.

### (d) Explique como os processadores ARM tratam as exceções e as interrupções. Quais são os diferentes tipos de exceção e como elas são priorizadas? Descreva a estratégia de **group priority** e **sub-priority** presente nesse processo.

### (e) Qual a diferença entre os registradores **CPSR** (***Current Program Status Register***) e **SPSR** (***Saved Program Status Register***)?

### (f) Qual a finalidade do **LR** (***Link Register***)?

### (g) Qual o propósito do Program Status Register (PSR) nos processadores ARM?

### (h) O que é a tabela de vetores de interrupção?

### (i) Qual a finalidade do NVIC (**Nested Vectored Interrupt Controller**) nos microcontroladores ARM e como ele pode ser utilizado em aplicações de tempo real?

### (j) Em modo de execução normal, o Cortex-M pode fazer uma chamada de função usando a instrução **BL**, que muda o **PC** para o endereço de destino e salva o ponto de execução atual no registador **LR**. Ao final da função, é possível recuperar esse contexto usando uma instrução **BX LR**, por exemplo, que atualiza o **PC** para o ponto anterior. No entanto, quando acontece uma interrupção, o **LR** é preenchido com um valor completamente  diferente,  chamado  de  **EXC_RETURN**.  Explique  o  funcionamento  desse  mecanismo  e especifique como o **Cortex-M** consegue fazer o retorno da interrupção. 

### (k) Qual  a  diferença  no  salvamento  de  contexto,  durante  a  chegada  de  uma  interrupção,  entre  os processadores Cortex-M3 e Cortex M4F (com ponto flutuante)? Descreva em termos de tempo e também de uso da pilha. Explique também o que é ***lazy stack*** e como ele é configurado. 


## Referências

### Básicas

[1] [STM32F411xC Datasheet](https://www.st.com/resource/en/datasheet/stm32f411ce.pdf)

[2] [RM0383 Reference Manual](https://www.st.com/resource/en/reference_manual/rm0383-stm32f411xce-advanced-armbased-32bit-mcus-stmicroelectronics.pdf)

[3] [Using the GNU Compiler Collection (GCC)](https://gcc.gnu.org/onlinedocs/gcc/index.html)

[4] [GNU Make](https://www.gnu.org/software/make/manual/html_node/index.html)

### Vídeos Microsoft Teams

[5] [05 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[6] [06 - Arquitetura Cortex-M Parte 1/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[7] [07 - Arquitetura Cortex-M Parte 2/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[8] [08 - Microcontroladores STM32](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[9] [10 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

### Material Suplementar

[5] [A General Overview of What Happens Before main()](https://embeddedartistry.com/blog/2019/04/08/a-general-overview-of-what-happens-before-main/)
 
[6] [Bare metal embedded lecture-1: Build process](https://youtu.be/qWqlkCLmZoE?si=mn5yDnJYudQ1PpZH)
 
[7] [Bare metal embedded lecture-2: Makefile and analyzing relocatable obj file](https://youtu.be/Bsq6P1B8JqI?si=yuNLPj3JQ-2IT1yo)
 
[8] [Bare metal embedded lecture-3: Writing MCU startup file from scratch](https://youtu.be/2Hm8eEHsgls?si=c27MpZ47ApiMSwHR)
 
[9] [Lecture 15: Booting Process](https://youtu.be/3brOzLJmeek?si=MsHRUEJP8zofjwJQ)
