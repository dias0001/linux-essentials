# Laboratório 03 — Servidor Web Nginx

**Projeto:** Linux Essentials 010-160  
**Ambiente:** Ubuntu 26.04.1 LTS  
**Data:** 24/10/2026  
**Objetivo:** Aprender a instalar, verificar, remover e personalizar um servidor web Nginx.

## 1. Instalação e gerenciamento de pacotes

Comandos praticados:

```bash
sudo apt update
sudo apt install nginx
apt list --installed nginx
sudo apt remove nginx
```

Aprendizado: o APT gerencia pacotes de software no Ubuntu, incluindo instalação, atualização e remoção.

## 2. Gerenciamento do serviço

```bash
systemctl status nginx
sudo systemctl restart nginx
sudo systemctl enable nginx
```

Aprendizado: verificamos o estado do serviço, reiniciamos o Nginx e confirmamos sua configuração de inicialização automática.

## 3. Arquivos e permissões

```bash
ls -l /var/www/html/
cat /var/www/html/index.nginx-debian.html
```

Identificamos as permissões `rw-r--r--` e o proprietário `root`.

Realizamos um backup do HTML original antes de modificá-lo.

## 4. Personalização da página

Editamos o arquivo HTML utilizando Nano e alteramos o título para:

**Linux Essentials | Blue Team Lab**

Validamos a página no Firefox pelo endereço:

`http://127.0.0.1/`

A alteração do HTML foi exibida sem reiniciar o Nginx.

## 5. Observações e dificuldades

- O comando `curl` não estava instalado.
- Aprendemos a diferença entre caminhos absolutos e relativos.
- Entendemos por que algumas operações exigem `sudo`.
- Confirmamos a diferença entre remover pacotes e gerenciar serviços.
- Criamos uma cópia da página HTML para versionamento no GitHub.

## 6. Próximas etapas

- Versionar o laboratório com Git.
- Enviar os arquivos ao GitHub.
- Continuar a preparação para o Linux Essentials 010-160.

**Laboratório realizado com acompanhamento do ChatGPT, com execução e verificação dos comandos no Ubuntu.**
