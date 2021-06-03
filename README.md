# Configuração de Ambiente de Desenvolvimento
##### Por: [@amanda-lima](https://github.com/amanda-lima)

Neste documento será demonstrado o passo a passo da configuração do ambiente de desenvolvimento para uma máquina Linux Ubuntu.

Serão instaladas as ferramentas: 
- Chrome; 
- VSCode; 
- Git; 
- PHP; 
- Node (NVM);
- Docker; 
- Docker Compose;
- Portainer.io;
- XAMPP;



Para realizar a instalação dessas ferramentas neste sistema iremos utilizar o Terminal Linux.

## Instalando o Chrome:
- Baixando o pacote mais recente do Google Chrome:
  ```shell
  wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
  ```
- Instalando o pacote .deb:
  ```shell
  sudo apt install ./google-chrome-stable_current_amd64.deb
  ```
- Durante o processo de instalação, o repositório oficial do Google será adicionado ao seu sistema. Você pode usar o comando cat para verificar o conteúdo do arquivo:
  ```shell
  cat /etc/apt/sources.list.d/google-chrome.list
  ```
- Esse comando deverá retornar o seguinte output:
  ```shell
  ### THIS FILE IS AUTOMATICALLY CONFIGURED ###
  # You may comment out this entry, but any other modifications may be lost.
  deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main
  ```
---
## Instalando o VSCode:


Iremos instalar o VScode pela própria loja de aplicativos do Ubuntu e instalar os plugins: PHPIntelephense, MySQL (cweijan) e Docker.


---
## Instalando o Git:

> O Git é um sistema de controle de versão de arquivos. Através deles podemos desenvolver projetos na qual diversas pessoas podem contribuir simultaneamente no mesmo, editando e criando novos arquivos e permitindo que os mesmos possam existir sem o risco de suas alterações serem sobrescritas.


- Verificando se existem atualizações e atualizando os pacotes já existentes:
  ```shell
  sudo apt-get update && sudo apt-get upgrade
  ```

- Instalando o Git:
  ```shell
  sudo apt install git
  ```

- Verificando a versão instalada:
  ```shell
  git --version
  ```

### Configurando o Git:
- Definindo user name:
  ```shell
  git config --global user.name "Your Name"
  ```
- Definindo email:
  ```shell
  git config --global user.email "your_email@domain.com"
  ```
- Verificando configurações:
  ```shell
  git config --list
  ```
### Configurando chave SSH:

- Verificando chaves SSH:
  ```shell
    ls -agit@github.com:user-name/repository-name.gitl ~/.ssh
  ```
- Gerando nova chave SSH:
    - Abra o Git Bash/Terminal;

    - Cole o texto abaixo, substituindo o endereço de e-mail pelo seu GitHub. 

      ```shell
      ssh-keygen -t ed25519 -C "your_email@example.com"
      ```

    - Quando aparecer a solicitação "Enter a file in which to save the key" (Insira um arquivo no qual salvar a chave), 
    presssione `Enter.` O local padrão do arquivo será aceito.

    - Será criada uma chave (se definido caminho padrão) em: `/home/<your-user>/.ssh/id_ed25519.pub`

    - Abra o arquivo criado com o comando abaixo:
      ```shell
      cat /home/<your-user>/.ssh/id_ed25519.pub
      ```

    - Copie a chave que será exibida no terminal, e colaremos em nosso github, em configurações > SSH & GPG Keys
      ```shell
      ssh-ed25519 <hash-random-key> your_email@example.com
      ```      
---

## Instalando o PHP 7.4:
- Verificando se existem atualizações e atualizando os pacotes já existentes:
  ```shell
  sudo apt-get update && sudo apt-get upgrade
  ```

- Instalando o PHP:
  ```shell
  sudo apt-get install php
  ```

- Verificando a versão instalada:
  ```shell
  php -v
  ```
---
## Instalando o Node (via NVM):
Source: [Tutorial DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04-pt)

> O **Node.js** pode ser definido como um ambiente de execução Javascript server-side. Isso significa que com o **Node.js** é possível criar aplicações Javascript para rodar como uma aplicação standalone em uma máquina, não dependendo de um browser para a execução, como estamos acostumados.

> O **nvm** é um gerenciador de versões do Node. E é usado para instalar e gerenciar suas versões.

Para instalar o NVM em sua máquina Ubuntu 20.04, visite a página do GitHub do projeto. Copie o comando `curl` do arquivo README, mostrado na página principal. Isso dará a você a versão mais recente do script de instalação.

### Instalando o NVM

- Execute o comando abaixo com o `| bash` anexado no final para que o script possa ser baixado e executado:

  ```shell
  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
  ```

- Isso instalará o script nvm em sua conta de usuário. Para usá-lo, você deve antes gerar seu arquivo `.bashrc`:

  ```shell
  cat ~/.bashrc
  ```
### Instalando o Node via NVM

- Para instalar a versão mmais recente, utilizaremos o comando:
  ```shell
  nvm install node
  ```

- Para instalar uma versão diferente, iremos listar quais versões do Node estão disponíveis em nosso NVM:
  ```shell
  nvm list-remote
  ```

- Instale uma versão do Node digitando qualquer uma das versões que estiver vendo. Por exemplo, para obter a versão v13.6.0, digite:

  ```shell
  nvm install v13.6.0
  ```
- Para verificarmos a versão instalada, utilizaremos o comando:
  ```shell
  node -v
  ```

---
## Instalando o Docker:
Source: [Tutorial DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04)

> O Docker é um aplicativo que simplifica o processo de gerenciamento de processos de aplicação em containers. Os containers deixam você executar suas aplicações em processos isolados de recurso. Eles são semelhantes a máquinas virtuais, mas os containers são mais portáveis, mais fáceis de usar e mais dependentes do sistema operacional do host.

