Linux Essentials 010-160 — Objetivo 1.4
Anotações de estudo — Segurança, privacidade e criptografia
Material: Linux Essentials, versão 1.6 — LPI
Status: Em andamento — leitura teórica realizada; exercícios guiados pendentes.
Este README registra apenas o conteúdo teórico estudado. Não documenta laboratórios executados nem atividades futuras.

1. Linux na indústria e na nuvem
- Virtualização: permite executar máquinas virtuais em um computador físico, utilizando um hipervisor, como KVM, Xen ou VirtualBox.
- Computação em nuvem: fornece recursos computacionais sob demanda.
- IaaS: infraestrutura virtual, como servidores, redes e armazenamento.
- PaaS: plataforma para desenvolver e executar aplicações.
- SaaS: software disponibilizado como serviço.
- OpenStack: conjunto de componentes open source para gerenciar infraestrutura de nuvem, incluindo recursos de computação, rede e armazenamento.
2. Privacidade na Internet
- Cookies primários (first-party): podem manter sessões e preferências de um site.
- Cookies de terceiros (third-party): podem ser utilizados para rastreamento entre sites.
- Do Not Track (DNT): sinaliza uma preferência de não rastreamento, mas não obriga o site a respeitá-la.
- Navegação privada/anônima: reduz registros locais da sessão; não torna o usuário anônimo perante sites, redes ou provedores.
- HTTPS/TLS: protege dados transmitidos entre cliente e servidor, mas não elimina todos os riscos de privacidade.
- Computadores públicos: podem conter programas como keyloggers, capazes de capturar informações digitadas antes de serem protegidas pela transmissão criptografada.
3. Escolha a senha certa
- Usar senhas fortes, longas e exclusivas para cada serviço.
- Evitar reutilizar senhas: um vazamento pode permitir tentativas de acesso a outras contas (credential stuffing).
- Um gerenciador de senhas mantém credenciais em um cofre criptografado.
- KeePass: gerencia um banco de dados criptografado que pode ser armazenado localmente.
- Bitwarden: oferece cofre criptografado e sincronização entre dispositivos.
- A senha mestra deve ser forte, exclusiva e protegida.
- Backup e disponibilidade: conhecer a senha mestra não recupera um banco de dados local perdido se não existir outra cópia válida.
4. Criptografia e TLS
- Criptografia: transforma informações legíveis em dados protegidos, que dependem da chave apropriada para serem recuperados.
- TLS (Transport Layer Security): protocolo utilizado para proteger comunicações na rede; é o sucessor do SSL.
- HTTPS: utiliza TLS para proteger a comunicação HTTP e permite validar a identidade do servidor por meio de certificados digitais, conforme a confiança estabelecida.
5. Criptografia de arquivos e emails com GnuPG
GnuPG (GNU Privacy Guard) é uma implementação open source do padrão OpenPGP. Pode ser utilizado para criptografar, descriptografar e assinar mensagens e arquivos.
Chaves pública e privada
- Chave pública: pode ser compartilhada.
- Chave privada: deve permanecer secreta e protegida.
- Para enviar um arquivo confidencial a alguém, utiliza-se a chave pública do destinatário para criptografá-lo; a chave privada correspondente permite a descriptografia.
- Para assinar digitalmente, o autor usa sua chave privada; a assinatura é verificada com a chave pública do autor.
Integridade e assinatura digital
- Um hash criptográfico representa o conteúdo de um arquivo e ajuda a detectar modificações.
- Uma alteração de apenas uma letra pode invalidar a assinatura digital.
- Tamanho do arquivo não comprova integridade: dois arquivos podem ter o mesmo tamanho e conteúdos diferentes.
- Uma assinatura válida permite verificar a integridade e a relação com a chave que assinou; para associá-la a uma pessoa, é preciso confiar na identidade vinculada à chave pública.
Conceitos relacionados
- Confidencialidade: impedir leitura não autorizada.
- Integridade: detectar alterações indevidas.
- Autenticidade: verificar a origem declarada de uma informação.
6. Criptografia de disco
O material apresenta duas abordagens principais.
Criptografia empilhada no sistema de arquivos
- Funciona sobre um sistema de arquivos existente.
- Arquivos e diretórios são criptografados antes de serem gravados e descriptografados quando acessados pela camada apropriada.
- Os dados criptografados continuam armazenados como arquivos no sistema de arquivos hospedeiro.
- EncFS: ferramenta citada pelo material como exemplo desse método, sem exigir privilégios de root para seu uso típico.
Criptografia de dispositivos de bloco
- Funciona abaixo da camada do sistema de arquivos.
- Protege os dados gravados no dispositivo de bloco, incluindo estruturas do sistema de arquivos contidas no volume criptografado.
- Sem a chave adequada, os blocos parecem dados aleatórios e não revelam diretamente a estrutura do sistema de arquivos.
- dm-crypt: mecanismo de criptografia de bloco integrado ao kernel Linux.
- LUKS (Linux Unified Key Setup): formato/especificação usado com ferramentas de criptografia de bloco, normalmente em conjunto com dm-crypt.
VeraCrypt
- Ferramenta de criptografia de volumes e contêineres.
- Permite utilizar dados criptografados em diferentes plataformas, como Linux, Windows e macOS.
- É apresentado no material como sucessor do TrueCrypt.
7. Situação do estudo
- [x] Leitura e discussão: senhas e gerenciadores de senhas.
- [x] Leitura e discussão: TLS.
- [x] Leitura e discussão: GnuPG, chaves e assinaturas digitais.
- [x] Leitura: criptografia de disco, EncFS, dm-crypt/LUKS e VeraCrypt.
- [ ] Exercícios guiados do Objetivo 1.4.
- [ ] Revisão final das anotações.
Referência: Linux Essentials (Versão 1.6), LPI Learning Materials, Objetivo 1.4, especialmente páginas 58–64.
Princípio de estudo: Estudar. Compreender. Praticar. Documentar. Compartilhar.
