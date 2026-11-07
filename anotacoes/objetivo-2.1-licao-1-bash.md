# Linux Essentials 010-160 — Objetivo 2.1 — Lição 1

**Tema:** fundamentos da linha de comando no Bash  
**Situação:** Lição 1 estudada, exercícios guiados e exploratórios praticados; Objetivo 2.1 ainda em andamento.  
**Referência principal:** material oficial LPI Linux Essentials 010-160 (v1.6), Objetivo 2.1, Lição 1.  
**Método:** estudar, compreender, praticar, documentar e compartilhar.

## Estrutura de um comando

Formato geral: `comando [opções] [argumentos]`.

| Exemplo | Comando | Opções | Argumento |
| --- | --- | --- | --- |
| `ls -l /etc` | `ls` | `-l` | `/etc` |
| `ls -l -a` | `ls` | `-l`, `-a` | nenhum caminho explícito |
| `cd /home/user` | `cd` | nenhuma | `/home/user` |

O caminho `/home/user` é um exemplo do exercício; no laboratório real, o usuário era `aluno`.

## Comandos internos e externos do Bash

Um **builtin** é implementado no próprio shell. Um comando **externo** é normalmente executado a partir de um programa no sistema de arquivos. O Bash pode manter caminhos de comandos externos na sua tabela hash; isso **não** os transforma em builtins.

| Comando | Tipo no Bash | Uso básico |
| --- | --- | --- |
| `cd` | interno | alterar diretório |
| `pwd` | interno (também existe versão externa) | mostrar diretório atual |
| `echo` | interno (também existe versão externa) | exibir texto |
| `exit` | interno | encerrar shell |
| `type` | interno | identificar como o shell reconhece um comando |
| `history` | interno | consultar histórico |
| `export` | interno | exportar variáveis |
| `unset` | interno | remover variáveis/funções |
| `alias` | interno | definir apelidos |
| `ls` | externo | listar arquivos |
| `cat` | externo | mostrar/concatenar arquivos |
| `touch` | externo | criar arquivo ausente ou atualizar datas |
| `mkdir` | externo | criar diretórios |
| `rm` | externo | remover arquivos |
| `rmdir` | externo | remover diretório vazio |
| `cp` | externo | copiar arquivos |
| `mv` | externo | mover/renomear |
| `tail` | externo | mostrar linhas finais |

**Evidência observada:** `type touch` retornou `touch está na tabela hash (/usr/bin/touch)`. Isso identifica um executável externo. Para verificar outros comandos: `type cd`, `type cat`, etc. A classificação depende do shell e de eventuais aliases/funções.

## Aspas e escape

- Aspas simples `'...'`: preservam literalmente os caracteres dentro delas, sem expansão de variáveis.
- Aspas duplas `"..."`: preservam o texto como um argumento, mas permitem expansões como `$USER`.
- Barra invertida `\`: pode proteger um caractere da interpretação do shell, conforme o contexto.

Exemplos estudados: `touch "$USER"` usa o nome do usuário atual (no laboratório, `aluno`); `touch 'touch'` usa o nome literal `touch`, **sem aspas no nome do arquivo**.

## Expansão de chaves e padrões de arquivos

- `game{1..5}` gera as palavras `game1 game2 game3 game4 game5`, mesmo que os arquivos não existam.
- `game{1,2,3,4,5}` gera a mesma lista por enumeração explícita.
- `game?` corresponde a nomes existentes com `game` seguido de **exatamente um caractere**.
- `teste??` corresponde a `teste` seguido de **exatamente dois caracteres**.

Não confundir `game{1..5}` com `game{1.2.3.4.5}`: a segunda forma não define uma sequência numérica válida.

## Operadores complementares explorados

Estes operadores apareceram na prática e foram investigados como **complemento**, sem antecipar a conclusão de outras lições.

| Sintaxe | Comportamento | Cuidado |
| --- | --- | --- |
| `comando1 && comando2` | executa o segundo somente se o primeiro terminar com sucesso | verificar cada etapa |
| `comando > arquivo` | redireciona a saída padrão, criando ou sobrescrevendo o arquivo | pode perder conteúdo anterior |
| `comando >> arquivo` | acrescenta a saída padrão ao final do arquivo | não sobrescreve o conteúdo anterior |
| `comando1 | comando2` | conecta a saída padrão do primeiro à entrada padrão do segundo | os comandos têm funções distintas |
| `\` | escape de caracteres em determinados contextos do Bash | efeito depende das aspas e do contexto |

**Exemplos realmente praticados:** `history | tail -n 5`, `history | tail -n 3`, `echo Linux > redes.txt`, `echo Cisco > redes.txt` e `echo Linux >> redes.txt`.

## Aprendizados e pontos de reforço

- Distinguir `cat`, `touch`, `mkdir` e `cp` (externos) de `cd` e `exit` (internos).
- Ler a sintaxe com atenção: `{1..5}` usa **dois pontos consecutivos**.
- Conferir o resultado com `ls` e `cat`; ausência de mensagem não substitui validação.
- Antes de `rm` com curinga, visualizar quais nomes correspondem ao padrão.
- A opção `-p` de `mkdir` e o operador `&&` foram introduzidos durante a prática e explicados posteriormente; devem ser entendidos antes de reutilização.

**Laboratório relacionado:** [LPI 2.1 — Lição 1 — Bash](../laboratorios/lpi-2.1-licao-1-bash/README.md).

**Próxima etapa de estudo:** Objetivo 2.1, Lição 2. Não declarar o objetivo inteiro concluído.

