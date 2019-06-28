# Teste Back End 2019 #

## Abrindo o projeto pela primeira vez em ambiente local

Copie o bloco de código abaixo e cole num terminal dentro de sua pasta de jobs

```shell
echo -e "\033[1;92m Clonando repositório com recurse-submodules...\033[m" &&\
git clone git@github.com:dindigital/teste-back-end-2019.git --recurse-submodules &&\
echo -e "\033[1;92m Entrando na pasta do repositório clonado...\033[m" &&\
cd teste-back-end-2019 &&\
echo -e "\033[1;92m Entrando na pasta docker...\033[m" &&\
cd docker &&\
echo -e "\033[1;92m Buildando o docker...\033[m" &&\
docker-compose build &&\
echo -e -e "\033[1;92m Parando possíveis dockers abertos...\033[m" &&\
docker stop $(docker ps -a -q) &&\
echo -e "\033[1;92m Ligando o docker...\033[m" &&\
docker-compose up -d &&\
echo -e "\033[1;92m Criando arquivo .env...\033[m" &&\
ln -s ../site/.env.example ../site/.env &&\
echo -e "\033[1;92m Composer install...\033[m" &&\
docker-compose exec --user=laradock workspace sh -c "cd /var/www/site && composer -vvv install --no-scripts" &&\
while ! docker-compose exec mysql mysqladmin --user=root --password=root --host "127.0.0.1" ping --silent &> /dev/null ; do
    echo "Waiting for database connection..."
    sleep 2
done
echo -e "\033[1;92m Acesso Site: hhttp://localhost\033[m"
python -m webbrowser "http://localhost" > /dev/null 2>&1
```

