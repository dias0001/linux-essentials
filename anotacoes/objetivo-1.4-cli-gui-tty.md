# Linux Essentials — Objetivo 1.4

## Conhecimentos de TIC e trabalho com Linux

**Certificação:** LPI Linux Essentials 010-160  
**Material de referência:** LPI Learning Materials 1.6 e CertBest  
**Status:** Em andamento

## 1. GUI e CLI

GUI (Graphical User Interface) é uma interface gráfica que permite interagir com o sistema utilizando janelas, ícones e menus.

Exemplos de ambientes gráficos Linux:

- GNOME
- KDE Plasma
- XFCE

CLI (Command-Line Interface) é uma interface baseada em comandos de texto.

A CLI é muito utilizada na administração de servidores, automação e acesso remoto.

## 2. Terminal e Bash

O terminal oferece uma interface para executar comandos.

O Bash é um shell que interpreta comandos e permite interagir com o sistema operacional.

Exemplos de comandos:

```bash
pwd
ls
tty
who
```

## 3. TTY e pseudoterminais

O Linux permite acessar terminais virtuais sem depender de um ambiente gráfico.

Exemplo de terminal virtual:

```text
/dev/tty3
```

Em sessões SSH interativas, normalmente são utilizados pseudoterminais.

Durante o laboratório, foram identificados:

```text
VS Code Remote SSH: /dev/pts/0
PuTTY:              /dev/pts/1
```

Os números identificam pseudoterminais distintos e não representam portas TCP.

## 4. Laboratório prático

**Ambiente:** Ubuntu Server 26.04.1 LTS  
**Hostname:** ubuntu-lab  
**IP:** 192.168.179.233

Foram abertas duas sessões SSH simultâneas utilizando VS Code e PuTTY.

Comando executado:

```bash
tty
```

O resultado demonstrou que cada sessão utilizava um pseudoterminal diferente.

Também foi executado:

```bash
who
```

Resultado observado:

```text
1000    seat0    2026-10-26 19:48
1000    tty2     2026-10-26 19:48
```

O comando `who` apresentou registros de sessões locais, mas não listou as duas conexões SSH observadas no laboratório.

## 5. Conclusão

O laboratório permitiu compreender que:

1. GUI e CLI são formas diferentes de interação com o Linux.
2. O Bash é um interpretador de comandos.
3. Terminais virtuais e pseudoterminais são conceitos distintos.
4. O Ubuntu permite múltiplas sessões SSH independentes.
5. O comando `tty` identifica o terminal associado à sessão atual.
6. O comando `who` consulta os registros de sessões de login.

**Próxima etapa:** continuar o Objetivo 1.4 com aplicações de desktop, apresentações e gerenciamento de projetos.
