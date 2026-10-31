# Laboratório 05 — Navegação entre diretórios e comando `ls`

**Data:** 31/10/2026  
**Trilha:** Linux Essentials 010-160  
**Ambiente:** Ubuntu Linux, Bash, VS Code Remote SSH e Git  
**Tipo:** Laboratório prático de exploração e revisão

---

## 1. Objetivo

Compreender a navegação pelo sistema de arquivos Linux, a utilização de caminhos absolutos e relativos e o funcionamento das principais opções do comando `ls`.

Também foi explorada a diferença entre o diretório atual do terminal e a pasta aberta no Explorer do VS Code.

O laboratório surgiu durante a alternância entre dois projetos:

- `linux-estudos`: repositório principal de estudos Linux.
- `git-beyond-commit`: repositório dedicado ao aprendizado de Git e GitHub.

## 2. Ambiente utilizado

O laboratório foi realizado em uma máquina virtual Ubuntu, acessada remotamente pelo VS Code utilizando SSH.

Diretório pessoal do usuário:

```bash
/home/aluno
```

Estrutura dos projetos:

```text
/home/aluno/
├── git-beyond-commit/
│   ├── .git/
│   ├── assets/
│   │   └── mapa-mental-git.png
│   └── README.md
│
└── linux-estudos/
    ├── anotacoes/
    ├── laboratorios/
    └── README.md
```

Essa representação mostra apenas os diretórios e arquivos relevantes para o exercício, não o conteúdo completo de `/home/aluno`.

## 3. Identificação do diretório atual

O comando `pwd` permite identificar o diretório de trabalho atual do terminal.

```bash
pwd
```

Exemplo observado:

```text
/home/aluno/linux-estudos
```

**Aprendizado:** o terminal possui um diretório de trabalho atual, que pode ser diferente da pasta exibida no Explorer do VS Code.

## 4. Navegação entre diretórios

O comando `cd` permite alterar o diretório de trabalho atual.

### 4.1. Voltar ao diretório pai

```bash
cd ..
```

Exemplo:

```text
Antes:  /home/aluno/linux-estudos
Depois: /home/aluno
```

O símbolo `..` representa o diretório pai.

### 4.2. Entrar em um diretório

Estando em `/home/aluno`:

```bash
cd git-beyond-commit
```

Resultado:

```text
/home/aluno/git-beyond-commit
```

### 4.3. Navegar diretamente para o diretório pessoal

```bash
cd ~
```

O símbolo `~` é expandido pelo Bash para o diretório pessoal do usuário.

Neste ambiente:

```text
/home/aluno
```

### 4.4. Alternar entre projetos usando caminho relativo

Estando em:

```text
/home/aluno/linux-estudos
```

Foi executado:

```bash
cd ../git-beyond-commit
```

Resultado:

```text
/home/aluno/git-beyond-commit
```

**Interpretação:**

1. `..` representa o diretório pai.
2. `/` separa os componentes do caminho.
3. `git-beyond-commit` identifica o diretório de destino.

Esse comando permite navegar entre dois diretórios que compartilham o mesmo diretório pai.

## 5. Caminhos absolutos e relativos

### Caminho absoluto

Começa com `/`, representando a raiz do sistema de arquivos.

Exemplo:

```bash
cd /home/aluno/linux-estudos
```

### Caminho relativo

É interpretado a partir do diretório de trabalho atual.

Exemplo:

```bash
cd ../linux-estudos
```

### Caminho utilizando `~`

```bash
cd ~/linux-estudos
```

Nesse caso, o Bash expande `~` para `/home/aluno`.

### Comparação

| Expressão | Significado |
|---|---|
| `/` | Raiz do sistema de arquivos |
| `.` | Diretório atual |
| `..` | Diretório pai |
| `~` | Diretório pessoal do usuário, quando expandido pelo shell |
| `../linux-estudos` | Caminho relativo ao diretório pai |
| `/home/aluno/linux-estudos` | Caminho absoluto |

## 6. Erros encontrados durante o laboratório

Os erros abaixo ocorreram durante a navegação entre os projetos.

### Tentativa 1 — Diretório inexistente no caminho atual

Estando em:

```text
/home/aluno/git-beyond-commit
```

Foi executado:

```bash
cd linux-estudos
```

Resultado:

```text
bash: cd: linux-estudos: Arquivo ou diretório inexistente
```

**Causa:**

O Bash tentou acessar:

```text
/home/aluno/git-beyond-commit/linux-estudos
```

Esse diretório não existia.

**Correção:**

