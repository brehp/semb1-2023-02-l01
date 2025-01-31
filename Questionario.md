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
As dependências de um target estão associadas as dependências dos prerequisites, pois cada um contem uma lista de arquivos que é necessário para
realizar a sua compilação de maneira adequada e não gerar erros, elas são especificadas no contexto de compilação e compilados antes do target, senão
o compilador não teria acesso aos recursos dos arquivos-fontes ou bibliotecas externas. O make utiliza elas para definir quais targets precisam ser 
atualizados quando há uma mudança nos arquivos associados. Quando o utilitário é usado, ele verifica os timestamps dos arquivos de prerequisites e compara
com o do target, se o do target for mais "velho" significa que ele precisa ser reconstruido, assim executa os comandos escritos na regra do makefile. A 
prática descrita permite que o makefile seja uma ferramenta eficiente e de grande atualização.

#### (e) O que são as regras do **Makefile**, qual a diferença entre regras implícitas e explícitas?
As regras informam quando o target está desatualizado e precisa reconstrui-lo, pois houve mudanças nos arquivos-fontes, bem como, oferta instruções de como reconstruir 
o arquivo adequadamente e somente das partes necessárias não perdendo tempo de processamento com arquivos que não foram modificados. A regra explicita determina como e 
quando refazer os arquivos, utilizando comando relacionados com o nome dos arquivos a serem compilados, já as implícitas utilizam as extensões dos arquivos para falar
quais comandos devem ser executados, deixando o código mais generico, porém mais difícil de ser visualizado e compreendido.


## 4. Sobre a arquitetura **ARM Cortex-M** responda:

### (a) Explique o conjunto de instruções ***Thumb*** e suas principais vantagens na arquitetura ARM. Como o conjunto de instruções ***Thumb*** opera em conjunto com o conjunto de instruções ARM?
O conjunto de instruções Thumb é vital para utilizar a arquitetura ARM, pois otimiza o seu desempenho, economiza espaço, além de reduzir o consumo de energia. O thumb 
possui 16 bits e coexiste com o conjunto de instruções ARM que possuem 32 bits, seu principal objetivo é oferecer maior densidade ao codigo, já que economiza espaço de
memoria, em razão de suas instruções serem mais curtas, melhora a eficiência do cache, já que as instruções são armazenadas nele e economiza energia, porque a memoria
é menor. Como o thumb e o ARM coexistem, o desenvolvedor escolhe qual combinação melhor atende suas necessidades, essa posssibilidade garante uma maior flexibilidade
sendo considerado uma vantagem ao processador ARM. 

### (b) Explique as diferenças entre as arquiteturas ***ARM Load/Store*** e ***Register/Register***.
A arquitetura ARM Load/Store, é um processador RISC e suas instruções de acesso à memória não interagem diretamente com os registradores. Ela possui duas instruções,
a Load (LDR) que carrega dados da memória para o registrador, e a Store (STR) que armazena dados dos registradores na memória. A arquitetura simplifica o conjunto
de instruções fazendo com que gaste menos energia, além de reduzir a complexidade. Todavia necessita de mais instruções para realizar operações aritméticas.
No que se refere a Register/Register, as suas operações matemáticas são realizadas diretamente nos registradores não tendo acesso à memoria, as suas manipulações são
mais eficiente e melhora o desempenho, contudo a complexidade do hardware aumenta e necessita de mais registradores.

### (c) Os processadores **ARM Cortex-M** oferecem diversos recursos que podem ser explorados por sistemas baseados em **RTOS** (***Real Time Operating Systems***). Por exemplo, a separação da execução do código em níveis de acesso e diferentes modos de operação. Explique detalhadamente como funciona os níveis de acesso de execução de código e os modos de operação nos processadores **ARM Cortex-M**.
O ARM Cortex-M possui dois níveis de acesso, o privilegiado, no qual todas as funcionalidades do processador estão disponíveis para serem manipulados e o não privilegiado
onde algumas restrições foram impostas pelo programador, afim de não afetar o bom funcionamento do programa e terceiros não acarretarem nenhum erro.  
Em relação aos modos há quatro modos de operação: o modo de Usuário onde somente instruções predeterminadas são executadas, afim de garantir a compilação segura e sem erros
do código fonte, além do acesso seguro à memória, modo de Interrupção, utilizado em interrupções e permite um acesso privilegiado em quando ela está sendo tratada, 
bem como, garante a assiduidade na execução do código, Modo de Exceção, ativado quando há uma falha ou instrução inválida, permitindo que um erro não seja levado até o final
podendo ocasionar em consequências piores, por fim o modo de depuração utilizado para depurar o código proporcionando acesso à recursos específicos. 
Em suma, os níveis de acesso ditam os limites do processador e os modos de operação como o processador vai lidar com um determinado evento e com ações limitadas ou não.

### (d) Explique como os processadores ARM tratam as exceções e as interrupções. Quais são os diferentes tipos de exceção e como elas são priorizadas? Descreva a estratégia de **group priority** e **sub-priority** presente nesse processo.
As exceções e interrupções são tratadas pelo NVIC, ele que define qual será executada primeiro, a de maior urgência e a de menor, consegue fazer isso por meio de registradores, os quais
são programáveis e modificados conforme o objetivo do desenvolvedor. Primeiramente é preciso definir que exceções são erros desencadeados durante a execução do código, por exemplo, divisão
por zero, extrapolou a memória, execução de ações privilegiadas que não são permitidas, já a interrupção são eventos externos que interferem no fluxo normal do código, como entradas,
temporizador, comunicação com periféricos. As prioridades das exceções é dada conforme a sua urgência e importância em relação ao programa, o NVIC possui dois níveis de prioridade para fazer o gerenciamento das exceções, o Group Priority que divide elas em diferentes grupos, os quais possuem prioridades diferentes, se dentro deles houver exceções com mesmo nível de prioridade utiliza a sub-priority, nelas as exceções são tratadas conforme a ordem de chegada.

