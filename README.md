
# 🐧 Linux Estudos | Linux Essentials → LPIC-1

Repositório pessoal dedicado ao aprendizado prático de Linux, com foco nos fundamentos do sistema operacional, administração de sistemas e preparação para as certificações **Linux Essentials** e, futuramente, **LPIC-1**.

## 🎯 Objetivo

Construir uma base sólida em Linux, combinando teoria, prática no terminal, resolução de problemas e documentação dos laboratórios.

Os conhecimentos também contribuem para minha formação em redes de computadores, infraestrutura e segurança defensiva (**Blue Team**).

O projeto segue uma abordagem progressiva: **estudar, compreender, praticar, documentar e revisar**.

## 💻 Ambiente de laboratório

- **Sistema operacional:** Ubuntu 26.04.1 LTS em máquina virtual
- **Virtualização:** VMware Workstation
- **Acesso local:** ambiente gráfico do Ubuntu
- **Acesso remoto:** SSH
- **Ferramentas de acesso:** Visual Studio Code Remote SSH e PuTTY
- **Shell:** Bash
- **Versionamento:** Git e GitHub
- **Documentação:** Markdown

## 📚 Anotações

| Tema | Material | Status |
|---|---|---|
| Linux Essentials — Objetivo 1.1 | [Introdução ao Linux](anotacoes/objetivo-1.1-linux.md) | ✅ Estudado |
| Linux Essentials — Objetivo 1.2 | [Aplicativos Open Source](anotacoes/objetivo-1.2-aplicativos-open-source.md) | ✅ Estudado |
| Linux Essentials — Objetivo 1.3 | [Software Open Source e Licenças](anotacoes/objetivo-1.3-licencas-open-source.md) | ✅ Estudado |
| Linux Essentials — Objetivo 1.4 | [GUI, CLI, Bash e TTY](anotacoes/objetivo-1.4-cli-gui-tty.md) | 🔄 Em andamento |
| Linux Essentials — Objetivo 1.4 | [PATH, caminhos e links simbólicos](anotacoes/objetivo-1.4-path-links-simbolicos.md) | ✅ Laboratório realizado |

## 🧪 Laboratórios práticos

| Laboratório | Conteúdo |
|---|---|
| 01 — Bash e Git | [Primeiros comandos e versionamento](laboratorios/laboratorio-01-bash-git.md) |
| 02 — Usuários, grep, cut e pipe | [Criação de contas e consulta ao /etc/passwd](laboratorios/laboratorio-02-usuarios-cut/README.md) |
| 03 — Nginx | [Instalação, gerenciamento e validação de servidor web](laboratorios/laboratorio-03-nginx/README.md) |
| Prática complementar — GUI, PATH e links simbólicos | [Investigação do LibreOffice, Snap e caminhos lógicos e físicos](anotacoes/objetivo-1.4-path-links-simbolicos.md) |

## 🔍 Conhecimentos praticados

### Fundamentos Linux

- Navegação no sistema de arquivos Linux.
- Diferença entre arquivos e diretórios.
- Caminhos absolutos e relativos.
- Interpretação de permissões e tipos de arquivos com `ls -l`.
- Identificação de links simbólicos.
- Consulta ao destino de links com `readlink`.
- Diferença entre caminhos lógicos e físicos utilizando `pwd -L` e `pwd -P`.
- Criação e consulta de contas de usuários.
- Estrutura do arquivo `/etc/passwd`.
- Processamento de texto com `grep` e `cut`.
- Encadeamento de comandos com pipe (`|`).
- Interpretação de mensagens de erro.

### Gerenciamento de pacotes e serviços

- Atualização de índices de pacotes com APT.
- Instalação, atualização e remoção de pacotes.
- Gerenciamento básico de serviços com `systemctl`.
- Instalação e configuração inicial do Nginx.
- Validação de acesso HTTP ao servidor web.
- Observação da estrutura de instalação do LibreOffice via Snap.
- Identificação de revisões de aplicativos Snap e do link simbólico `current`.