```bash
cd ../linux-estudos
```

### Tentativa 2 — Caminho absoluto incorreto

Foi executado:

```bash
cd /linux-estudos
```

Resultado:

```text
bash: cd: /linux-estudos: Arquivo ou diretório inexistente
```

**Causa:**

A barra inicial fez o sistema procurar o diretório diretamente na raiz:

```text
/linux-estudos
```

**Correção utilizada:**

```bash
cd ~/linux-estudos
```

**Aprendizado:** compreender de onde o caminho começa é essencial para navegar corretamente.

## 7. Diferença entre Explorer e terminal no VS Code

Durante o laboratório, surgiu uma dúvida ao alternar entre os projetos.

O Explorer continuava exibindo `git-beyond-commit`, mesmo após o terminal retornar para `/home/aluno`.

Isso ocorre porque o VS Code mantém uma pasta aberta no editor, enquanto o terminal possui seu próprio diretório de trabalho.

| Recurso | Função |
|---|---|
| Explorer | Exibe a pasta aberta no VS Code |
| Terminal | Executa comandos a partir de seu diretório atual |
| `cd` | Altera o diretório atual do terminal |
| `pwd` | Mostra o diretório atual do terminal |
| File → Open Folder | Permite abrir outra pasta no Explorer |

### Alternância entre projetos

Para visualizar outro projeto no Explorer:

1. Acessar **File → Open Folder**.
2. Navegar até `/home/aluno`.
3. Selecionar `linux-estudos` ou `git-beyond-commit`.
4. Confirmar a abertura.

**Conclusão:** alterar o diretório com `cd` não muda automaticamente a pasta aberta no Explorer.

## 8. Estudo do comando `ls`

O comando `ls` permite listar arquivos e diretórios.

Durante o laboratório, foram comparadas diferentes opções.

| Comando | Função |
|---|---|
| `ls` | Lista entradas visíveis |
| `ls -l` | Exibe uma listagem detalhada |
| `ls -a` | Inclui entradas ocultas |
| `ls -la` | Inclui entradas ocultas e informações detalhadas |
| `ls -ld .` | Exibe detalhes do diretório atual |
| `ls -ld ..` | Exibe detalhes do diretório pai |
| `ls -ld assets` | Exibe detalhes do próprio diretório `assets` |
| `ls -l assets` | Lista detalhadamente o conteúdo de `assets` |

### 8.1. A opção `-l`

```bash
ls -l
```

Apresenta informações como:

- Tipo de arquivo e permissões.
- Contagem de links.
- Proprietário.
- Grupo.
- Tamanho.
- Data de modificação.
- Nome.

### 8.2. A opção `-a`

```bash
ls -a
```

Inclui entradas cujo nome começa com ponto.

Exemplo:

```text
.
..
.git
README.md
assets
```

No Linux, nomes iniciados por `.` normalmente não aparecem nas listagens padrão.

### 8.3. Combinando opções

```bash
ls -la
```

É equivalente a:

```bash
ls -l -a
```

### 8.4. A opção `-d`

A opção `-d` permite consultar o próprio diretório, em vez de listar seu conteúdo.

Exemplo:

```bash
ls -ld assets
```

Resultado observado:

```text
drwxrwxr-x 2 aluno aluno 4096 Oct 29 21:57 assets
```

Agora, sem `-d`:

```bash
ls -l assets
```

Resultado observado:

```text
total 2020
-rw-rw-r-- 1 aluno aluno 2065087 Oct 29 21:57 mapa-mental-git.png
```

**Diferença:**

- `ls -ld assets`: apresenta informações sobre o diretório.
- `ls -l assets`: apresenta informações sobre seu conteúdo.

## 9. Diretório atual (`.`) e diretório pai (`..`)

Durante os testes, foi observada uma diferença entre dois comandos semelhantes.

### Diretório atual

```bash
ls -ld .
```

Resultado:

```text
drwxrwxr-x 4 aluno aluno 4096 Oct 29 22:09 .
```

### Diretório pai

```bash
ls -ld ..
```

Resultado:

```text
drwxr-x--- 19 aluno aluno 4096 Oct 29 21:19 ..
```

A diferença ocorreu porque os comandos consultaram diretórios diferentes.

No contexto do exercício:

```text
.  = /home/aluno/git-beyond-commit
.. = /home/aluno
```

### Por que aparecem os números 4 e 19?

Esses números representam a contagem de links associados aos diretórios.

Em sistemas de arquivos tradicionais, como ext4, essa contagem costuma estar relacionada às entradas `.` e `..` e à quantidade de subdiretórios imediatos.

