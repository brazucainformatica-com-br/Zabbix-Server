# Para instalar o Zabbix Server, siga os seguintes passos

Adicione o repositório Zabbix: Abra o terminal e execute o seguinte comando para adicionar o repositório Zabbix:

wget https://repo.zabbix.com/zabbix/5.4/ubuntu/pool/main/z/zabbix-release/zabbix-release_5.4-1+ubuntu20.04_all.deb

sudo dpkg -i zabbix-release_5.4-1+ubuntu20.04_all.deb

Atualize a lista de pacotes: Execute o seguinte comando para atualizar a lista de pacotes disponíveis:

sudo apt update

Instale o Zabbix Server: Execute o seguinte comando para instalar o Zabbix Server:

sudo apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-agent

Crie um banco de dados para o Zabbix: Execute os seguintes comandos para criar um banco de dados MySQL e um usuário para o Zabbix:

sudo apt install mysql-server

sudo mysql -u root -p

Digite a senha do root do MySQL quando solicitado, e depois execute os seguintes comandos dentro do MySQL:

create database zabbix character set utf8 collate utf8_bin;

create user 'zabbix'@'localhost' identified by 'senha';

grant all privileges on zabbix.* to 'zabbix'@'localhost';

quit;

Substitua 'senha' pela senha que você deseja atribuir ao usuário 'zabbix'.

Importe o esquema do banco de dados do Zabbix: Execute o seguinte comando para importar o esquema do banco de dados do Zabbix:

zcat /usr/share/doc/zabbix-server-mysql*/create.sql.gz | mysql -u zabbix -p zabbix

Digite a senha do usuário 'zabbix' quando solicitado.

Configure o Zabbix Server: Abra o arquivo de configuração do Zabbix Server:

sudo nano /etc/zabbix/zabbix_server.conf

Altere a seguinte linha para apontar para o banco de dados MySQL que você criou anteriormente:

DBPassword=senha
Substitua 'senha' pela senha que você atribuiu ao usuário 'zabbix'.

Reinicie o Zabbix Server e o Apache: Execute os seguintes comandos para reiniciar o Zabbix Server e o Apache:

sudo systemctl restart zabbix-server zabbix-agent apache2

sudo systemctl enable zabbix-server zabbix-agent apache2

Acesse a interface web do Zabbix: Abra um navegador da web e acesse a interface do Zabbix digitando o endereço do servidor seguido de "/zabbix" (por exemplo, http://endereco_do_servidor/zabbix). O assistente de configuração do Zabbix será exibido. Siga as instruções na tela para configurar o Zabbix.

Usuário e senha padrão para login na interface web:
Usuário: Admin
Senha: zabbix

Este é o passo a passo básico para instalar o Zabbix Server. Você pode personalizar a instalação de acordo com suas necessidades, consultando a documentação oficial do Zabbix em https://www.zabbix.com/documentation/current/manual/installation.
