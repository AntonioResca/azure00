# azure00


per installare:

cd

git clone https://github.com/AntonioResca/azure00.git

cd azure00

source install.sh

a questo punto crea una directory generica (es: django-projects) e una sottodirectory per ogni repository:

mkdir -p ~/django-projects/{primo,secondo}

ora clona i repository dei tuoi progetti

git clone <URL_REPO_PRIMO> ~/django-projects/primo

git clone <URL_REPO_SECONDO> ~/django-projects/secondo

ogni repository deve contenere una copia del Dockerfile (che ovviamente può essere modificato)

copia nella directory principale (~/django-projects) il file docker-compose.yml

ora modifica la configurazione di apache

sudo nano /etc/apache2/sites-available/000-default.conf

aggiungendo in fondo:

    <VirtualHost *:80>
        ServerName yourdomain.com

        ProxyPass /primo http://127.0.0.1:8001/
        ProxyPassReverse /primo http://127.0.0.1:8001/

        ProxyPass /secondo http://127.0.0.1:8002/
        ProxyPassReverse /secondo http://127.0.0.1:8002/
    </VirtualHost>

riavvia per rendere effettiva la nuova configurazione

sudo service apache2 restart

fai partire i container:

cd ~/django-projects

docker-compose up -d
