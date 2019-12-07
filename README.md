# Valet & Magento 2
Steps for installing  &amp; using valet for Magento 2 development.

### Prerequisites
  - [Homebrew](https://brew.sh)
  - [Composer](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-macos)
  
## Valet Installation
Latest MacOs uses bin/zsh, this document tested on zsh based terminal. You can use on bin/bash too

```sh
$composer global require laravel/valet
$echo "export PATH=$PATH:$HOME/.composer/vendor/bin/" >> ~/.zshrc 
$valet install
$valet -v
```
## Valet Custom Folder Linking
Create your own folder whereever you want to place all projects which should run using Valet, enter into the folder and run valet park to create vatel symlinks

```sh
$mkdir valet-projects
$cd valet-projects
$valet park
```

To See all Paths, including above created valet-projects path, run command

```sh
$valet paths
```

## PHP & Mysql for Magento 2.3.3

```sh
$valet use php@7.3
$brew unlink php@7.3 && brew link --force php@7.3
$echo 'export PATH="/usr/local/opt/php@7.3/bin:$PATH"' >> ~/.zshrc 
$echo 'export PATH="/usr/local/opt/php@7.3/sbin:$PATH"' >> ~/.zshrc
$brew install mysql@5.7 
$brew services start mysql@5.7
$brew services list
$brew link --force mysql@5.7
$echo 'export PATH="/usr/local/opt/mysql@5.7/bin:$PATH"' >> ~/.zshrc
$mysql -uroot
mysql> create database magento233;
mysql> exit
```
Note: Please restart terminal session or open a new terminal window and test php & mysql

```sh
$php -v
$mysql -V
```
## Install Magento using Cli
##### Note: magento233 is the project name, valet will create domain magento233.test automatically

Run below commands one by one

```sh
$composer create-project --repository=https://repo.magento.com/ magento/project-community-edition magento233
$cd magento233
$valet link
$php -d memory_limit=-1 bin/magento setup:install --base-url=http://magento233.test/ \
--db-name=magento233 \
--admin-firstname=Kishore --admin-lastname=K \ --admin-email=kmyprojects@gmail.com \
--admin-user=admin --admin-password=Passwd.12! --language=en_GB \
--currency=GBP --timezone=Europe/London --use-rewrites=1
$php -d memory_limit=-1 bin/magento sampledata:deploy
$bin/magento s:up
$bin/magento de:mo:se developer
```

### Well Done. Your Magento 2 instance is ready for development.

Your local site is supposed to be ready here: 
http://magento233.test/

Moving forward, I will try to update this docuement with additional features like using Elastic Search, Redis.

##### Thank You -  [Chandravadana](https://www.linkedin.com/in/chandu-kandregula/)
