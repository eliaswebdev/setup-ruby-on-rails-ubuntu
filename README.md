# Setup Ruby on Rails Ubuntu
Configurando Ruby, Rails, MySQL, PostgreSQL e Git no Ubuntu

## 1) Atualizando tudo
```zsh
lsb_release -a
sudo apt update
sudo apt dist-upgrade
sudo apt upgrade
```
ou
```zsh
sudo apt update && sudo apt dist-upgrade && sudo apt upgrade
```

## 2) Instalando ZSH e Oh-My-Zsh
### [zsh]
```zsh
sudo apt install build-essential git htop zsh curl
```
### [oh-my-zsh] https://ohmyz.sh
```zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### [oh-my-zsh] Spaceship Theme - https://github.com/denysdovhan/spaceship-prompt

Clone this repo:

```zsh
git clone https://github.com/denysdovhan/spaceship-prompt.git "$ZSH_CUSTOM/themes/spaceship-prompt" --depth=1
```

Symlink `spaceship.zsh-theme` to your oh-my-zsh custom themes directory:

```zsh
ln -s "$ZSH_CUSTOM/themes/spaceship-prompt/spaceship.zsh-theme" "$ZSH_CUSTOM/themes/spaceship.zsh-theme" 
```

Set `ZSH_THEME="spaceship"` in your `.zshrc`.

```zsh
nano ~/.zshrc
```
```zsh
ZSH_THEME="spaceship"
```

### Plugins ZSH
- zsh-autosuggestions (https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md)
```zsh
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

- zsh-syntax-highlighting (https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md)
```zsh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

- File `.zshrc`
```zsh
plugins=(git
  colored-man-pages
  colorize
  bundler
  rake
  ruby
  zsh-autosuggestions
  zsh-syntax-highlighting)
```

### Alias (`.zshrc`)
```zsh
alias gc="git commit -m"
alias gs="git status"
alias fs="foreman start"
alias rs="rails server"
alias fds="make run"
```

### Variables
```zsh
export RAILS_ENV="development"
export PORT='3001'
export EDITOR='code'
```

## 3) Instalando dependências básicas
```zsh
sudo apt-get install build-essential git curl net-tools jpegoptim optipng imagemagick libmagickwand-dev unattended-upgrades patch zlib1g-dev liblzma-dev postgresql-client libpq-dev mysql-client libmysqlclient-dev
```

## 4) Instalando o Git

Para instalar o Git, basta execute o comando sudo apt-get install git. Depois de instalado, será necessário configurar os dados que serão utilizados na hora que você for fazer um commit.

```zsh
git config --global user.name 'Elias Ferreira Junior'
git config --global user.email eliaswebdev@gmail.com
```

Para listar as configurar instaladas, execute o comando git config -l.

```zsh
git config -l
```

Resultado esperado:
```zsh
user.name=Elias Ferreira Junior
user.email=eliaswebdev@gmail.com
```

## 5) Instalando o Ruby com RVM (http://rvm.io/)

### Install GPG2: 
```zsh
sudo apt install gnupg2
```

### Install GPG keys: 
```zsh
gpg2 --keyserver keyserver.ubuntu.com --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
```

### Install RVM: 
```zsh
\curl -sSL https://get.rvm.io | bash -s stable
```

### For installing RVM with default Ruby and Rails in one command, run: 
```zsh
\curl -sSL https://get.rvm.io | bash -s stable --rails
```

### Recarregue seu zshrc
```zsh
source ~/.zshrc
```
### Instalando versões antigas do ruby com rvm
```zsh
rvm pkg install openssl
```

```zsh
rvm install ruby-2.7.1 --with-openssl-dir=$HOME/.rvm/usr
```

### Instalando versões antigas do ruby com rvm - v2

```zsh
wget http://archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2.20_amd64.deb
wget http://security.ubuntu.com/ubuntu/pool/main/o/openssl/openssl_1.1.1f-1ubuntu2.20_amd64.deb
wget http://security.ubuntu.com/ubuntu/pool/main/o/openssl/libssl-dev_1.1.1f-1ubuntu2.20_amd64.deb