### Instalando Docker
- Primeiro, atualize sua lista existente de pacotes:
  
  ```shell
    sudo apt update
  ```  

- Em seguida, instale alguns pacotes de pré-requisitos que permitem ao apt usar pacotes sobre HTTPS:
  
  ```shell
    sudo apt install apt-transport-https ca-certificates curl software-properties-common
  ```   

- Em seguida, adicione a chave GPG para o repositório oficial do Docker ao seu sistema:
  
  ```shell
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  ```

- Adicione o repositório Docker às fontes APT:
  
  ```shell
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
  ```

- Em seguida, atualize o banco de dados de pacotes com os pacotes Docker do repo recém-adicionado:
  
  ```shell
    sudo apt update
  ```   

- Certifique-se de que está prestes a instalar a partir do repositório Docker em vez do repositório Ubuntu padrão:
  
  ```shell
    apt-cache policy docker-ce
  ```  

  _Observe que docker-ce não está instalado, mas o candidato para instalação é do repositório Docker para Ubuntu 20.04 (focal)._
Finalmente, instale o Docker:
    
  ```shell
      sudo apt install docker-ce
  ```     

- O Docker agora deve estar instalado, o daemon iniciado e o processo habilitado para iniciar na inicialização. Verifique se ele está funcionando:
    
  ```shell
      sudo systemctl status docker #para linux
  ```
### Executando o comando Docker sem Sudo (opcional)

- Se quiser evitar digitar sudo sempre que executar o comando docker, adicione seu nome de usuário ao grupo docker:
  
  ```shell
    sudo usermod -aG docker ${USER}
  ```  

- Para aplicar a nova associação de grupo, saia do servidor e entre novamente ou digite o seguinte:
  
  ```shell
    su - ${USER}
  ```   

- Você será solicitado a inserir sua senha de usuário para continuar.

- Confirmando se o seu usuário foi adicionado ao grupo docker digitando:
  
  ```shell
    id -nG
  ```  
  ```shell
    #Output
    sammy sudo docker
  ```  
- Listando docker:
  
  ```shell
    docker ps
  ```  
- Executando docker teste: 

  ```shell
    docker run hello-world
  ```  
### Instalando o Docker Compose (utilizaremos 1.28.2)

- Baixando docker-compose:
  ```shell
    sudo curl -L "https://github.com/docker/compose/releases/download/1.28.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  ```  
- Dando permissão de execução para docker-compose:
  
  ```shell
    sudo chmod +x /usr/local/bin/docker-compose
  ```  
- Verificando versão:
  
  ```shell
    docker-compose --version
  ```
---
## Instalando o Portainer.io
> O Portainer é uma ferramenta para ajudar na administração de seus containers, sejam eles locais, ou rodando em modo "swarm". Resumidamente, o Portainer é um ótimo front-end para Docker.

### Instalando o Portainer

- Crie um volume para o Portainer com o seguinte comando:

  ```shell
  docker volume create portainer_data
  ```
- Instalando o portainer:

  ```shell
  docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
  ```

    _Observação: o parâmetro -v /var/run/docker.sock:/var/run/docker.sock serve apenas para servidores e ambientes Linux._

- Verificando se o container está de pé:
  ```
  docker ps
  ```

- Em seguida, acesse o seu servidor na porta 9000 para prosseguir a instalação:

  `http://localhost:9000/`

- Preencha um nome de usuário e senha:

  ![imagem](https://i.imgur.com/tMuSKCW.png)

- Em seguida, você deve selecionar qual tipo de instalação deseja realizar. Note que é possível administrar vários serviços de containeres, inclusive remotos. Vamos selecionar,por ora, a opção `Local`:

  ![imagem](https://i.imgur.com/SwiPDzD.png)

- Agora selecione o servidor e começar a utilizar:

  ![imagem](https://i.imgur.com/L1fyZl8.png)

- Aqui são encontrados as informações e controles sobre containers, imagens, volumes, etc.

  ![imagem](https://i.imgur.com/rs3liXd.png)

---
## Instalando o XAMPP
[Tutorial Point Comunicação](https://pointcom.sampa.br/linux/como-instalar-o-xampp-no-ubuntu-20-04-lts/)


> O XAMPP é um pacote que oferece um ambiente de desenvolvimento onde você pode desenvolver um software para a web ou criar um website com todas as ferramentas necessárias.

### Instalando o XAMPP

 - Baixando o pacote mais recente do XAMPP:
    ```shell
    wget https://www.apachefriends.org/xampp-files/7.4.19/xampp-linux-x64-7.4.19-0-installer.run
    ```

 - Alterando a permissão do instalador. _755 significa acesso de leitura e execução para todos e também acesso de gravação para o proprietário do arquivo._
    ```shell
    chmod 755 xampp-linux-x64-7.4.19-0-installer.run
    ```

- Executando o instalador:
  ```shell
  sudo ./xampp-linux-x64-7.4.19-0-installer.run
  ```

### Assistente de Instalação

- No momento em que você executar o comando de instalação, um assistente de configuração do XAMP será aberto. Clique no botão `Avançar` .

  ![imagem](https://i.imgur.com/Y69bApB.jpeg)

- Selecione os componentes `“Arquivos XAMPP Core”` e arquivos `XAMPP Developer` e, em seguida, `AVANÇAR`.

  ![imagem](https://i.imgur.com/n9GGNoD.jpg)

- Por padrão, todos os arquivos serão descompactados em `/opt/lampp.`

  ![imagem](https://i.imgur.com/wT6bxuT.jpg)

  ![imagem](https://i.imgur.com/J68N2YZ.jpg)

  ![imagem](https://i.imgur.com/TKZcz85.jpg)
