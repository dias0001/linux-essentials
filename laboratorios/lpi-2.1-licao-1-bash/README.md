# Laboratório complementar — LPI 2.1, Lição 1 — Bash

**Ambiente:** Ubuntu, usuário `aluno`, shell Bash.  
**Diretório temporário utilizado:** `/tmp/lpi-2.1-lab`.  
**Situação:** execução e validação registradas a partir das saídas reais do terminal.

> O diretório `/tmp/lpi-2.1-lab` é um local de trabalho temporário na VM, **não** uma pasta a versionar no Git. Este README registra os procedimentos e resultados, não copia os arquivos temporários para o repositório.

## 1. Preparação e navegação

```bash
mkdir -p /tmp/lpi-2.1-lab && cd /tmp/lpi-2.1-lab
pwd
```

**Resultado observado de `pwd`:** `/tmp/lpi-2.1-lab`.

- `mkdir -p` cria o diretório se necessário; não falha só porque já existe.
- `&&` só executa `cd` se `mkdir` terminar com sucesso.
- `ls -la /` lista a raiz `/`, mesmo quando o terminal está em outro diretório.
- `cd ..` sobe um nível; `cd` sem argumento retorna ao diretório pessoal.

## 2. Erro real na expansão de chaves

**Primeira tentativa registrada no histórico:**

```bash
touch game{1.2.3.4.5}
```

O Bash não expandiu essa expressão em cinco nomes. O `ls -l` mostrou **um único arquivo**:

```text
game{1.2.3.4.5}
```

**Correção executada:**

```bash
touch game{1..5}
ls -l
```

**Resultado observado:** `game1`, `game2`, `game3`, `game4`, `game5` e o arquivo anterior `game{1.2.3.4.5}`. Todos estavam vazios, com tamanho 0 byte.

## 3. Investigar padrões antes de remover

**Comando de inspeção executado:**

```bash
printf '%s\n' game?
```

**Saída observada:**

```text
game1
game2
game3
game4
game5
```

O padrão `game?` selecionou nomes com exatamente um caractere depois de `game`, sem selecionar `game{1.2.3.4.5}`.

**Remoção executada e verificada:**

```bash
rm game?
ls -l
```

O `ls -l` mostrou apenas `game{1.2.3.4.5}`. Depois:

```bash
rm 'game{1.2.3.4.5}'
ls -l
```

**Resultado observado:** `total 0`. As aspas simples preservaram o nome literal. A verificação com `ls -l` não inclui eventuais arquivos ocultos; o registro confirma que não restaram arquivos visíveis.

## 4. Histórico e pipe

**Comandos executados:**

```bash
history | tail -n 5
history | tail -n 3
```

O histórico revelou a entrada `touch game{1.2.3.4.5}`, permitindo identificar o erro de digitação. `history` fornece os dados; `tail -n 3` mostra as três últimas linhas recebidas via pipe `|`.

## 5. Redirecionamento de saída

**Sequência executada:**

```bash
echo Linux > redes.txt
cat redes.txt
# Linux

echo Cisco > redes.txt
cat redes.txt
# Cisco

echo Linux >> redes.txt
cat redes.txt
# Cisco
# Linux
```

- `>` sobrescreveu o conteúdo de `redes.txt`.
- `>>` acrescentou uma nova linha sem apagar a anterior.
- `cat` confirmou o resultado de cada etapa.

**Estado final documentado:** após a remoção dos arquivos `game*`, o diretório ficou sem arquivos visíveis; posteriormente, `redes.txt` foi criado e continha as linhas `Cisco` e `Linux`. Não foi registrada sua remoção.

## 6. Comandos internos e externos

**Verificação real executada:**

```bash
type touch
```

**Saída observada:**

```text
touch está na tabela hash (/usr/bin/touch)
```

Isso indica que `touch` é um comando externo cujo caminho foi memorizado pelo Bash. A classificação comparativa está em [Anotações — Objetivo 2.1, Lição 1](../../anotacoes/objetivo-2.1-licao-1-bash.md).

## 7. Lições aprendidas

1. Ler cada caractere da sintaxe antes de executar.
2. Entender operadores novos antes de usá-los em comandos combinados.
3. Formular hipóteses, observar a saída, investigar erros e validar a correção.
4. Conferir curingas antes de executar `rm`.
5. Registrar somente comandos e resultados efetivamente observados; não inventar saídas.

**Escopo:** laboratório complementar da **Lição 1**. O Objetivo 2.1 permanece em andamento.