### Terminal, aplicativos e acesso remoto

- Diferenças entre GUI e CLI.
- Utilização do Bash.
- Localização de comandos com `command -v`.
- Consulta à variável de ambiente `$PATH`.
- Inicialização do LibreOffice Impress pelo terminal.
- Observação do comportamento de aplicações gráficas em sessões locais e SSH.
- Interrupção de comandos com `Ctrl+C`.
- Acesso remoto ao Linux utilizando SSH.
- Utilização de múltiplas sessões SSH.
- Identificação de pseudoterminais com `tty`.
- Consulta de sessões de login com `who`.
- Diferença entre terminais virtuais e pseudoterminais.

### Documentação e versionamento

- Criação de arquivos Markdown.
- Organização de anotações e laboratórios.
- Controle de versões utilizando Git.
- Publicação de documentação no GitHub.
- Sincronização de alterações entre GitHub e Ubuntu.
- Utilização dos comandos `git status`, `git add`, `git commit`, `git push` e `git pull`.
- Registro de procedimentos e resultados observados em laboratório.

## 🔬 Destaque — Investigação prática do sistema Linux

Durante o estudo do **Objetivo 1.4**, uma atividade inicialmente voltada à execução do LibreOffice Impress pelo terminal evoluiu para uma investigação sobre como o Linux localiza e executa aplicativos.

O laboratório começou com:

```bash
command -v libreoffice
```

Resultado:

```text
/snap/bin/libreoffice
```

A investigação continuou com a análise do diretório `/snap/bin`, onde foi identificado o link simbólico:

```text
/snap/bin/libreoffice -> /usr/bin/snap
```

Também foi analisada a estrutura de revisões do LibreOffice:

```text
/snap/libreoffice/
├── 377/
├── 379/
└── current -> 379
```

Por fim, foi comprovada a diferença entre caminhos lógicos e físicos:

```bash
pwd -L
# /snap/libreoffice/current

pwd -P
# /snap/libreoffice/379
```

**Principal aprendizado:** compreender o funcionamento do sistema exige observar os resultados dos comandos, formular hipóteses e investigar os caminhos utilizados pelo Linux.

📖 **Documentação completa:** [Laboratório — PATH e links simbólicos](anotacoes/objetivo-1.4-path-links-simbolicos.md)

## 🛡️ Aplicação em Blue Team

Os laboratórios ajudam a desenvolver fundamentos úteis para:

- Investigação de sistemas Linux.
- Análise de contas e usuários.
- Identificação de serviços e conexões.
- Administração remota de servidores.
- Interpretação de informações do sistema operacional.
- Identificação de arquivos, diretórios e links simbólicos.
- Investigação de caminhos utilizados por aplicativos e comandos.

Essas habilidades constituem uma base para estudos futuros de monitoramento, segurança de redes e resposta a incidentes.

## 📖 Metodologia de estudo

O projeto utiliza como referência principal o material oficial **LPI Linux Essentials 010-160, versão 1.6**, complementado pelas aulas da CertBest.

Cada objetivo é estudado progressivamente, com exercícios e laboratórios quando aplicáveis.

Os registros publicados representam atividades efetivamente estudadas ou executadas.

O objetivo não é apenas memorizar comandos, mas desenvolver a capacidade de compreender, investigar e solucionar problemas.

## 🚀 Próximos passos

1. Continuar o Objetivo 1.4 do Linux Essentials.
2. Avançar pelos demais objetivos da certificação 010-160.
3. Revisar os fundamentos e realizar simulados.
4. Preparar-se para o exame Linux Essentials.
5. Após essa etapa, iniciar os estudos direcionados ao LPIC-1.
6. Aprofundar o uso do Git progressivamente, aplicando-o à documentação e aos futuros projetos de automação.

---

**Início do projeto:** outubro de 2026  
**Última atualização:** 27/10/2026

*Estudar. Compreender. Praticar. Documentar. Compartilhar.*