Uma relação comum é:

```text
Contagem de links = 2 + quantidade de subdiretórios imediatos
```

Essa relação depende do sistema de arquivos e não deve ser tratada como uma regra universal.

**Importante:** o número `19` não significa que existem 19 arquivos dentro do diretório.

## 10. Identificação de arquivos e diretórios

Na saída detalhada do comando `ls`, o primeiro caractere identifica o tipo de entrada.

### Diretório

```text
drwxrwxr-x
^
```

O caractere `d` identifica um diretório.

### Arquivo comum

```text
-rw-rw-r--
^
```

O caractere `-` identifica um arquivo comum.

### Introdução às permissões

As letras seguintes representam permissões:

| Símbolo | Significado |
|---|---|
| `r` | Read — leitura |
| `w` | Write — escrita |
| `x` | Execute — execução |
| `-` | Permissão ausente naquela posição |

As permissões são organizadas em três grupos:

```text
d | rwx | rwx | r-x
    dono grupo outros
```

Neste laboratório, foi realizada apenas a identificação inicial dessas permissões.

O estudo aprofundado de permissões, proprietários e grupos poderá ser desenvolvido em uma etapa posterior.

## 11. Principais aprendizados

Este laboratório permitiu compreender que:

1. O Explorer do VS Code e o terminal possuem contextos de navegação distintos.
2. O comando `pwd` identifica o diretório atual do terminal.
3. O comando `cd` permite navegar pela estrutura de diretórios.
4. Caminhos relativos dependem do diretório atual.
5. Caminhos absolutos começam na raiz `/`.
6. O símbolo `.` representa o diretório atual.
7. O símbolo `..` representa o diretório pai.
8. O símbolo `~` permite referenciar o diretório pessoal no Bash.
9. A opção `-a` inclui entradas ocultas na listagem.
10. A opção `-l` apresenta informações detalhadas.
11. A opção `-d` altera a forma como o `ls` trata diretórios.
12. O primeiro caractere da listagem detalhada permite distinguir arquivos comuns de diretórios.

## 12. Perguntas para revisão

**1.** Qual é a diferença entre `.` e `..`?

**2.** Por que `cd linux-estudos` pode falhar quando executado dentro de `git-beyond-commit`?

**3.** Qual é a diferença entre um caminho absoluto e um caminho relativo?

**4.** O que representa o símbolo `~` no Bash?

**5.** Qual comando lista entradas ocultas sem solicitar o formato detalhado?

**6.** Qual é a diferença entre `ls -ld assets` e `ls -l assets`?

**7.** O que significa o primeiro caractere `d` na saída de `ls -l`?

**8.** Por que executar `cd ..` não altera automaticamente a pasta aberta no Explorer do VS Code?

**9.** O que representa a contagem de links exibida por `ls -l`?

**10.** Estando em `/home/aluno/linux-estudos`, como acessar `git-beyond-commit` usando um único comando e caminho relativo?

## 13. Conclusão

O laboratório começou com uma dúvida sobre como alternar entre projetos no VS Code e evoluiu para uma investigação prática sobre diretórios, caminhos, listagens e metadados no Linux.

Os erros de navegação foram utilizados para compreender como o Bash interpreta os caminhos informados.

O objetivo não foi memorizar comandos isolados, mas compreender seus componentes e observar o comportamento real do sistema.

---

## 14. Revisão de alterações com Git Diff

Durante a atualização do README principal, utilizamos o Git
para conferir as alterações antes de registrá-las.

### 14.1 Verificando alterações não preparadas

```bash
git diff -- README.md
```

Mostra as diferenças entre o arquivo de trabalho e a staging area.

### 14.2 Verificando alterações preparadas

```bash
git diff --staged -- README.md
```

Mostra as diferenças entre a staging area e o último commit.

### 14.3 Interpretando o resultado

- `+` indica uma linha adicionada.
- `-` indica uma linha removida.
- `@@` identifica a localização das alterações.
- `--` separa os argumentos de revisão das opções de caminho.

### 14.4  Aprendizado prático

Após executar `git add README.md`, o comando `git diff -- README.md`
não apresentou diferenças.

Entretanto, `git diff --staged -- README.md` mostrou a linha
adicionada ao índice do repositório.

Isso demonstrou a diferença entre alterações no diretório de
trabalho e alterações preparadas para o próximo commit.

Fluxo praticado:

Editar → Conferir → Preparar → Registrar → Publicar.

---

**Estudar. Compreender. Praticar. Documentar. Compartilhar.**
