
# 🐳 Docker no WSL 2 (Sem Docker Desktop)

Este guia rápido mostra como instalar o **Docker Engine** diretamente em sua distribuição **WSL 2** (como o Ubuntu) no Windows, dispensando o uso do Docker Desktop.

-----

## 🚀 Pré-requisitos

  * **Windows 10/11** com o **WSL 2** configurado.
  * Uma distribuição Linux (ex: Ubuntu) instalada no WSL.

-----

## ⚙️ 1. Atualizando o Sistema e Instalando Dependências

Comece atualizando sua distribuição Linux e instalando os pacotes necessários para gerenciar repositórios `apt` através de HTTPS.

```bash
# Atualiza a lista de pacotes
sudo apt update

# Faz o upgrade dos pacotes existentes
sudo apt upgrade -y

# Instala as dependências necessárias
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
```

-----

## 🔑 2. Adicionando a Chave GPG e o Repositório Oficial do Docker

Agora, vamos adicionar a chave GPG oficial do Docker e configurar o repositório `stable` do Docker em suas fontes de pacote.

```bash
# Adiciona a chave GPG oficial do Docker
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Adiciona o repositório do Docker à lista de fontes
echo "deb [signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

-----

## 📦 3. Instalando o Docker Engine

Com o repositório configurado, atualize a lista de pacotes novamente e instale o **Docker Engine**, o **CLI** e o **containerd**.

```bash
# Atualiza os repositórios novamente
sudo apt update

# Instala o Docker Engine e dependências
sudo apt install -y docker-ce docker-ce-cli containerd.io
```

-----

## 🛠️ 4. Configurando Permissões (Dica Importante\!)

Por padrão, você precisaria usar `sudo` para cada comando `docker`. Para evitar isso, adicione seu usuário ao grupo `docker`.

⚠️ **Importante:** Após executar este comando, você precisará **sair e entrar novamente** na sua sessão do WSL (ou reiniciar o terminal) para que a alteração do grupo tenha efeito.

```bash
# Adiciona seu usuário atual ($USER) ao grupo 'docker'
sudo usermod -aG docker $USER
```

-----

## ✅ 5. Verificação Final

Após a reentrada na sessão do WSL, você deve ser capaz de verificar a versão do Docker sem usar o `sudo`.

```bash
# Verifica a versão do Docker para confirmar a instalação
docker --version
```

Se tudo correu bem, o Docker está pronto para ser usado diretamente no seu ambiente WSL 2\!