### (e) Qual a diferença entre os registradores **CPSR** (***Current Program Status Register***) e **SPSR** (***Saved Program Status Register***)?
O CPSR contem informações sobre o estado do processador, bits de condição, resultado das operações lógicas, controla as interrupções e o modo de operação delas, para isso utiliza flags: N, caso o sinal seja positivo ou negativo, Z, resultado zero, C quando há carry, V se estourar o campo de operação, I desabilita interrupções IRQ, F desabilita interrupções FIQ e T que explicita se o processador está executando instruções ARM ou thumb. 
Já o SPSR é usado em interrupções e em chamadas de sub-rotinas, ele armazena o estado do CPSR para depois da interrupção ele possa ser restaurado adequadamente sem nenhuma perda. Cada tipo de interrupção tem um SPSR diferente, em razão disso que consegue restaurar o CPSR de maneira tão completa. 

### (f) Qual a finalidade do **LR** (***Link Register***)?
O LR armazena o endereço da memória no qual a rotina estava acontecendo, desse modo, quando acabar a execução da subrotina o código irá saber o local que deve voltar, diminuindo as possibilidades de erros no retorno.

### (g) Qual o propósito do Program Status Register (PSR) nos processadores ARM?
O PSR é um registrador de 32 bits, que controla o processador e gerência suas interrupções, bem como, fala qual o estado recente de operação dele. Ele garante que a modificação do ambiente de execução possa ser executada utilizando instruções de baixo nível, além disso, combina registradores para torna-lo mais eficiente. 

### (h) O que é a tabela de vetores de interrupção?
É uma tabela que contem informações de vários endereços na memória os quais indicam rotinas destinadas a tratamento de interrupções, quando há alguma interrupção o linker register e PSR salvam seu estado e posição para haver o tratamento desse contratempo, o endereço dessa sub-rotina está sendo apontado por uma das linhas dos vetores de interrupção. Nessa tabela há 15 vetores de interrupção destinados as exções advindas do processador, e 86 endereços para tratar interrupções ou eventos externos advindos do periférico, entretanto, todas elas são gerenciadas pelo NVIC. Por fim, ela é armazenada no início da FLASH, por ser um requisito de arquitetura.

### (i) Qual a finalidade do NVIC (**Nested Vectored Interrupt Controller**) nos microcontroladores ARM e como ele pode ser utilizado em aplicações de tempo real?
O NVIC é um controlador que gerencia e fornece comandos baseados em interrupções nos microcontroladores ARM Cortex-M, ele é integrado junto ao núcleo do Cortex-M e faz todo o tratamento de interrupções. O NVIC determina a priorização das diferentes interrupções, possue uma reposta rápida quando elas são acionadas, encadeando o tratamento delas, pode realizar a realocação da tabela de vetores, entre outras. Em tempo real ele pode realizar a leitura rápida de sensores e comunicação entre periféricos, garantindo o gerenciamento eficiente das interrupções do aparelho.

### (j) Em modo de execução normal, o Cortex-M pode fazer uma chamada de função usando a instrução **BL**, que muda o **PC** para o endereço de destino e salva o ponto de execução atual no registador **LR**. Ao final da função, é possível recuperar esse contexto usando uma instrução **BX LR**, por exemplo, que atualiza o **PC** para o ponto anterior. No entanto, quando acontece uma interrupção, o **LR** é preenchido com um valor completamente  diferente,  chamado  de  **EXC_RETURN**.  Explique  o  funcionamento  desse  mecanismo  e especifique como o **Cortex-M** consegue fazer o retorno da interrupção. 
Quando está no modo de execução normal e uma instrução BL é executada o PC assume o endereço que o comando mandou ele ir e o do modo de execução normal é salvo no LR, para após o tratamento da interrupção, o PC possa voltar ao local de onde ele saiu. No momento que ocorre essa pertubação o processador Cortex-M salva o contexto no qual estava na pilha e o valor EXC_RETURN é colocado no LR, afim de mostrar como deve ser o retorno, o EXC_RETURN codifica informações a respeito do modo de operação, por exemplo, se está usando o process Stack Pointer ou o Main Stack Pointer, além de ditar se deve voltar ao estado anterior ou se algo deve mudar depois da interrupção, em suma ele fala como o contexto deve ser restaurado.

### (k) Qual  a  diferença  no  salvamento  de  contexto,  durante  a  chegada  de  uma  interrupção,  entre  os processadores Cortex-M3 e Cortex M4F (com ponto flutuante)? Descreva em termos de tempo e também de uso da pilha. Explique também o que é ***lazy stack*** e como ele é configurado. 
O processador precisava salvar o contexto em que estava antes de ir tratar uma interrupção afim de que quando ela terminar ele saiba para onde voltar. No cortex-M3 uso uma pilha completa para salvar o contexto deixando o tempo de salvamento mais rapido, pois os registradores de uso geral e de ponto flutuante não são diferenciados, eles apenas são empilhados na pilha. Já no Cortex-M4F o tempo de salvamento é mais lento porque os registradores de uso geral e ponto flutuante são diferenciado, o de uso geral são empilhados na pilha e os de ponto flutuante somente são salvos se houver necessidade deles no tratamento da interrupção, esse processo economiza espaço na pilha. O lazy Stack é essa tecnica usada pelo cortex-M4F onde somente os registradores gerais são salvos na pilha e os de ponto flutuante são salvos conforme a demanda, ele é configurada por meio de bits de controle e conforme eles que o processador determina se é preciso salva-los ou não, essa tecnica otimiza o salvamento de contexto.   

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
