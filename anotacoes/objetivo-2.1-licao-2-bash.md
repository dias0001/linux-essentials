# Linux Essentials 010-160 — Objetivo 2.1 — Lição 2

**Tema:** variáveis do Bash, ambiente, expansão e substituição de comandos.  
**Situação:** teoria e exercícios guiados estudados; exercícios exploratórios 1 a 4 praticados; exercício 5 e revisão final pendentes.  
**Referência principal:** material oficial LPI Linux Essentials 010-160 (v1.6), Objetivo 2.1, Lição 2.  
**Método:** estudar, compreender, praticar, documentar e compartilhar.

## Variáveis locais e variáveis de ambiente

Uma variável permite armazenar um valor para utilização pelo shell.

No Bash, a atribuição utiliza o formato `NOME=valor`, sem espaços ao redor do sinal de igualdade.

```bash
number=10
```

A variável `number` foi criada no shell atual. Ela não é automaticamente transmitida aos processos filhos.

Para exportar uma variável:

```bash
export ORDER=100
```

A variável `ORDER` passa a fazer parte do ambiente exportado pelo shell, podendo ser herdada pelos processos filhos.

**Importante:** variável local não significa processo pai, assim como variável de ambiente não significa processo filho. Ambas existem no shell atual; a diferença está na herança.

## Expansão de variáveis

O símbolo `$` permite recuperar o valor armazenado.

```bash
number=10

echo number
echo "$number"
```

Resultados:

```text
number
10
```

No primeiro comando, `number` é texto literal. No segundo, `$number` é expandido para seu valor.

As aspas duplas permitem a expansão e preservam o resultado como um único argumento.

As aspas simples impedem a expansão de variáveis pelo shell que interpreta o texto.

## Herança entre processos pai e filho

O Bash pode iniciar outro processo Bash:

```bash
number=10
export ORDER=100

bash -c 'echo "number=$number"; echo "ORDER=$ORDER"'
```

Resultado observado no laboratório:

```text
number=
ORDER=100
```

**Interpretação:**

- `number` não foi exportada e não foi herdada pelo Bash filho.
- `ORDER` foi exportada e ficou disponível ao Bash filho.
- `bash -c` inicia outro Bash para executar o comando informado.
- As aspas simples impedem que o Bash pai expanda as variáveis antes de passar o texto ao filho.

Essa demonstração foi essencial para compreender o escopo das variáveis.

## Variáveis importantes do ambiente

| Variável | Finalidade |
| --- | --- |
| `USER` | Identifica o usuário associado à sessão. |
| `HOME` | Indica o diretório pessoal do usuário. |
| `PATH` | Contém diretórios usados na procura por comandos executáveis. |
| `TZ` | Permite definir o fuso horário utilizado por programas que respeitam essa variável. |

### PATH

O `PATH` contém caminhos separados por `:`.

O comando:

```bash
which nano
```

pode ajudar a identificar o executável encontrado no caminho de pesquisa.

Alterar `PATH` incorretamente pode impedir que o shell encontre programas esperados ou fazer com que execute outro programa de mesmo nome.

### TZ

A variável `TZ` pode ser definida temporariamente para um comando:

```bash
TZ=Asia/Tokyo date
```

Isso consulta a data e a hora no fuso de Tóquio sem modificar permanentemente o fuso horário do Ubuntu.

## Substituição de comandos

A sintaxe `$(comando)` executa um comando e utiliza sua saída.

Exemplo:

```bash
nr_files="$(wc -l < /etc/passwd)"
```

O comando `wc -l` conta linhas. O operador `<` fornece o conteúdo do arquivo pela entrada padrão.

No laboratório, foram observados os resultados:

```bash
wc -l /etc/passwd
# 51 /etc/passwd

wc -l < /etc/passwd
# 51
```

A variável `nr_files` armazena o resultado da contagem naquele momento.

**Ponto importante:** a variável não acompanha automaticamente as mudanças no arquivo. Para atualizar o valor, é necessário executar novamente a atribuição.

## Exercícios guiados — LPI

### 1. Criar uma variável local

```bash
number=10
```

### 2. Criar uma variável de ambiente

```bash
export ORDER=100
```

### 3. Exibir nomes e valores

```bash
echo "number=$number"
echo "ORDER=$ORDER"
```

Resultado observado:

```text
number=10
ORDER=100
```

Esses comandos confirmam os valores no shell atual, mas não comprovam a herança.

### 4. Explicar o escopo

A variável `number` pertence ao shell atual e não é automaticamente herdada.

A variável `ORDER` foi exportada e pode ser herdada pelos processos filhos.

A diferença foi demonstrada com `bash -c`.

**Situação:** exercícios guiados concluídos e compreendidos.

## Exercícios exploratórios — LPI

### 1. Variável nr_files

Objetivo: armazenar a quantidade de linhas do arquivo `/etc/passwd`.

