# Linux Essentials 010-160 — Objetivo 1.4
## Laboratório: GUI, CLI, PATH e links simbólicos

**Ambiente:** Ubuntu Linux — VMware Workstation  
**Usuário:** aluno  
**Terminal:** GNOME Terminal e VS Code Remote SSH  
**Data:** 27/10/2026  
**Status:** Laboratório realizado e validado

---

## 1. Objetivo

Investigar como o Linux localiza e executa aplicativos, compreender a diferença entre caminhos absolutos e relativos e identificar links simbólicos no sistema de arquivos.

O laboratório surgiu durante o estudo sobre aplicações gráficas (GUI) e interfaces de linha de comando (CLI).

O aplicativo utilizado foi o LibreOffice Impress, instalado no Ubuntu por meio do Snap.

## 2. Investigação inicial — Localizando o LibreOffice

Comando executado:

```bash
command -v libreoffice
```

Resultado:

```text
/snap/bin/libreoffice
```

O comando `command -v` permitiu identificar o caminho utilizado pelo shell para localizar o aplicativo.

A variável de ambiente `PATH` contém diretórios nos quais o shell procura comandos executáveis.

Para visualizar seu conteúdo:

```bash
echo $PATH
```

Durante a investigação, identificamos `/snap/bin` entre os diretórios disponíveis no `PATH`.

**Aprendizado:** não é necessário informar o caminho absoluto de um programa quando seu comando pode ser localizado pelo shell através do `PATH`.

## 3. Executando uma aplicação gráfica pela CLI

No terminal gráfico do Ubuntu:

```bash
libreoffice --impress
```

**Resultado observado:** o LibreOffice Impress abriu sua interface gráfica.

O terminal apresentou avisos relacionados a componentes gráficos, mas eles não impediram a abertura do aplicativo.

A experiência demonstrou que uma aplicação GUI pode ser iniciada por um comando CLI.

### Comparação com o acesso SSH

O mesmo comando foi executado em um terminal do VS Code conectado ao Ubuntu por SSH.

Nessa sessão, não foi observada a abertura de uma janela no Windows, e o comando permaneceu ocupado até ser interrompido com `Ctrl+C`.

Isso mostrou que encontrar um executável no `PATH` não garante que uma sessão tenha acesso a um ambiente gráfico.

**Observação:** a causa específica do comportamento na sessão SSH não foi investigada até sua conclusão.

## 4. Caminhos absolutos e relativos

Durante a investigação, foi executado:

```bash
cd snap/bin
```

O comando retornou um erro porque o diretório não existia dentro do caminho de trabalho naquele momento.

O acesso correto foi realizado com:

```bash
cd /snap/bin
```

A diferença está na barra inicial.

| Caminho | Tipo | Interpretação |
|---|---|---|
| `/snap/bin` | Absoluto | Começa na raiz do sistema |
| `snap/bin` | Relativo | Começa no diretório atual |
| `../` | Relativo | Referência ao diretório pai |
| `./` | Relativo | Referência ao diretório atual |

**Aprendizado:** conhecer o diretório atual é essencial para interpretar caminhos relativos e evitar erros na execução de comandos.

## 5. Investigando o diretório /snap/bin

Comando executado:

```bash
ls -l /snap/bin
```

Entre os resultados, foi identificado:

```text
libreoffice -> /usr/bin/snap
```

Essa saída revelou que `/snap/bin/libreoffice` não era o executável principal do LibreOffice, mas um link simbólico.

Para investigar especificamente o link:

```bash
ls -l /snap/bin/libreoffice
```

Resultado:

```text
lrwxrwxrwx 1 root root 13 Oct 22 19:17 /snap/bin/libreoffice -> /usr/bin/snap
```

O primeiro caractere, `l`, identifica um link simbólico.

A seta `->` mostra seu destino.

Para consultar diretamente esse destino:

```bash
readlink /snap/bin/libreoffice
```

Resultado:

```text
/usr/bin/snap
```

**Aprendizado:** um link simbólico funciona como uma referência a outro caminho. No caso do LibreOffice instalado via Snap, o link participa do mecanismo utilizado para iniciar o aplicativo.

## 6. Identificando revisões do LibreOffice

Comando executado:

```bash
ls -l /snap/libreoffice
```

Resultado observado:

```text
drwxr-xr-x ... 377
drwxr-xr-x ... 379
lrwxrwxrwx ... current -> 379
```

Foram identificadas duas revisões do pacote LibreOffice: `377` e `379`.

O link simbólico `current` apontava para a revisão `379`.

A presença de revisões diferentes está relacionada ao mecanismo de atualização e retenção de revisões do Snap.

Para verificar o destino do link:

```bash
readlink /snap/libreoffice/current
```

Resultado:

```text
379
```

Nesse caso, o destino do link é relativo.

Portanto:

```text
/snap/libreoffice/current
           |
           v
/snap/libreoffice/379
```

O link `current` permite acessar a revisão ativa sem precisar informar diretamente seu número.

## 7. Caminho lógico versus caminho físico

Acessamos o diretório:

```bash
cd /snap/libreoffice/current
```

Em seguida:

```bash
pwd
```

Resultado:

```text
/snap/libreoffice/current
```

Depois:

```bash
pwd -P
```

Resultado:

```text
/snap/libreoffice/379
```

Finalmente:

```bash
pwd -L
```

Resultado:

```text
/snap/libreoffice/current
```

### Interpretação

| Comando | Resultado | Significado |
|---|---|---|
| `pwd -L` | `/snap/libreoffice/current` | Caminho lógico |
| `pwd -P` | `/snap/libreoffice/379` | Caminho físico |
| `readlink` | `379` | Destino do link simbólico |

A opção `-L` preserva o caminho lógico.

A opção `-P` resolve os links simbólicos presentes no caminho.

## 8. Identificando tipos de arquivos com ls -l

O primeiro caractere da listagem longa indica o tipo de arquivo.

| Caractere | Significado |
|---|---|
| `-` | Arquivo comum |
| `d` | Diretório |
| `l` | Link simbólico |

Exemplos:

```text
drwxr-xr-x ... 379
lrwxrwxrwx ... current -> 379
```

O diretório `379` é identificado pela letra `d`.

O link `current` é identificado pela letra `l`.

## 9. Comandos utilizados

```bash
command -v libreoffice
echo $PATH
libreoffice --impress

cd /snap/bin
ls -l

ls -l /snap/bin/libreoffice
readlink /snap/bin/libreoffice

ls -l /snap/libreoffice
readlink /snap/libreoffice/current

cd /snap/libreoffice/current
pwd
pwd -L
pwd -P
```

## 10. Conclusão e aprendizado

Este laboratório começou com a execução de um aplicativo gráfico pelo terminal e evoluiu para uma investigação sobre a organização do sistema de arquivos Linux.

Durante a atividade, foram praticados conceitos fundamentais:

- Localização de comandos por meio do `PATH`.
- Diferença entre aplicativos GUI e CLI.
- Interpretação de caminhos absolutos e relativos.
- Identificação de links simbólicos.
- Utilização de `readlink`.
- Interpretação de resultados do `ls -l`.
- Diferença entre caminhos lógicos e físicos.
- Observação do comportamento de aplicativos gráficos em sessões locais e SSH.

O principal aprendizado foi compreender que **executar comandos é apenas parte do trabalho: interpretar seus resultados e investigar o funcionamento do sistema é essencial para desenvolver autonomia técnica.**

---

**Projeto:** Linux Essentials 010-160  
**Metodologia:** Estudar. Compreender. Praticar. Documentar. Compartilhar.
