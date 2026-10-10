# Laboratório 01 — Fundamentos do Bash e Git

## 1. Objetivo

Compreender a execução de comandos no Bash, identificar comandos internos, aliases e executáveis externos, praticar a atribuição e expansão de variáveis e aplicar os fundamentos do Git para versionamento e recuperação de arquivos em uma máquina virtual Ubuntu.

## 2. Ambiente

- Sistema operacional: Ubuntu
- Shell: Bash
- Acesso remoto: SSH pelo VS Code
- Controle de versão: Git

## 3. Comandos internos, aliases e executáveis externos

### 3.1 Identificação de comandos no Bash

O Bash permite identificar a natureza de um comando utilizando o builtin `type`.

Neste laboratório, foram examinados três exemplos:

| Comando | Classificação | Resultado observado |
|---|---|---|
| `cd` | Builtin | `cd is a shell builtin` |
| `cat` | Executável externo | `cat is hashed (/usr/bin/cat)` |
| `ll` | Alias | `ll is aliased to 'ls -alF'` |

**Interpretação:**

- **Builtin:** comando implementado pelo próprio shell, como `cd`.
- **Alias:** nome alternativo que o Bash expande para outro comando ou sequência de palavras, como `ll`.
- **Executável externo:** programa localizado no sistema de arquivos, como `/usr/bin/cat`.

O comando `type` permite verificar essas diferenças diretamente no terminal.

## 4. Variáveis e expansão no Bash

### 4.1 Atribuição, expansão e execução

No Bash, atribuir um valor a uma variável não significa executar esse valor como comando.

**Atribuição:**

```bash
PROGRAMA=hostname
```

A variável `PROGRAMA` recebe o texto `hostname`.

**Expansão como argumento de `echo`:**

```bash
echo "Programa: $PROGRAMA"
```

Saída observada:

```text
Programa: hostname
```

O Bash expande `$PROGRAMA`, mas quem é executado nessa linha é o builtin `echo`.

**Execução após expansão:**

```bash
$PROGRAMA
```

Saída observada:

```text
ubuntu-lab
```

Nesse caso, o Bash expande a variável e utiliza o valor `hostname` como nome do comando a executar.

**Conclusão:** o resultado da expansão de uma variável pode ser utilizado como argumento de outro comando ou como nome de um comando, dependendo de sua posição na linha.

### 4.2 Expansão de variáveis com aspas

No Bash, as aspas influenciam a interpretação das variáveis.

**Atribuição:**

```bash
SISTEMA=Linux
```

**Aspas duplas — permitem expansão:**

```bash
echo "O sistema é $SISTEMA"
```

Saída observada:

```text
O sistema é Linux
```

**Aspas simples — impedem expansão:**

```bash
echo 'O sistema é $SISTEMA'
```

Saída observada:

```text
O sistema é $SISTEMA
```

**Conclusão:** as aspas duplas permitem que o Bash substitua `$SISTEMA` pelo valor armazenado. As aspas simples preservam o texto literalmente, incluindo o caractere `$`.

## 5. Exercícios práticos

### 5.1 Identificação de comandos

**Objetivo:** identificar como o Bash interpreta diferentes comandos.

Comandos utilizados:

```bash
type cd
type cat
type ll
```

**Resultados observados:**

- `cd`: comando interno (*builtin*) do Bash.
- `cat`: executável externo localizado em `/usr/bin/cat`.
- `ll`: alias configurado para `ls -alF`.

**Aprendizado:** comandos digitados no terminal não são necessariamente programas externos. O Bash também possui comandos internos e aliases.

### 5.2 Expansão de variáveis

**Objetivo:** verificar como o Bash interpreta variáveis com aspas simples e duplas.

```bash
SISTEMA=Linux
echo "O sistema é $SISTEMA"
echo 'O sistema é $SISTEMA'
```

**Resultados observados:**

```text
O sistema é Linux
O sistema é $SISTEMA
```

**Aprendizado:** aspas duplas permitem expansão de variáveis; aspas simples preservam o conteúdo literalmente.

## 6. Troubleshooting — recuperação de arquivo com Git

### 6.1 Cenário do incidente

Durante a organização do repositório `linux-estudos`, foi criado acidentalmente um arquivo com nome incorreto, contendo sequências de caracteres de escape.

Ao tentar remover esse arquivo com o comando `rm -i -- *`, o terminal também solicitou confirmação para remover o `README.md`.

A remoção do `README.md` foi confirmada por engano.

### 6.2 Diagnóstico

Foi utilizado o comando:

```bash
git status
```

O Git informou que o `README.md` estava preparado na staging area, mas havia sido excluído do diretório de trabalho (*working tree*).

Isso indicou que ainda existia uma versão do arquivo disponível no índice do Git.

