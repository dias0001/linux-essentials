# Laboratório 02 — Usuários Linux, cut, grep e pipe

**Período:** 19 e 20/10/2026  
**Registro:** 20/10/2026, às 19h54 (horário de Brasília)  
**Ambiente:** Ubuntu Server — VM acessada pelo VS Code Remote SSH  
**Trilha:** Linux Essentials → LPIC-1  
**Referências de estudo:** prática própria, questão 1 do simulado DLTEC.

## Objetivo

Compreender como o Linux representa contas de usuários, distinguir arquivos de diretórios, interpretar caminhos e utilizar `grep`, `cut` e pipe para consultar informações do sistema.

## 1. Arquivo de treinamento

Criamos `usuarios.txt` com o conteúdo:

```text
ana:Ana Silva:Redes
bruno:Bruno Costa:seguranca
```

Cada linha representa um registro. O caractere `:` separa os campos. O espaço em `Ana Silva` não cria um novo campo.

Comandos praticados:

```bash
cat -n usuarios.txt
cut -d ':' -f 1 usuarios.txt
cut -d ':' -f 2 usuarios.txt
cut -d ':' -f 1,3 usuarios.txt
```

Aprendizado: `-f` seleciona campos de todas as linhas, não números de linhas. Sem `-d`, o `cut` usa TAB como delimitador padrão.

## 2. Criação de contas reais

No Ubuntu, criamos duas contas de laboratório:

```bash
sudo adduser ana
sudo adduser bruno
```

Informamos os nomes descritivos Ana Silva e Bruno Costa. As senhas foram configuradas apenas no sistema e não estão documentadas neste repositório.

Verificamos as contas em `/etc/passwd`:

```bash
grep '^ana:' /etc/passwd
grep '^bruno:' /etc/passwd
```

Campos observados:

| Campo | Informação | Ana | Bruno |
|---|---|---|---|
| 1 | Login | ana | bruno |
| 2 | Indicador de senha | x | x |
| 3 | UID | 1001 | 1002 |
| 4 | GID | 1001 | 1002 |
| 5 | GECOS | Ana Silva,,, | Bruno Costa,,, |
| 6 | Home | /home/ana | /home/bruno |
| 7 | Shell | /bin/bash | /bin/bash |

Os valores são os observados nesta VM. O campo `x` não é a senha em texto claro.

## 3. Arquivos, diretórios e caminhos

Experimentamos navegar até `/etc/passwd` com `cd`, mas o comando falhou porque `passwd` é um arquivo comum, não um diretório.

```bash
cd /etc
ls -ld passwd ssh
```

Na saída de `ls -l`, o primeiro caractere `-` indica arquivo comum e `d` indica diretório.

Compreendemos também:

- `/etc/passwd`: caminho absoluto, independente do diretório atual.
- `passwd`: caminho relativo, encontrado diretamente quando estamos em `/etc`.
- `cd` muda de diretório, não abre arquivos comuns.

## 4. grep, cut e pipe

Usamos `grep` para localizar registros e `cut` para extrair campos.

```bash
grep -E '^(ana|bruno):' /etc/passwd
```

Depois combinamos os comandos:

```bash
grep -E '^(ana|bruno):' /etc/passwd | cut -d ':' -f 1,5
```

Resultado observado:

```text
ana:Ana Silva,,,
bruno:Bruno Costa,,,
```

O pipe `|` fora das aspas conecta a saída padrão do `grep` à entrada padrão do `cut`. O `|` dentro da expressão regular `(ana|bruno)` significa OU, pois usamos `grep -E`.

## 5. Questão 1 — Simulado DLTEC

**Tema:** extrair login e nome descritivo das contas listadas em `/etc/passwd`.

Resposta correta identificada: alternativa C.

```bash
cut -d: -f1,5 /etc/passwd
```

Explicação:

- `-d:` define os dois-pontos como delimitador.
- `-f1,5` seleciona o login (campo 1) e o GECOS (campo 5).
- `/etc/passwd` é o arquivo consultado.

A alternativa sem `-d:` não atende ao formato do arquivo, pois o delimitador padrão do `cut` é TAB.

## 6. Aplicação em Blue Team

A consulta de contas é um fundamento útil para investigar usuários em sistemas Linux. Em uma investigação real, seria necessário também verificar permissões, grupos, logs e a origem das alterações; a existência da conta, isoladamente, não comprova atividade maliciosa.

## 7. Aprendizados e próximos passos

**Praticado:** criação de usuários, leitura de `/etc/passwd`, campos e delimitadores, `grep`, `cut`, pipe, navegação, caminhos absolutos e relativos, interpretação de erros e identificação de arquivos e diretórios.

**Revisar:** opções de `cut`, padrões do `grep` e uso de pipe sem consultar exemplos.

**Próximo passo:** continuar a progressão do Linux Essentials e aplicar os comandos em novos exercícios.

---

**Fontes:** questão 1 do simulado DLTEC e prática realizada na VM Ubuntu.
