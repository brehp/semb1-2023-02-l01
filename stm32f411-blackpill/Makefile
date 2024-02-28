#Comando que corresponde ao compilador
Compilado = arm-none-eabi-gcc

#Comando para remover os arquivos compilados pelo make
Remove = rm -rf

# Diretorio que armazenaram os arquivo .o (objetos)
DiretorioO = build

#Diretorio que armazena a lista de dependencias do arquivo .c
DiretorioD = .deps

#Arquivos que vao virar objeto e irão gerar lista de dependencia
ArquivoC = startup.c \
        main.c

#Conjunto de comandos para conseguir gerar informações de debug (-g), desabilitar otimizações (O0), falar o processador (-mcpu=cortex-m4), ligar Warning (-Wall) e alterar o conjunto de instruções(-mthumb)
ComandoO = -g -mcpu=cortex-m4 -mthumb -Wall -O0

#comandos utilizados para gerar lista de dependencia 
ComandoD = -MMD -MP -MF $(DiretorioD)/$*.d

#Gera um lista de arquivos objetos com base em seus nomes
ListaO = $(patsubst %, $(DiretorioO)/%.o, $(basename $(ArquivoC)))

#Cria diretorio onde os arquivos objetos vão ser feitos
$(shell mkdir -p $(dir $(DiretorioO)) > /dev/null)

#Gera um lista de dependencia e cria seu diretorio 
ListaD = $(patsubst %, $(DiretorioD)/%.d, $(basename $(ArquivoC)))
$(shell mkdir -p $(dir $(DiretorioD)) > /dev/null)

#regra para executar todo o codigo pois makefile so faz a primeira regra
all: $(ListaO)

#regra para gerar os arquivos .o e as dependencias
$(DiretorioO)/%.o: %.c $(DiretorioD)/%.d
	$(Compilado) -c $(ComandoO) $(ComandoD) $< -o $@


# Cria um novo target para cada arquivo de dependencia
$(ListaD):

# Inclui conteudo dos arquivos de dependencia
-include $(ListaD)

.PHONY: clean
clean:
	$(Remove) $(DiretorioO) $(DiretorioD)
