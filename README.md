# guilherme-lorran2
configuração de diversos sistemas operacionais e serviços em um ambiente de rede.
🔧 1. Inicializar o repositório local (caso ainda não tenha feito)
No terminal ou prompt de comando:

bash
Copiar
Editar
cd caminho/do/seu/projeto
git init
📄 2. Adicionar os arquivos e fazer o commit inicial
bash
Copiar
Editar
git add .
git commit -m "Commit inicial"
🌐 3. Criar um repositório no GitHub
Acesse github.com

Clique em "New repository"

Escolha nome, visibilidade (público ou privado) e crie o repositório

🔗 4. Conectar o repositório local ao GitHub
Copie o link HTTPS do repositório criado (ex: https://github.com/usuario/nome-repo.git) e rode:

bash
Copiar
Editar
git remote add origin https://github.com/usuario/nome-repo.git
Se já houver um origin, use:

bash
Copiar
Editar
git remote set-url origin https://github.com/usuario/nome-repo.git
🚚 5. Enviar os arquivos para o GitHub
bash
Copiar
Editar
git push -u origin master
Ou, se estiver usando a branch main:

bash
Copiar
Editar
git push -u origin main
🔄 Atualizando o projeto futuramente
Depois de fazer mudanças:

bash
Copiar
Editar
git add .
git commit -m "Mensagem das alterações"
git push
# 📘 Passo a Passo: Instalação do Windows Server

Guia simples e direto para instalar o **Windows Server** (ex: 2022).

## ✅ Pré-requisitos
- 💽 ISO do Windows Server (disponível no site da Microsoft)
- 🔌 Pendrive bootável (mínimo 8 GB, pode usar o [Rufus](https://rufus.ie/))
- 💻 Hardware compatível:
  - CPU 64 bits, 1.4 GHz+
  - 2 GB RAM
  - 32 GB de espaço em disco

---

## 🛠️ Etapas de Instalação

### 1. Criar Pendrive Bootável
- Abra o **Rufus**
- Selecione o pendrive
- Escolha a ISO do Windows Server
- Clique em `Iniciar`

### 2. Configurar Boot pelo Pendrive
- Reinicie o PC
- Acesse a BIOS/UEFI (`Del`, `F2`, `F12` ou `Esc`)
- Defina o boot pelo pendrive
- Salve e reinicie

### 3. Iniciar a Instalação
- Selecione idioma e teclado
- Clique em `Avançar` > `Instalar agora`

### 4. Selecionar Edição
- Escolha a edição desejada:
  - `Standard` ou `Datacenter`
  - Com ou sem GUI (interface gráfica)

### 5. Aceitar Termos
- Marque a caixa de aceite
- Clique em `Avançar`

### 6. Tipo de Instalação
- Escolha: `Personalizada (avançado)`

### 7. Selecionar Disco/Partição
- Selecione onde instalar
- Crie/apague partições se necessário
- Clique em `Avançar`

### 8. Processo de Instalação
- Aguarde a cópia dos arquivos
- O sistema reiniciará automaticamente

### 9. Definir Senha de Administrador
- Crie uma senha forte
- Clique em `Concluir`

### 10. Fazer Login
- Pressione `Ctrl + Alt + Del`
- Login com:
  - Usuário: `Administrator`
  - Senha: a que você definiu

---

## 🔧 Pós-instalação (opcional)
- Configurar IP fixo
- Ativar Windows
- Instalar funções como:
  - Active Directory (AD DS)
  - DNS
  - DHCP
  - Servidor de Arquivos

---

> 💡 Contribuições são bem-vindas! Sinta-se à vontade para abrir um PR ou issue.
# 🌐 Configuração do DNS no Windows Server

Guia passo a passo para configurar o **Servidor DNS** no **Windows Server** (ex: 2022), usando o Server Manager.

---

## 📦 1. Instalar a Função DNS

1. Abra o **Server Manager**
2. Vá em **Manage > Add Roles and Features**
3. Avance até a etapa **Server Roles**
4. Marque a opção **DNS Server**
5. Clique em **Next** até a etapa final
6. Clique em **Install**
7. Após a conclusão, clique em **Close**

---

## 🔧 2. Criar Zona de Pesquisa Direta (Forward Lookup Zone)

1. No Server Manager, acesse: **Tools > DNS**
2. No console DNS:
   - Expanda o nome do servidor
   - Clique com o botão direito em **Forward Lookup Zones**
   - Selecione **New Zone**
3. No assistente:
   - Selecione **Primary Zone**
   - Se for controlador de domínio: **Store in Active Directory**
   - Defina o nome da zona (ex: `empresa.local`)
   - Tipo de atualização: **Allow only secure dynamic updates** (recomendado)
   - Finalize

---

## 🧾 3. Criar um Registro A (Host)

1. Clique na zona criada (`empresa.local`)
2. Botão direito > **New Host (A or AAAA)**
3. Preencha:
   - **Name**: `srv01`
   - **IP Address**: `192.168.1.10`
4. Clique em **Add Host**

---

## 🔍 4. Testar Resolução DNS

```bash
nslookup srv01.empresa.local
Deve retornar o IP definido.

🔁 5. Criar Zona de Pesquisa Reversa (Reverse Lookup Zone) (opcional)
No console DNS:

Botão direito em Reverse Lookup Zones

Clique em New Zone

No assistente:

Primary Zone

Tipo: IPv4

Informe o ID da rede (ex: 192.168.1)

Permita atualizações dinâmicas

Finalize

🧪 6. Testar Resolução Reversa
bash
Copiar
Editar
nslookup 192.168.1.10
Deve retornar: srv01.empresa.local

✅ Pronto! O servidor DNS está configurado e funcional.
Contribuições são bem-vindas — sinta-se à vontade para abrir um Pull Request ou Issue.

yaml
Copiar
Editar
# 📡 Configuração do DHCP no Windows Server

Guia direto para instalar e configurar o **Servidor DHCP** no Windows Server (ex: 2022), usando Server Manager.

---

## 🧩 1. Instalar a Função DHCP

1. Abra o **Server Manager**
2. Vá em **Manage > Add Roles and Features**
3. Avance até a etapa **Server Roles**
4. Marque: `DHCP Server`
5. Clique em `Next` até a instalação
6. Após instalar, clique em `Complete DHCP configuration`
7. No assistente:
   - Autorize o servidor (caso esteja em domínio)
   - Finalize a configuração

---

## 📐 2. Criar um Escopo DHCP

1. Vá em **Tools > DHCP**
2. No console DHCP:
   - Expanda o servidor
   - Botão direito em `IPv4 > New Scope`
3. No assistente:
   - **Nome do escopo**: `Escopo LAN`
   - **Intervalo de IPs**: `192.168.1.100 – 192.168.1.200`
   - **Máscara de sub-rede**: `255.255.255.0`
   - **Exclusões (opcional)**: `192.168.1.150 – 192.168.1.160`
   - **Tempo de concessão**: padrão (8 dias)
4. Configurações adicionais:
   - **Gateway (router)**: `192.168.1.1`
   - **DNS Server**: `192.168.1.10`
   - **Nome do domínio**: `empresa.local` (opcional)
5. Finalize e ative o escopo

---

## 🔎 3. Testar a Distribuição de IP

No cliente Windows:

```bash
ipconfig /release
ipconfig /renew
ipconfig /all
🔹 Deve receber um IP dentro do intervalo configurado.

⚙️ 4. Configurações Avançadas (Opcional)
Reservas de IP:

Vá em: IPv4 > Reservations > New Reservation

Informe:

Nome

IP reservado

MAC Address do cliente

Opções adicionais (ex: PXE Boot):

Vá em: IPv4 > Server Options

Adicione opções como:

066 – Nome do servidor TFTP

067 – Nome do arquivo de inicialização

✅ DHCP pronto e funcional!
Contribuições são bem-vindas. Abra um PR ou Issue se quiser colaborar.

yaml
Copiar
Editar
# 🏢 Configuração do Active Directory (AD DS) no Windows Server

Guia direto para instalação e configuração do **Active Directory Domain Services (AD DS)** no Windows Server.

---

## 🛠️ 1. Instalar a Função AD DS

1. Abra o **Server Manager**
2. Vá em `Manage > Add Roles and Features`
3. Avance até `Server Roles`
4. Marque: `Active Directory Domain Services`
5. Clique em `Next` até a etapa final e selecione `Install`
6. Ao concluir, clique em `Promote this server to a domain controller`

---

## 🌐 2. Promover o Servidor a Controlador de Domínio

1. No assistente de promoção:
   - Escolha: `Add a new forest`
   - Nome do domínio: `empresa.local`
2. Defina a senha do modo de restauração (DSRM)
3. Avance pelas etapas seguintes
4. Verifique os pré-requisitos e clique em `Install`
5. O servidor será reiniciado automaticamente

---

## 🔐 3. Login no Domínio

Após reiniciar, o login padrão será:

empresa\Administrator

yaml
Copiar
Editar

---

## 📂 4. Verificar o Domínio

Acesse:

Server Manager > Tools > Active Directory Users and Computers

yaml
Copiar
Editar

Você verá:
- O domínio criado (ex: `empresa.local`)
- As unidades organizacionais padrão (`Users`, `Computers`, etc.)

---

## 🖥️ 5. Adicionar um Cliente ao Domínio

1. Em um computador cliente:
   - Configure o **DNS** apontando para o IP do servidor AD
   - Vá em `Sistema > Nome do computador`
   - Clique em `Alterar > Domínio`
   - Digite: `empresa.local`
2. Insira as credenciais de um usuário do domínio
3. Reinicie o cliente
4. Faça login usando: `empresa\nome_de_usuario`

---

> ✅ Active Directory configurado com sucesso.  
> Contribuições são bem-vindas — sinta-se à vontade para abrir um Pull Request ou Is
# 🐧 Documentação – Instalação e Configuração do Debian

Guia básico para instalação e configuração inicial do **Debian GNU/Linux**, voltado para ambientes de servidores ou estações de trabalho.

---

## 💽 Requisitos

- ISO do Debian: [https://www.debian.org/distrib/](https://www.debian.org/distrib/)
- Requisitos mínimos:
  - 512 MB RAM (mínimo), 2 GB (recomendado)
  - 10 GB de disco
  - Acesso à internet
  - Software para gravar ISO: Rufus, balenaEtcher, etc.

---

## 🧰 Instalação do Debian

1. Grave a ISO em um pendrive bootável
2. Inicie o computador pelo pendrive
3. Selecione `Install` ou `Graphical Install`
4. Siga os passos:
   - Idioma e região
   - Hostname (nome da máquina)
   - Domínio (opcional)
   - Senha do usuário root
   - Criação do usuário normal
   - Particionamento (guiado ou manual)
   - Configuração de rede e mirror
   - Instalar GRUB
5. Remova o pendrive e reinicie

---

## 🔧 Pós-instalação (via terminal)

### Atualizar o sistema

```bash
sudo apt update && sudo apt upgrade -y
Instalar utilitários comuns
bash
Copiar
Editar
sudo apt install curl wget net-tools vim git htop -y
🔐 Habilitar acesso root via SSH (opcional)
Editar o arquivo de configuração:

bash
Copiar
Editar
sudo nano /etc/ssh/sshd_config
Alterar ou descomentar a linha:

nginx
Copiar
Editar
PermitRootLogin yes
Reiniciar o serviço SSH:

bash
Copiar
Editar
sudo systemctl restart ssh
🌐 Configurar IP Estático
Editar interfaces de rede:

bash
Copiar
Editar
sudo nano /etc/network/interfaces
Exemplo:

ini
Copiar
Editar
auto enp0s3
iface enp0s3 inet static
  address 192.168.1.100
  netmask 255.255.255.0
  gateway 192.168.1.1
  dns-nameservers 8.8.8.8 8.8.4.4
Reiniciar rede:

bash
Copiar
Editar
sudo systemctl restart networking
🛡️ Ativar UFW (Firewall)
bash
Copiar
Editar
sudo apt install ufw -y
sudo ufw allow OpenSSH
sudo ufw enable
✅ Verificações Finais
Verificar conectividade:

bash
Copiar
Editar
ping google.com
Verificar IP:

bash
Copiar
Editar
ip a
Testar acesso remoto via SSH (se configurado)

🚀 Debian instalado e configurado com sucesso.
Para melhorias, envie um Pull Request ou abra uma Issue.

yaml
Copiar
Editar
# 💿 Instalação do Debian – Passo a Passo

Guia direto para instalação do **Debian GNU/Linux** em máquinas físicas ou virtuais.

---

## 📋 Requisitos

- ISO do Debian: [https://www.debian.org/distrib/](https://www.debian.org/distrib/)
- Pendrive (4 GB ou mais) ou VM
- Gravador de ISO (ex: **Rufus**, **balenaEtcher**)
- Conexão com a internet

---

## 🧰 Criar Mídia Bootável

1. Baixe a ISO do Debian (stable)
2. Use o **Rufus** (Windows) ou **balenaEtcher** (Linux/macOS) para gravar a ISO no pendrive
3. Inicie o computador pelo pendrive

---

## 🚀 Etapas da Instalação

### 1. Início

- Selecione: `Install` ou `Graphical Install`

### 2. Configuração básica

- Idioma, país e layout do teclado
- Hostname (nome do computador)
- Domínio (opcional – ex: `empresa.local`)
- Senha do root
- Criação do usuário comum

### 3. Particionamento

- Escolha entre:
  - Guiado (recomendado para iniciantes)
  - Manual (mais flexível)
- Sugestão: sistema de arquivos `ext4`

### 4. Configuração de rede

- DHCP automático ou IP fixo (ajustável depois)
- Escolha o mirror (espelho de repositório Debian)

### 5. Instalando o GRUB

- Confirme a instalação do GRUB no disco principal (`/dev/sda`)
- Finalize a instalação

---

## 🔄 Após a Instalação

1. Remova o pendrive
2. Reinicie o sistema
3. Faça login com o usuário criado

---

## ✅ Sistema Debian Pronto

Próximos passos recomendados:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install vim curl net-tools git htop -y
💡 Para configurações de rede, SSH, firewall e outros serviços, veja os outros arquivos deste repositório ou abra uma Issue para dúvidas.

yaml
Copiar
Editar
# 🌐 Configuração de Servidor DNS no Debian (BIND9)

Guia passo a passo para configurar um **servidor DNS local** com **BIND9** no Debian.

---

## 📦 Instalação

```bash
sudo apt update
sudo apt install bind9 -y
📁 Arquivos principais
/etc/bind/named.conf → Arquivo principal

/etc/bind/named.conf.local → Definições de zonas

/etc/bind/db.* → Arquivos de zona (direta e reversa)

⚙️ Configurar Zonas DNS
1. Editar zonas em named.conf.local
bash
Copiar
Editar
sudo nano /etc/bind/named.conf.local
Adicione:

bash
Copiar
Editar
zone "empresa.local" {
    type master;
    file "/etc/bind/db.empresa";
};

zone "1.168.192.in-addr.arpa" {
    type master;
    file "/etc/bind/db.192";
};
📝 Criar Arquivos de Zona
Zona direta: db.empresa
bash
Copiar
Editar
sudo cp /etc/bind/db.local /etc/bind/db.empresa
sudo nano /etc/bind/db.empresa
Conteúdo de exemplo:

lua
Copiar
Editar
$TTL 604800
@       IN      SOA     ns.empresa.local. root.empresa.local. (
                        2         ; Serial
                        604800    ; Refresh
                        86400     ; Retry
                        2419200   ; Expire
                        604800 )  ; Negative Cache TTL
@       IN      NS      ns.empresa.local.
ns      IN      A       192.168.1.10
www     IN      A       192.168.1.20
Zona reversa: db.192
bash
Copiar
Editar
sudo cp /etc/bind/db.127 /etc/bind/db.192
sudo nano /etc/bind/db.192
Conteúdo de exemplo:

lua
Copiar
Editar
$TTL 604800
@       IN      SOA     ns.empresa.local. root.empresa.local. (
                        1         ; Serial
                        604800    ; Refresh
                        86400     ; Retry
                        2419200   ; Expire
                        604800 )  ; Negative Cache TTL
@       IN      NS      ns.empresa.local.
10      IN      PTR     ns.empresa.local.
20      IN      PTR     www.empresa.local.
✅ Verificar e Aplicar Configuração
Testar os arquivos:
bash
Copiar
Editar
sudo named-checkconf
sudo named-checkzone empresa.local /etc/bind/db.empresa
sudo named-checkzone 1.168.192.in-addr.arpa /etc/bind/db.192
Reiniciar o serviço:
bash
Copiar
Editar
sudo systemctl restart bind9
🔎 Testar DNS
Usando dig:
bash
Copiar
Editar
dig @localhost www.empresa.local
Usando nslookup:
bash
Copiar
Editar
nslookup www.empresa.local 127.0.0.1
📌 Dica Final
Para que outros dispositivos da rede usem esse DNS:

Configure manualmente o IP do servidor como DNS primário

Ou configure via servidor DHCP (ex: isc-dhcp-server)

✅ Servidor DNS funcional no Debian com BIND9.
Contribuições são bem-vindas — abra uma issue ou envie um PR.

yaml
Copiar
Editar
# 📡 Servidor DHCP no Debian (ISC DHCP Server)

Guia rápido para instalar e configurar o **servidor DHCP** no Debian usando o **isc-dhcp-server**.

---

## 📦 Instalação

```bash
sudo apt update
sudo apt install isc-dhcp-server -y
⚙️ Configuração
Editar o arquivo principal:
bash
Copiar
Editar
sudo nano /etc/dhcp/dhcpd.conf
Exemplo básico:
conf
Copiar
Editar
option domain-name "empresa.local";
option domain-name-servers 192.168.1.10, 8.8.8.8;

default-lease-time 600;
max-lease-time 7200;

authoritative;

subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.100 192.168.1.200;
  option routers 192.168.1.1;
  option broadcast-address 192.168.1.255;
}
🌐 Definir interface de rede
Editar o arquivo:

bash
Copiar
Editar
sudo nano /etc/default/isc-dhcp-server
Ajustar conforme sua interface:

conf
Copiar
Editar
INTERFACESv4="enp0s3"
🔄 Ativar o serviço
bash
Copiar
Editar
sudo systemctl restart isc-dhcp-server
sudo systemctl enable isc-dhcp-server
Verificar status:

bash
Copiar
Editar
sudo systemctl status isc-dhcp-server
🧪 Teste e logs
Conecte um cliente à rede

Configure o cliente para obter IP automaticamente

Verifique se ele recebe IP no intervalo configurado

Verificar logs:

bash
Copiar
Editar
journalctl -u isc-dhcp-server
tail -f /var/log/syslog
🎯 Reserva de IP (opcional)
Adicione ao dhcpd.conf:

conf
Copiar
Editar
host impressora01 {
  hardware ethernet 00:11:22:33:44:55;
  fixed-address 192.168.1.50;
}
✅ DHCP ativo e funcional. Combine com DNS para uma rede interna completa.

yaml
Copiar
Editar
# 🔐 Wazuh – Monitoramento e Segurança Open Source

Este repositório contém um guia prático para instalar e configurar o **Wazuh**, uma plataforma open source de **detecção de intrusão (HIDS)**, **SIEM**, e **monitoramento de segurança**.

---

## 📦 Componentes

- **Wazuh Server**: Processa e analisa dados.
- **Wazuh Agent**: Instalação nos hosts monitorados.
- **Elastic Stack**: Armazena e exibe logs (Elasticsearch, Kibana).
- **Wazuh Dashboard**: Interface web baseada em Kibana.

---

## ☁️ Requisitos

- SO: Debian, Ubuntu, CentOS, RHEL
- 4 GB RAM (mínimo)
- 2 vCPUs
- Acesso root
- Acesso à internet

---

## 🚀 Instalação All-in-One (Server + Elastic + Dashboard)

```bash
sudo apt update && sudo apt upgrade -y
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh -a
O parâmetro -a instala todos os componentes (server, elasticsearch e dashboard).

🌐 Acesso ao Dashboard
Após a instalação:

makefile
Copiar
Editar
URL: https://<IP_DO_SERVIDOR>
Usuário: admin
Senha: (fornecida ao final da instalação)
🖥️ Instalação do Agente em Clientes
1. Adicionar o repositório:
bash
Copiar
Editar
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo apt-key add -
echo "deb https://packages.wazuh.com/4.x/apt/ stable main" | sudo tee /etc/apt/sources.list.d/wazuh.list
sudo apt update
2. Instalar o agente:
bash
Copiar
Editar
sudo apt install wazuh-agent -y
3. Configurar o agente:
Editar o IP do servidor no arquivo:

bash
Copiar
Editar
sudo nano /var/ossec/etc/ossec.conf
Adicionar:

xml
Copiar
Editar
<server>
  <address>192.168.1.10</address>
</server>
4. Iniciar o serviço:
bash
Copiar
Editar
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
🔍 Comandos úteis
bash
Copiar
Editar
# Verificar status do agente
sudo systemctl status wazuh-agent

# Reiniciar servidor
sudo systemctl restart wazuh-manager
🛡️ Recursos do Wazuh
Análise de logs

Detecção de rootkits

Monitoramento de integridade

Inventário de hardware/software

Política de segurança

Vulnerability detection

Integração com Active Directory, Office 365, etc.

📚 Documentação oficial
https://documentation.wazuh.com

https://github.com/wazuh

✅ Segurança e monitoramento centralizados em uma única plataforma. Contribuições são bem-vindas via PR ou Issues.

yaml
Copiar
Editar
# 🚀 Instalação do Wazuh (All-in-One)

Este guia mostra como instalar o **Wazuh Server**, **Elastic Stack** e **Dashboard** em um único servidor Debian/Ubuntu.

---

## Requisitos mínimos

- Sistema: Debian, Ubuntu ou similar
- 2 vCPUs
- 4 GB RAM
- Acesso root
- Conexão com a internet

---

## Passo 1 – Atualizar sistema

```bash
sudo apt update && sudo apt upgrade -y
Passo 2 – Baixar instalador oficial
bash
Copiar
Editar
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
Passo 3 – Executar instalador completo
bash
Copiar
Editar
sudo bash wazuh-install.sh -a
O parâmetro -a instala todos os componentes (server, elasticsearch e dashboard).

Passo 4 – Acessar painel web
Após a instalação, acesse:

makefile
Copiar
Editar
https://<IP_DO_SERVIDOR>
Usuário: admin
Senha: (fornecida no final da instalação)
Observações
A instalação pode demorar vários minutos.

O script configura e inicia todos os serviços necessários.

Para instalações avançadas e cluster, consulte a documentação oficial:
https://documentation.wazuh.com

🎉 Wazuh instalado com sucesso! Próximo passo: instalar e configurar agentes nos hosts monitorados.

css
Copiar
Editar
# 🐉 Kali Linux – Distribuição para Testes de Penetração

Guia básico para instalação e uso do **Kali Linux**, distribuição Debian focada em segurança ofensiva e pentest.

---

## 📋 O que é o Kali Linux?

- Baseado em Debian
- Ferramentas integradas para pentest, análise forense, engenharia reversa
- Atualizações frequentes e comunidade ativa

---

## 💻 Requisitos mínimos

- CPU: 1 GHz (64-bit recomendado)
- RAM: mínimo 2 GB (4+ GB recomendado)
- Espaço em disco: 20 GB+
- Internet para atualizações e instalação de pacotes

---

## 🚀 Instalação

### 1. Baixe a ISO oficial

[https://www.kali.org/get-kali/](https://www.kali.org/get-kali/)

### 2. Crie um pendrive bootável

- No Windows: use [Rufus](https://rufus.ie)
- No Linux/macOS:

```bash
sudo dd if=kali-linux.iso of=/dev/sdX bs=4M status=progress && sync
(Substitua /dev/sdX pela unidade correta.)

3. Faça boot pelo pendrive e siga o instalador
Escolha idioma, região e teclado

Configure rede e usuário

Particione o disco

Finalize instalação

🛠️ Uso básico
Atualize o sistema:

bash
Copiar
Editar
sudo apt update && sudo apt full-upgrade -y
Instale ferramentas adicionais:

bash
Copiar
Editar
sudo apt install <pacote>
🧰 Ferramentas populares
Nmap – Scanner de rede

Metasploit – Framework de exploração

Wireshark – Analisador de pacotes

John the Ripper – Quebra de senhas

Aircrack-ng – Auditoria Wi-Fi

Burp Suite – Teste de segurança web

🔐 Segurança e boas práticas
Use somente em ambientes autorizados

Evite uso como sistema principal

Utilize VPN em testes remotos

Mantenha ferramentas atualizadas

📚 Links úteis
Documentação oficial: https://www.kali.org/docs/

Fórum: https://forums.kali.org/

Blog: https://www.kali.org/blog/

⚠️ Use o Kali Linux com responsabilidade e legalidade.

arduino
Copiar
Editar
# 🚀 Instalação do Kali Linux

Guia rápido para instalar o Kali Linux, distribuição focada em segurança ofensiva e pentest.

---

## Requisitos mínimos

- Processador 1 GHz (64-bit recomendado)
- 2 GB RAM (4 GB recomendado)
- 20 GB de espaço em disco
- Internet para atualizações

---

## Passo 1 – Baixar a ISO oficial

[https://www.kali.org/get-kali/](https://www.kali.org/get-kali/)

---

## Passo 2 – Criar pendrive bootável

**Windows:** Use [Rufus](https://rufus.ie)

**Linux/macOS:**

```bash
sudo dd if=kali-linux.iso of=/dev/sdX bs=4M status=progress && sync
(Substitua /dev/sdX pelo dispositivo correto)

Passo 3 – Boot pelo pendrive e instalação
Reinicie e dê boot pelo pendrive

Siga o instalador:

Configure idioma, teclado e rede

Crie partições conforme preferir

Finalize instalação

Passo 4 – Atualizar sistema
bash
Copiar
Editar
sudo apt update && sudo apt full-upgrade -y
Passo 5 – Instalar ferramentas extras (opcional)
bash
Copiar
Editar
sudo apt install <pacote>
Observações
Use Kali apenas em ambientes autorizados

Evite usar como sistema principal

Mantenha o sistema sempre atualizado

⚠️ Use com ética e responsabilidade.

arduino
Copiar
Editar
# 🤖 Ansible – Automação e Orquestração de TI

Este repositório contém documentação e exemplos básicos para começar com **Ansible**, ferramenta open source para automação de configuração, deploy e gerenciamento.

---

## 📋 O que é Ansible?

- Automação simples e poderosa, sem agentes (agentless).
- Usa YAML para playbooks.
- Comunicação via SSH.
- Ideal para configurar servidores, deploy de apps e orquestração.

---

## 💻 Requisitos

- Máquina de controle: Linux/macOS/Windows (WSL)
- Python 3.8+
- Acesso SSH configurado nos hosts

---

## 🚀 Instalação rápida

No Ubuntu/Debian:

```bash
sudo apt update
sudo apt install ansible -y
No macOS (Homebrew):

bash
Copiar
Editar
brew install ansible
No Windows (via WSL):

bash
Copiar
Editar
sudo apt update
sudo apt install ansible -y
📁 Estrutura básica do projeto
arduino
Copiar
Editar
ansible-project/
├── inventory        # lista de hosts
├── playbook.yml     # playbook principal
├── roles/           # roles para modularização
│   └── common/
│       ├── tasks/
│       ├── handlers/
│       ├── templates/
│       └── files/
└── README.md
📝 Exemplo de playbook
yaml
Copiar
Editar
---
- name: Configurar servidor Apache
  hosts: webservers
  become: yes

  tasks:
    - name: Atualizar cache apt
      apt:
        update_cache: yes
    
    - name: Instalar Apache2
      apt:
        name: apache2
        state: present
    
    - name: Copiar index.html personalizado
      copy:
        src: files/index.html
        dest: /var/www/html/index.html
        owner: www-data
        group: www-data
        mode: '0644'
    
    - name: Iniciar e habilitar Apache
      systemd:
        name: apache2
        state: started
        enabled: yes
⚙️ Inventário (inventory)
ini
Copiar
Editar
[webservers]
web1.example.com
web2.example.com
🔧 Executar playbook
bash
Copiar
Editar
ansible-playbook -i inventory playbook.yml
📚 Links úteis
Documentação oficial

Guia rápido

Exemplos oficiais

🚀 Automatize sua infraestrutura com Ansible!# 📖 Explicação dos Scripts Ansible

Este documento explica o que faz cada parte do playbook de exemplo para configurar um servidor Apache.

---

## Playbook completo

```yaml
---
- name: Configurar servidor Apache
  hosts: webservers
  become: yes

  tasks:
    - name: Atualizar cache apt
      apt:
        update_cache: yes

    - name: Instalar Apache2
      apt:
        name: apache2
        state: present

    - name: Copiar index.html personalizado
      copy:
        src: files/index.html
        dest: /var/www/html/index.html
        owner: www-data
        group: www-data
        mode: '0644'

    - name: Iniciar e habilitar Apache
      systemd:
        name: apache2
        state: started
        enabled: yes
Explicação detalhada
1. Atualizar cache apt
yaml
Copiar
Editar
- name: Atualizar cache apt
  apt:
    update_cache: yes
Atualiza a lista de pacotes disponíveis no gerenciador apt.

Garante que as próximas instalações usem os pacotes mais recentes.

2. Instalar Apache2
yaml
Copiar
Editar
- name: Instalar Apache2
  apt:
    name: apache2
    state: present
Instala o pacote apache2 caso não esteja instalado.

O state: present assegura que o pacote estará instalado, sem reinstalar se já existir.

3. Copiar arquivo index.html personalizado
yaml
Copiar
Editar
- name: Copiar index.html personalizado
  copy:
    src: files/index.html
    dest: /var/www/html/index.html
    owner: www-data
    group: www-data
    mode: '0644'
Copia o arquivo files/index.html do controle para o servidor remoto.

Define o proprietário e grupo para www-data (usuário padrão do Apache).

Ajusta as permissões do arquivo para leitura.

4. Iniciar e habilitar Apache
yaml
Copiar
Editar
- name: Iniciar e habilitar Apache
  systemd:
    name: apache2
    state: started
    enabled: yes
Inicia o serviço Apache.

Habilita para iniciar automaticamente no boot do sistema.

Resumo
Este playbook automatiza:

Atualização do sistema

Instalação do Apache

Configuração do site padrão

Ativação do serviço web

💡 Automatizar esses passos facilita a administração em múltiplos servidores.

perl
Copiar
Editar
# ⚙️ Playbooks Ansible para Automação

Exemplos práticos de playbooks para tarefas comuns com Ansible.

---

## 1. Atualizar pacotes do sistema

```yaml
---
- name: Atualizar pacotes em servidores Linux
  hosts: all
  become: yes

  tasks:
    - name: Atualizar cache apt (Debian/Ubuntu)
      apt:
        update_cache: yes
        cache_valid_time: 3600
      when: ansible_os_family == "Debian"

    - name: Atualizar sistema usando apt
      apt:
        upgrade: dist
      when: ansible_os_family == "Debian"

    - name: Atualizar sistema usando yum (RHEL/CentOS)
      yum:
        name: '*'
        state: latest
      when: ansible_os_family == "RedHat"
2. Instalar e iniciar Nginx
yaml
Copiar
Editar
---
- name: Instalar e iniciar Nginx
  hosts: webservers
  become: yes

  tasks:
    - name: Instalar Nginx (Debian/Ubuntu)
      apt:
        name: nginx
        state: present
      when: ansible_os_family == "Debian"

    - name: Instalar Nginx (RedHat)
      yum:
        name: nginx
        state: present
      when: ansible_os_family == "RedHat"

    - name: Iniciar e habilitar Nginx
      systemd:
        name: nginx
        state: started
        enabled: yes
3. Criar usuário Linux
yaml
Copiar
Editar
---
- name: Criar usuário com senha
  hosts: all
  become: yes

  vars:
    username: "novo_usuario"
    password: "{{ 'senha123' | password_hash('sha512') }}"

  tasks:
    - name: Criar usuário
      user:
        name: "{{ username }}"
        password: "{{ password }}"
        shell: /bin/bash
        state: present
4. Copiar arquivo para múltiplos hosts
yaml
Copiar
Editar
---
- name: Distribuir arquivo de configuração
  hosts: all
  become: yes

  tasks:
    - name: Copiar arquivo de configuração
      copy:
        src: files/config.conf
        dest: /etc/app/config.conf
        owner: root
        group: root
        mode: '0644'
5. Reiniciar serviço após alteração
yaml
Copiar
Editar
---
- name: Atualizar e reiniciar serviço
  hosts: all
  become: yes

  tasks:
    - name: Copiar novo arquivo de serviço
      copy:
        src: files/myservice.service
        dest: /etc/systemd/system/myservice.service
        owner: root
        group: root
        mode: '0644'
      notify:
        - Reiniciar myservice

  handlers:
    - name: Reiniciar myservice
      systemd:
        name: myservice
        state: restarted
Como executar os playbooks
bash
Copiar
Editar
ansible-playbook -i inventory playbook.yml
🚀 Use esses exemplos como base para automações mais complexas e personalizadas.# 📂 Arquivos de Inventário Ansible

Este documento mostra exemplos básicos de arquivos de inventário usados pelo Ansible para definir os hosts e grupos de hosts.

---

## 1. Inventário simples (hosts únicos)

```ini
web1.example.com
db1.example.com
2. Inventário com grupos
ini
Copiar
Editar
[webservers]
web1.example.com
web2.example.com

[dbservers]
db1.example.com
db2.example.com
3. Inventário com variáveis de host
ini
Copiar
Editar
[webservers]
web1.example.com ansible_user=admin ansible_port=2222
web2.example.com ansible_user=admin ansible_port=2222

[dbservers]
db1.example.com ansible_user=dbadmin ansible_ssh_private_key_file=~/.ssh/id_rsa_db
4. Inventário com variáveis de grupo
ini
Copiar
Editar
[webservers:vars]
ansible_user=admin
ansible_port=2222
5. Inventário em formato YAML (hosts.yaml)
yaml
Copiar
Editar
all:
  hosts:
    web1.example.com:
      ansible_user: admin
    db1.example.com:
      ansible_user: dbadmin
  children:
    webservers:
      hosts:
        web1.example.com:
    dbservers:
      hosts:
        db1.example.com:
Como usar o inventário
Execute o playbook com o inventário especificado:

bash
Copiar
Editar
ansible-playbook -i inventory playbook.yml
📌 Mantenha seu inventário organizado para facilitar a automação em múltiplos servidores.



Ansible Automation Hub Repositório centralizado com playbooks, inventários e documentação para automação de infraestrutura usando Ansible. Contém exemplos práticos para gerenciar servidores Linux, configurar serviços, implementar segurança e orquestrar deploys de forma simples e eficiente.
