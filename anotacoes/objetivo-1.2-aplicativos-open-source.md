# Objetivo 1.2 — Principais Aplicativos de Código Aberto

## O que aprendi

Neste objetivo do Linux Essentials, estudei aplicativos de código aberto utilizados em diferentes atividades, como edição de documentos, imagens, áudio e administração de sistemas.

Também pratiquei a pesquisa, instalação e remoção de pacotes no Ubuntu usando o APT.

## Aplicativos estudados

| Aplicativo | Finalidade |
|---|---|
| LibreOffice Writer | Criar e editar documentos de texto |
| LibreOffice Calc | Criar e editar planilhas |
| LibreOffice Impress | Criar apresentações |
| GIMP | Editar imagens |
| Inkscape | Criar desenhos vetoriais |
| Audacity | Editar áudio |
| ImageMagick | Processar e converter imagens pelo terminal |
| Blender | Modelagem e criação de conteúdo 3D |
| Chromium | Navegador de código aberto |
| Samba | Compartilhar arquivos e impressoras pela rede usando SMB |

## Prática no terminal — Gerenciamento de pacotes com APT

Durante os exercícios, utilizei o APT para pesquisar pacotes, consultar informações e verificar se programas estavam instalados.

### Comandos utilizados

```bash
apt search audacity
apt show audacity
apt list --installed audacity
```

**O que observei:**

- `apt search` pesquisa pacotes disponíveis.
- `apt show` apresenta informações como versão, descrição e dependências.
- `apt list --installed` permite verificar se um pacote está instalado.
- O Audacity estava disponível nos repositórios, mas não estava instalado como pacote APT.

### Simulação de remoção

```bash
apt -s remove figlet
```

Aprendi que a opção `-s` simula a operação sem remover pacotes.

No meu laboratório, o APT informou que o `figlet` não estava instalado e que nenhum pacote seria removido.

Também estudei a diferença entre:

- `remove`: remove o pacote, podendo preservar configurações.
- `purge`: remove o pacote e suas configurações de sistema gerenciadas pelo APT.
- `autoremove`: remove dependências instaladas automaticamente que não são mais necessárias.

**Cuidado:** antes de executar uma remoção real, é importante verificar quais pacotes serão afetados.

## Laboratório — Conversão de imagens com ImageMagick

### Objetivo

Converter uma imagem PNG para JPEG utilizando o terminal Linux.

### Comandos executados

Criei uma imagem azul de 400 × 200 pixels usando o ImageMagick:

```bash
magick -size 400x200 xc:blue imagem-teste.png
```

Depois converti a imagem do formato PNG para JPEG:

```bash
magick imagem-teste.png imagem-teste.jpg
```

A conversão criou um novo arquivo chamado `imagem-teste.jpg`, mantendo o arquivo PNG original.

### Verificação dos resultados

Utilizei os comandos:

```bash
ls -lh imagem-teste.*
magick identify imagem-teste.png imagem-teste.jpg
```

Observei que os dois arquivos tinham as mesmas dimensões, mas tamanhos diferentes:

| Arquivo | Dimensões | Tamanho |
|---|---|---|
| `imagem-teste.png` | 400 × 200 pixels | 334 bytes |
| `imagem-teste.jpg` | 400 × 200 pixels | 1.225 bytes |

**Conclusão:** converter o formato de uma imagem não significa alterar suas dimensões. Também aprendi que um arquivo JPEG nem sempre ocupa menos espaço que um PNG.

## Laboratório — Instalação e diagnóstico do Blender

### Objetivo

Instalar o Blender no Ubuntu e verificar seu funcionamento.

### Instalação

Utilizei o APT para instalar o programa:

```bash
sudo apt install blender
```

Depois consultei informações sobre o pacote:

```bash
apt show blender
```

### Problema encontrado

O Blender foi instalado, mas apresentou falha ao iniciar na máquina virtual Ubuntu.

As mensagens de erro mencionavam `EGL_BAD_MATCH`, o renderizador `SVGA3D` e a ausência de suporte ao recurso `ARB_shader_draw_parameters` do OpenGL.

### Investigação

A principal hipótese foi uma limitação de compatibilidade entre os recursos gráficos oferecidos pela máquina virtual e os requisitos do Blender.

A instalação do pacote não garante que o aplicativo consiga executar corretamente no ambiente.

### Remoção

Como o Blender não funcionou no laboratório, removi o pacote:

```bash
sudo apt remove blender
```

Depois verifiquei se ele continuava instalado pelo APT:

```bash
apt list --installed blender
```

Também simulei uma limpeza de dependências:

```bash
apt -s autoremove
```

O APT apresentou uma lista de pacotes candidatos à remoção, mas **não executei o `autoremove` real**.

### O que aprendi

Aprendi que um programa pode ser instalado corretamente e ainda assim falhar durante a execução por limitações do ambiente.

Também pratiquei a leitura de mensagens de erro, a formulação de hipóteses e a remoção segura de pacotes.