```bash
nr_files="$(wc -l < /etc/passwd)"
echo "$nr_files"
```

Contagem observada durante a prática: `51`.

O nome `nr_files` foi definido pelo exercício, embora a operação conte linhas, não arquivos.

**Situação:** praticado e compreendido.

### 2. Variável de ambiente ME

Objetivo: criar `ME` com o valor de `USER`.

```bash
export ME="$USER"
```

Teste com processo filho:

```bash
bash -c 'echo "ME=$ME"'
```

Resultado observado:

```text
ME=aluno
```

O teste confirmou que a variável exportada foi herdada pelo processo filho.

**Situação:** concluído.

### 3. Concatenar ME e HOME

Valor observado:

```bash
echo "$HOME"
# /home/aluno
```

Atribuição:

```bash
ME="$ME:$HOME"
```

Resultado observado:

```text
aluno:/home/aluno
```

O valor anterior de `ME` foi preservado e o conteúdo de `HOME` foi acrescentado utilizando `:` como separador.

Como `ME` já havia sido exportada, a nova atribuição preservou seu atributo de exportação.

**Situação:** concluído.

### 4. Variável today com outro fuso horário

```bash
today="$(TZ=Asia/Tokyo date)"
echo "$today"
```

Resultado observado:

```text
ter. 10 nov 2026 08:59:38 JST
```

A substituição de comandos armazenou a data e a hora de Tóquio no momento da execução.

Consultar `today` posteriormente não executa novamente o comando `date`.

**Situação:** concluído.

### 5. Variável today1 com a data do sistema

Objetivo: criar a variável `today1` utilizando a data do sistema Ubuntu.

**Situação:** pendente de execução e validação.

Não registrar como concluído antes da prática.

## Laboratório adicional — Diagnóstico de horário no Ubuntu

Durante o exercício com `date`, foi identificado um horário incorreto no Ubuntu.

### Diagnóstico inicial

O comando:

```bash
timedatectl
```

mostrou:

```text
Local time: sáb 2026-11-07 03:49:38 -03
RTC time: seg 2026-11-09 23:53:01
Time zone: America/Sao_Paulo
System clock synchronized: no
NTP service: active
```

O relógio do sistema estava atrasado, embora o RTC apresentasse uma data coerente.

### Identificação do serviço NTP

O serviço `systemd-timesyncd` não foi encontrado na instalação.

O comando:

```bash
systemctl status chrony --no-pager
```

confirmou que o serviço `chrony` estava ativo.

### Análise da sincronização

Foram utilizados:

```bash
chronyc tracking
chronyc sources -v
```

O `chronyc tracking` indicou um atraso de aproximadamente 234.190 segundos em relação à referência NTP.

O `chronyc sources -v` mostrou fontes NTP válidas, incluindo uma fonte selecionada com o indicador `^*`.

### Correção executada

```bash
sudo chronyc makestep
```

Resultado:

```text
200 OK
```

Após a execução, o `timedatectl` mostrou:

```text
Local time: seg 2026-11-09 20:57:54 -03
Universal time: seg 2026-11-09 23:57:54 UTC
Time zone: America/Sao_Paulo
System clock synchronized: no
NTP service: active
```

**Conclusão:** o horário do sistema foi corrigido, mas o indicador `System clock synchronized` ainda apresentava `no` na última verificação. Portanto, não há evidência suficiente para declarar a sincronização completamente validada.

### Aplicação profissional

Relógios incorretos podem dificultar a correlação de logs, eventos e alertas em ambientes NOC/SOC.

Esse diagnóstico foi um aprendizado complementar surgido durante a prática, sem alterar o escopo principal da Lição 2.

## Mapa mental

![Mapa mental — Variáveis no Bash](../imagens/Mapa%20Mental_%20Vari%C3%A1veis%20no%20Bash%20Linux.png)

**Observação:** a imagem resume os assuntos estudados. A documentação textual permanece como referência para explicações e evidências técnicas.

## Aprendizados e pontos de reforço

- Diferenciar variáveis locais de variáveis exportadas.
- Entender que o shell pai não transmite automaticamente todas as suas variáveis aos processos filhos.
- Distinguir texto literal de expansão com `$`.
- Compreender a diferença entre consultar uma variável e executar novamente um comando.
- Utilizar `$(...)` para capturar a saída de comandos.
- Entender o papel de `USER`, `HOME`, `PATH` e `TZ`.
- Evitar alterar configurações do sistema sem verificar primeiro o estado atual.
- Validar resultados antes de declarar exercícios ou diagnósticos concluídos.

## Próxima etapa de estudo

1. Finalizar o exercício exploratório 5.
2. Realizar uma revisão prática dos conceitos da Lição 2.
3. Validar a conclusão da lição antes de avançar no material oficial.

**Status geral:** Objetivo 2.1 em andamento. A Lição 2 ainda não foi declarada concluída.