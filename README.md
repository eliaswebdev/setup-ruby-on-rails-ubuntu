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
sudo apt install build-essential git htop zsh
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

## 3) Instalando dependências básicas
```zsh
$ sudo apt-get install build-essential git curl net-tools jpegoptim optipng imagemagick libmagickwand-dev unattended-upgrades patch zlib1g-dev liblzma-dev postgresql-client libpq-dev mysql-client libmysqlclient-dev
```
## 4) Instalando o Git

Para instalar o Git, basta execute o comando sudo apt-get install git. Depois de instalado, será necessário configurar os dados que serão utilizados na hora que você for fazer um commit.

```zsh
$ git config --global user.name 'Elias Ferreira Junior'
$ git config --global user.email eliaswebdev@gmail.com
```

Para listar as configurar instaladas, execute o comando git config -l.

```zsh
$ git config -l
user.name=Elias Ferreira Junior
user.email=eliaswebdev@gmail.com
```
## 5) Instalando o Ruby com RVM (http://rvm.io/)

### Install GPG keys: 
```zsh
$ gpg2 --keyserver keyserver.ubuntu.com --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
```

### Install RVM: 
```zsh
$ \curl -sSL https://get.rvm.io | bash -s stable
```

### For installing RVM with default Ruby and Rails in one command, run: 
```zsh
$ \curl -sSL https://get.rvm.io | bash -s stable --rails
```

## 6) Instalando o Node e Yarn
Go to https://github.com/nodesource/distributions/blob/master/README.md

### Node.js v18.x:
```zsh
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - &&\
sudo apt-get install -y nodejs
```

### Yarn
```zsh
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
```
```zsh
sudo apt update && sudo apt install yarn
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

## 8) MySQL
```zsh
sudo apt-get install mysql-client mysql-server libmysqlclient-dev
```

mude para root e crie um usuário para o banco

```zsh
su root
```

```zsh
mysql
```

```zsh
CREATE USER 'dev'@'%' IDENTIFIED BY 'root@123';
GRANT ALL ON *.* TO 'dev'@'%';
```


```zsh

```


```zsh

```


```zsh

```


```zsh

```