sudo dpkg -i libssl1.1_1.1.1f-1ubuntu2.20_amd64.deb
sudo dpkg -i libssl-dev_1.1.1f-1ubuntu2.20_amd64.deb
sudo dpkg -i openssl_1.1.1f-1ubuntu2.20_amd64.deb
```
```zsh
rvm install ruby-2.7.1 --with-openssl-dir=/usr/local/ssl
```

## 6) Instalando o Node, Yarn e NVM
Go to https://github.com/nodesource/distributions/blob/master/README.md

### NVM
- Link: https://github.com/nvm-sh/nvm#installing-and-updating
- https://github.com/nvm-sh/nvm?tab=readme-ov-file#installing-and-updating
  
- Install
```zsh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

- add ~/.zshrc
```zsh
# NVM
export NVM_DIR="$HOME/.nvm"
[ -s "/usr/local/opt/nvm/nvm.sh" ] && . "/usr/local/opt/nvm/nvm.sh"  # This loads nvm
[ -s "/usr/local/opt/nvm/etc/bash_completion.d/nvm" ] && . "/usr/local/opt/nvm/etc/bash_completion.d/nvm"  # This loads nvm bash_completion

autoload -U add-zsh-hook
load-nvmrc() {
  local node_version="$(nvm version)"
  local nvmrc_path="$(nvm_find_nvmrc)"

  if [ -n "$nvmrc_path" ]; then
    local nvmrc_node_version=$(nvm version "$(cat "${nvmrc_path}")")

    if [ "$nvmrc_node_version" = "N/A" ]; then
      nvm install
    elif [ "$nvmrc_node_version" != "$node_version" ]; then
      nvm use
    fi
  elif [ "$node_version" != "$(nvm version default)" ]; then
    echo "Reverting to nvm default version"
    nvm use default
  fi
}
add-zsh-hook chpwd load-nvmrc
load-nvmrc
#NVM
```

- Recarregue seu zshrc

```zsh
source ~/.zshrc
```

- Install Node

```zsh
nvm install node
```

### Yarn
```zsh
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
```

```zsh
sudo apt update && sudo apt install --no-install-recommends yarn
```

## 7) PostgreSql

```zsh
sudo apt-get install postgresql postgresql-contrib libpq-dev
```

Para que seja mais simples gerenciar os bancos de dados de desenvolvimento, crie um usuário no PostgreSQL com o mesmo nome do seu usuário Ubuntu, no exemplo abaixo $USER.

```zsh
sudo -u postgres createuser -rds $USER
```

Depois, crie um banco de dados com o mesmo nome de seu usuário.
```zsh
createdb $USER
```

```zsh
$ psql
psql (12.4.2)
Type "help" for help.

elias=#
```

```zsh
su postgres
psql -d template1 -U postgres

create database <database>;
create user <user> with password '<password>';
grant all privileges on database <database> to <user>;
```

## 8) MySQL
```zsh
sudo apt-get install mysql-client mysql-server libmysqlclient-dev
```

mude para root e crie um usuário para o banco

```zsh
sudo su
```

```zsh
mysql
```

```zsh
CREATE USER 'dev'@'%' IDENTIFIED BY 'root@123';
GRANT ALL ON *.* TO 'dev'@'%';
```

## 9) Redis
```zsh
sudo apt install redis-tools
```

```zsh
sudo apt install redis-server
```
ou 

```zsh
sudo snap install redis
```

### testando
```zsh
redis-cli
```

```zsh
127.0.0.1:6379> ping
PONG
```

## Extras:
### Github keygen:
```zsh
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

### Fix ssh agent
```zsh
eval "$(ssh-agent)"
ssh-add -l
ssh-add ~/.ssh/id_rsa
```
