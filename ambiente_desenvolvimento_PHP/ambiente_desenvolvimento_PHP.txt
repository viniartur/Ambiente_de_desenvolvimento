#! /bin/bash
echo "          **********************************************************************************"
echo "          ** Bem vindo ao Script de configuração padrão para desenvolvimento PHP em Linux **"
echo "          **                                     Criado: por https://github.com/viniartur **"
echo "          **********************************************************************************"
echo
echo "Sinta-se a vontade para abrir o script com algum editor e verificar o codigo modificações, alterar"
echo " e dar sugestoes de mudanças no Github"
echo



echo "Seguindo com :"
echo " -->Instalando php"
echo "      *PHP 7.2"
echo "      *PHP cgi"
echo "      *PHP cli"
echo "      *PHP libapache2-mod-php"
echo "-->Instalando apache"
echo "      *Apache 2"
echo "-->Instalando Composer"
echo 
echo "Você deseja ver  detalhadamente o que vai ser instalado e alterado? "
echo "digite s para ver os topicos ou n para seguir com a configuração"
read topicos
if [ "$topicos" = "s" ]
    then
    echo " --> Atualização para o PHP mais recente "
fi
if [ "$topicos" = "n" ]
    then
    echo "vamos para a instalação padrão"
fi
echo
echo "      *** Apache ***"
apt install apache2
#systemctl status apache2
echo "      *** PHP 7.2***"
apt install php7.2
echo "      ***Modulos PHP**"
apt install php libapache2-mod-php
apt install php-cli
apt install php-cgi
apt install php-mysql
apt install php-pgsql
#systemctl restart apache2
apt install php7.2-mbstring 
#systemctl restart apache2
apt install php7.2-zip 
#systemctl restart apache2
apt install php7.2-gd
systemctl restart apache2
apt install php7.2-curl
echo "      ***Aplicando um Update no linux***"
apt update
echo
echo "Qual banco de dados você deseja instalar ? Digite m para mySQL ou p caso deseje instalar Postgres ou n para nenhum"
read banco
    if [ "$banco" = "m" ]
    then
    apt install mysql-server
    echo "A porta que o mySQL esta usando é:"
    ss -tap | grep mysql
    apt install mysql-workbench
    apt install phpmyadmin
    systemctl disable mysql
    apt install php7.2-imap
    apt update
fi
echo "por padrão uma workspace seré criada localizada em /var/www/html"
sudo chmod 777 /var/www/html -R
ls /var/www/html
apt install git
apt update
apt upgrade
apt autoremove
apt install php7.2-imap
pwd
EXPECTED_SIGNATURE="$(wget -q -O - https://composer.github.io/installer.sig)"
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
ACTUAL_SIGNATURE="$(php -r "echo hash_file('sha384', 'composer-setup.php');")"

if [ "$EXPECTED_SIGNATURE" != "$ACTUAL_SIGNATURE" ]
then
    >&2 echo 'ERROR: Invalid installer signature'
    rm composer-setup.php
    exit 1
fi

php composer-setup.php --quiet
RESULT=$?
rm composer-setup.php
exit $RESULT



     


     

