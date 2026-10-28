# 🧪 Laboratório 04 — Gerenciamento de Pacotes APT e Planner

**Projeto:** Linux Estudos  
**Certificação:** Linux Essentials 010-160  
**Contexto:** Objetivo 1.4 — Conhecimentos de TIC e o trabalho com Linux  
**Ambiente:** Ubuntu 26.04.1 LTS — VMware Workstation  
**Data:** 27/10/2026

## 🎯 Objetivo

Investigar a disponibilidade de aplicativos Linux, consultar informações sobre pacotes, simular uma instalação e instalar um aplicativo de gerenciamento de projetos.

A atividade surgiu durante o estudo de ferramentas de produtividade e gerenciamento de projetos no Linux.

## 1. Investigação inicial — ProjectLibre

O primeiro aplicativo pesquisado foi o ProjectLibre.

```bash
command -v projectlibre
man projectlibre
apt search projectlibre
apt show projectlibre
```

### Resultados observados

- `command -v` não encontrou o comando no `PATH`.
- `man` informou que não havia uma entrada de manual disponível.
- `apt search` não apresentou correspondências.
- `apt show` informou que o pacote não foi encontrado.

**Conclusão:** o ProjectLibre não foi localizado como comando nem como pacote disponível nos índices APT configurados naquele momento.

A ausência de resultados não significa que o aplicativo não exista para Linux.

## 2. Pesquisa de alternativas

Foi realizada uma pesquisa por funcionalidade:

```bash
apt search gantt
```

Entre os resultados, foi identificado:

```text
planner/resolute 0.14.92-1.1build2 amd64
  project management application
```

O pacote `planner` foi selecionado para investigação por oferecer funcionalidades de gerenciamento de projetos e gráficos de Gantt.

## 3. Utilização de head, tail e pipe

Para visualizar partes da saída da pesquisa, foram executados:

```bash
apt search gantt | head -n 10
apt search gantt | tail -n 10
```

### Conceitos praticados

- `|` encaminha a saída padrão de um comando para a entrada padrão de outro.
- `head -n 10` mostra as dez primeiras linhas recebidas.
- `tail -n 10` mostra as dez últimas linhas recebidas.

Durante os testes, o APT apresentou o aviso:

```text
WARNING: apt does not have a stable CLI interface.
Use with caution in scripts.
```

O aviso informa que a interface de linha de comando do `apt` não possui formato de saída estável para automações.

Também foi observado que mensagens enviadas para `stderr` podem aparecer no terminal mesmo quando a saída padrão é encaminhada por um pipe.

## 4. Consulta de informações do pacote

Comando:

```bash
apt show planner
```

### Informações identificadas

| Campo | Valor |
|---|---|
| Pacote | `planner` |
| Versão | `0.14.92-1.1build2` |
| Arquitetura | `amd64` |
| Origem | Ubuntu |
| Repositório | `universe` |
| Categoria | `gnome` |
| Descrição | Aplicativo de gerenciamento de projetos |

A descrição informou que o Planner oferece suporte a gráficos de Gantt e alocação de recursos.

## 5. Verificação da instalação

Foi executado:

```bash
apt list --installed planner
```

Nenhuma entrada correspondente ao pacote instalado foi apresentada.

A verificação indicou que o Planner ainda não estava instalado por meio do gerenciamento de pacotes APT.

## 6. Simulação da instalação

Antes de modificar o sistema, foi executado:

```bash
apt install --simulate planner
```

### Resumo apresentado

```text
Atualizando: 0
Instalando: 8
Removendo: 0
Não atualizando: 4
```

A simulação indicou a instalação do Planner e de sete pacotes adicionais, entre dependências e recomendações.

Foram observadas as indicações:

- `Inst`: instalação prevista de um pacote.
- `Conf`: configuração prevista de um pacote.

**Conclusão:** a simulação permitiu analisar as operações planejadas sem instalar ou remover pacotes.

## 7. Instalação real do Planner

Após a análise, foi executado:

```bash
sudo apt install planner
```

O APT solicitou autenticação e apresentou o resumo da operação.

### Resultado

```text
Atualizando: 0
Instalando: 8
Removendo: 0
Não atualizando: 4
```

Foram baixados aproximadamente 2,6 MB de pacotes, com previsão de utilização adicional de 15,7 MB em disco.

A instalação passou pelas etapas de download, desempacotamento, configuração e processamento de gatilhos.

A saída final incluiu:

```text
Configurando planner (0.14.92-1.1build2) ...
```

O comando foi concluído sem erros aparentes.

### Observação sobre autoremove

Durante a operação, o APT apresentou uma lista de pacotes instalados automaticamente que não eram mais considerados necessários.

**O comando `apt autoremove` não foi executado.**

A remoção desses pacotes não fazia parte do objetivo do laboratório.

## 8. Localização e execução do aplicativo

Após a instalação, foi executado:

```bash
command -v planner
```

Resultado:

```text
/usr/bin/planner
```

Em seguida, no terminal gráfico do Ubuntu:

```bash
planner
```

A interface gráfica do Planner foi aberta com sucesso.

### Comparação com o LibreOffice

Durante os estudos do Objetivo 1.4, também havia sido investigado o LibreOffice.

| Aplicativo | Caminho identificado | Gerenciamento |
|---|---|---|
| LibreOffice | `/snap/bin/libreoffice` | Snap |
| Planner | `/usr/bin/planner` | APT |

A comparação permitiu observar diferentes formas de distribuição e execução de aplicativos Linux.

## 9. Utilização do gráfico de Gantt

Na interface do Planner, foram exploradas as opções:

- Gantt;
- Tarefas;
- Recursos;
- Utilização de recursos.

Foram criadas atividades de exemplo relacionadas ao planejamento de uma rede corporativa:

1. Levantamento dos requisitos.
2. Planejamento do endereçamento IP.

As tarefas foram inicialmente apresentadas no mesmo período, sem dependências configuradas.

Também foi investigada a aba **Predecessores**, utilizada para estabelecer relações entre atividades.

Posteriormente, surgiu a proposta de utilizar o Planner para acompanhar o cronograma de preparação para o Linux Essentials.

**O planejamento completo da certificação ficou reservado para uma atividade futura.**

## 10. Conceitos consolidados

Este laboratório permitiu praticar:

- Pesquisa de aplicativos e pacotes.
- Localização de comandos com `command -v`.
- Consulta de páginas de manual.
- Pesquisa de pacotes com `apt search`.
- Consulta de metadados com `apt show`.
- Utilização de pipes, `head` e `tail`.
- Verificação de pacotes instalados.
- Simulação de instalação com APT.
- Interpretação de dependências e recomendações.
- Instalação de aplicativos com `sudo apt install`.
- Execução de aplicações gráficas pelo terminal.
- Introdução ao gerenciamento de projetos e gráficos de Gantt.

## 11. Conclusão

A atividade começou com a tentativa de localizar o ProjectLibre e evoluiu para uma investigação sobre pesquisa, instalação e execução de aplicativos Linux.

A utilização do APT permitiu compreender a importância de consultar informações e simular alterações antes de instalar um pacote.

O Planner foi instalado e executado com sucesso, permitindo relacionar o estudo teórico do Linux Essentials à utilização prática de um aplicativo gráfico.

**Metodologia aplicada:** estudar, investigar, executar, interpretar, documentar e revisar.

---

*Laboratório realizado como parte do projeto pessoal Linux Estudos.*
