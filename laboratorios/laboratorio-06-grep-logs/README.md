# Laboratório 06 — Investigação de logs com grep e pipe

**Data:** 31/10/2026  
**Trilha:** Linux Essentials 010-160  
**Ambiente:** Ubuntu Linux, Bash e terminal SSH

## 1. Objetivo

Praticar a pesquisa e filtragem de informações em arquivos de texto utilizando comandos Linux.

Comandos estudados:

- `cat`
- `grep`
- `head`
- `tail`
- `ls`
- `du`
- `stat`
- Pipe (`|`)

## 2. Ambiente de laboratório

O laboratório foi iniciado no diretório temporário:

```bash
/tmp/lab-grep
```

Foi criado o arquivo `sistema.log`, contendo mensagens simuladas de um sistema.

Posteriormente, o arquivo foi copiado para o repositório `linux-estudos`.

## 3. Arquivo utilizado

Conteúdo do arquivo `sistema.log`:

```text
INFO Serviço iniciado
ERROR Falha de autenticação
INFO Conexão estabelecida
WARNING Memória elevada
ERROR Acesso negado
INFO Serviço finalizado
error Falha de autenticação
error negado
```

As duas últimas linhas foram acrescentadas durante o estudo para investigar a diferença entre pesquisas que consideram ou ignoram maiúsculas e minúsculas.

## 4. Pesquisando erros com grep

```bash
grep "ERROR" sistema.log
```

Resultado:

```text
ERROR Falha de autenticação
ERROR Acesso negado
```

O comando encontrou duas linhas contendo `ERROR`.

## 5. Ignorando maiúsculas e minúsculas

```bash
grep -i "error" sistema.log
```

Resultado:

```text
ERROR Falha de autenticação
ERROR Acesso negado
error Falha de autenticação
error negado
```

A opção `-i` permite localizar o padrão independentemente de maiúsculas e minúsculas.

## 6. Contando ocorrências por linha

```bash
grep -ic "error" sistema.log
```

Resultado:

```text
4
```

A opção `-c` conta as linhas correspondentes ao padrão.

## 7. Identificando números das linhas

```bash
grep -n "ERROR" sistema.log
```

Resultado:

```text
2:ERROR Falha de autenticação
5:ERROR Acesso negado
```

A opção `-n` apresenta os números das linhas no arquivo original.

## 8. Excluindo linhas com grep

```bash
grep -v "ERROR" sistema.log
```

A opção `-v` apresenta as linhas que não correspondem ao padrão pesquisado.

## 9. Combinando grep com pipe

Primeiro erro:

```bash
grep "ERROR" sistema.log | head -n 1
```

Resultado:

```text
ERROR Falha de autenticação
```

Último erro:

```bash
grep "ERROR" sistema.log | tail -n 1
```

Resultado:

```text
ERROR Acesso negado
```

O pipe conecta a saída padrão de um comando à entrada padrão do próximo.

## 10. Investigando o espaço ocupado pelo arquivo

Comandos executados:

```bash
ls -ls sistema.log
du -h sistema.log
stat sistema.log
```

Resultados observados:

| Informação | Resultado |
|---|---|
| Tamanho do arquivo | 193 bytes |
| Espaço alocado | 4 KiB |
| Blocos informados pelo stat | 8 |
| Unidade dos blocos do stat | 512 bytes |
| Bloco de E/S informado | 4096 bytes |

Cálculo:

```text
8 × 512 = 4096 bytes = 4 KiB
```

O exercício demonstrou a diferença entre o tamanho lógico do arquivo e o espaço alocado no sistema de arquivos.

## 11. Conclusão

O laboratório permitiu compreender como pesquisar, filtrar e contar linhas em arquivos de texto.

Também demonstrou a importância de interpretar todos os comandos de um pipeline.

Durante o estudo, o arquivo de logs foi modificado propositalmente para testar diferentes comportamentos do `grep`.

A investigação foi complementada com comandos de análise de espaço em disco.

**Estudar. Compreender. Praticar. Documentar. Compartilhar.**
