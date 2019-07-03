# Teste Back End 2019 #

O teste consiste em criar uma mini API Rest utilizando Laravel como framework PHP, JWT como autenticação e um simples CRUD.
Aqui na DIN DIGITAL nós costumamos trabalhar o desenvolvimento utilizando Docker como ambiente local ([Laradock](https://laradock.io/)), então este repositório já está preparado para configurar a instância, basta possuir os [requisitos de software](#software-requirements) e executar o [comando de configuração automática do ambiente](#automatic-setup)

<a name="software-requirements"></a>
## Requisitos de software para o ambiente ##
- Algum terminal de comandos
- [Docker](https://www.docker.com/get-started)
- [Docker-compose](https://docs.docker.com/compose/install/)

<a name="automatic-setup"></a>
## Comando para configuração automática do ambiente ##
Copie o bloco de commandos abaixo e cole num terminal dentro de sua pasta de projetos
OBS: Este commando inclui o próprio git clone
No final você terá um ambiente LAMP e um Laravel 5.8, pronto para ser trabalhado, dentro da pasta site.

```shell
echo -e "\033[1;92m Clonando...\033[m" &&\
git clone git@github.com:dindigital/teste-back-end-2019.git &&\
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

## Requisitos de desenvolvimento ##
- [Postman](https://www.getpostman.com/downloads/) - Utilizar esta documentaçao: https://documenter.getpostman.com/view/2284246/S1a8yjgh?version=latest
- Utilizar biblioteca: [Laravel Responder](https://github.com/flugger/laravel-responder)
- Utilizar biblioteca: [JWT 1.0.0-rc.4.1](https://jwt-auth.readthedocs.io/en/develop/laravel-installation/) 

## O que será avalidado ##
- Funcionar o ambiente docker
- Ao abrir a collection do Postman, temos 4 rotas (referentes a Autenticação) com exemplos de como devem funcionar (inputs/outputs). Desenvolver essas rotas de forma que ao executá-las no Postman, os resultados sejam exibidos conforme o descrito na doc.
- Criar 4 rotas **privadas** referentes à um CRUD de produtos. As informações poderão ser: "Nome", "Preço", "Peso".
- Atualizar a documentação do Postman
- Enviar por e-mail o link de seu fork (não precisa criar PR) junto com o link de sua documentação do Postman
- Obrigado e boa sorte =)