### 6.3 Recuperação

O arquivo foi recuperado com:

```bash
git restore --worktree -- README.md
```

**Interpretação:** o comando restaurou o `README.md` no diretório de trabalho utilizando a versão armazenada na staging area.

A recuperação foi verificada com:

```bash
cat README.md
```

O conteúdo original voltou a ser exibido no terminal.

### 6.4 Lições aprendidas

- Conferir cuidadosamente os arquivos antes de confirmar uma remoção.
- Entender que `rm -i` solicita confirmação, mas não impede erros humanos.
- Evitar o uso de `*` em comandos de remoção sem verificar quais arquivos serão afetados.
- Utilizar `git status` para investigar alterações e exclusões.
- Compreender a diferença entre o diretório de trabalho e a staging area.
- Verificar a recuperação de arquivos antes de continuar o trabalho.

## 7. Evidências e resultados

### 7.1 Comandos e resultados verificados

| Comando | Resultado observado | O que demonstra |
|---|---|---|
| `type cd` | `cd is a shell builtin` | `cd` é um comando interno do Bash. |
| `type cat` | `cat is hashed (/usr/bin/cat)` | `cat` é um executável externo. |
| `type ll` | `ll is aliased to 'ls -alF'` | `ll` é um alias. |
| `echo "$SISTEMA"` | `Linux` | Aspas duplas permitem expansão de variáveis. |
| `echo '$SISTEMA'` | `$SISTEMA` | Aspas simples impedem expansão. |
| `git restore --worktree -- README.md` | Arquivo restaurado | O Git recuperou o arquivo a partir da staging area. |

### 7.2 Verificação da recuperação

Após a recuperação, o comando `cat README.md` confirmou o conteúdo original:

```text
# Linux Essentials

## Laboratorio 01 - Git

Estudando Linux, Bash e Git na VM Ubuntu.
```

### 7.3 Limitações e pendências

- O primeiro commit ainda não foi realizado.
- O repositório ainda não foi publicado no GitHub.
- Os testes estão documentados, mas ainda não foram adicionadas capturas de tela ao repositório.

## 8. Conclusão

### 8.1 Conhecimentos desenvolvidos

Neste laboratório, foram praticados fundamentos do Bash e do controle de versão com Git em uma máquina virtual Ubuntu, acessada remotamente por SSH pelo VS Code.

Os exercícios permitiram compreender:

- A diferença entre comandos internos do Bash, aliases e executáveis externos.
- A atribuição e a expansão de variáveis.
- O comportamento das aspas simples e duplas.
- A utilização de `type`, `echo`, `cat`, `head`, `tail`, `pwd` e `ls`.
- A diferença entre o diretório de trabalho e a staging area do Git.
- A recuperação de um arquivo removido acidentalmente.

### 8.2 Dificuldades encontradas

Durante a prática, houve dificuldades na interpretação da expansão de variáveis, especialmente com aspas simples e duplas.

Também ocorreram erros durante a manipulação de arquivos, permitindo exercitar o diagnóstico e a recuperação com Git.

Essas situações reforçaram a importância de interpretar os comandos antes de executá-los e verificar seus resultados no terminal.

### 8.3 Próximos passos

- Revisar a expansão de variáveis no Bash.
- Realizar o primeiro commit do repositório.
- Publicar o projeto no GitHub.
- Continuar os estudos conforme os objetivos do Linux Essentials 010-160.

## 9. Referências e materiais de apoio

### 9.1 Documentação oficial
- Instituição: Linux Professional Institute (LPI).
- Material: Linux Essentials - Material de Aprendizagem.
- Exame: 010-160.
- Arquivo consultado no curso: LPI-Learning-Material-010-160-pt.pdf.

### 9.2 Curso complementar
- Instituição: CertBest IT.
- Curso: Formação Essencial em Linux.
- Professor: Juliano Ramos.
- Plataforma: https://eadcertbest.com/
- Material utilizado: aulas e apostila de apoio do curso.

### 9.3 Ferramenta de apoio
- Ferramenta: Google NotebookLM.
- Caderno: Linux Essentials: Evolução e Distribuições.
- Finalidade: revisão de comandos internos, aliases,
  executáveis externos e variáveis no Bash.
- As respostas geradas por IA são utilizadas como apoio
  e devem ser verificadas nas fontes originais.

### 9.4 Evidências práticas
- Ambiente: máquina virtual Ubuntu.
- Acesso remoto: SSH utilizando VS Code.
- Shell utilizado: Bash.
- Comandos praticados: type, echo, cat, head, tail, pwd e ls.
- Git: inicialização do repositório e preparação do README.md.
- Troubleshooting: recuperação do README.md com git restore.
- Evidências: saídas observadas no terminal durante o laboratório.
