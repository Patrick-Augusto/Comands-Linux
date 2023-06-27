# Dio-Linux

Esta documentação contém informações sobre os scripts disponibilizados neste repositório do GitHub. Os scripts fornecidos são utilizados para automatizar tarefas de criação de usuários, configuração de diretórios, permissões e atualização de servidores.

## Scripts

### criar_user.sh

Este script cria usuários do sistema com suas respectivas senhas criptografadas. Os usuários são criados com nomes "guest10", "guest11", "guest12" e "guest13". Abaixo está o código-fonte do script:

```bash
#!/bin/bash

echo "Criando usuários do sistema...."

useradd guest10 -c "Usuário convidado" -s /bin/bash -m -p $(openssl passwd -crypt Senha123)
passwd guest10 -e

useradd guest11 -c "Usuário convidado" -s /bin/bash -m -p $(openssl passwd -crypt Senha123)
passwd guest11 -e

useradd guest12 -c "Usuário convidado" -s /bin/bash -m -p $(openssl passwd -crypt Senha123)
passwd guest12 -e

useradd guest13 -c "Usuário convidado" -s /bin/bash -m -p $(openssl passwd -crypt Senha123)
passwd guest13 -e

echo "Finalizado!!"
```

### iac1.sh

Este script cria diretórios e grupos de usuários no sistema. Além disso, cria usuários e atribui permissões aos diretórios. Os diretórios criados são "/publico", "/adm", "/ven" e "/sec". Os grupos criados são "GRP_ADM", "GRP_VEN" e "GRP_SEC". Abaixo está o código-fonte do script:

```bash
#!/bin/bash

echo "Criando diretórios..."

mkdir /publico
mkdir /adm
mkdir /ven
mkdir /sec

echo "Criando grupos de usuários..."

groupadd GRP_ADM
groupadd GRP_VEN
groupadd GRP_SEC

echo "Criando usuários..."

useradd carlos -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_ADM
useradd maria -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_ADM
useradd joao -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_ADM

useradd debora -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_VEN
useradd sebastiana -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_VEN
useradd roberto -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_VEN

useradd josefina -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_SEC
useradd amanda -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_SEC
useradd rogerio -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_SEC

echo "Especificando permissões dos diretórios...."

chown root:GRP_ADM /adm
chown root:GRP_VEN /ven
chown root:GRP_SEC /sec

chmod 770 /

adm
chmod 770 /ven
chmod 770 /sec
chmod 777 /publico

echo "Fim....."
```

### script-iac2.sh

Este script atualiza o servidor, instalando as atualizações disponíveis, o servidor Apache e o utilitário unzip. Em seguida, baixa e copia os arquivos de uma aplicação para o diretório "/var/www/html/". Abaixo está o código-fonte do script:

```bash
#!/bin/bash

echo "Atualizando o servidor..."
apt-get update
apt-get upgrade -y
apt-get install apache2 -y
apt-get install unzip -y

echo "Baixando e copiando os arquivos da aplicação..."

cd /tmp
wget https://github.com/denilsonbonatti/linux-site-dio/archive/refs/heads/main.zip
unzip main.zip
cd linux-site-dio-main
cp -R * /var/www/html/
```

## Como usar os scripts

1. Clone o repositório para sua máquina local:

```bash
git clone <url_do_repositório>
```

2. Navegue até o diretório do repositório clonado:

```bash
cd <nome_do_diretório>
```

3. Execute o script desejado:

```bash
./criar_user.sh
```

ou

```bash
./iac1.sh
```

ou

```bash
./script-iac2.sh
```

Certifique-se de fornecer as permissões adequadas aos scripts antes de executá-los:

```bash
chmod +x criar_user.sh
chmod +x iac1.sh
chmod +x script-iac2.sh
```

## Observações

- Certifique-se de ter os privilégios adequados para executar os scripts.
- Alguns comandos podem exigir privilégios de superusuário (root) para serem executados corretamente.
- Os scripts estão configurados com senhas fixas ("Senha123") para fins de demonstração. Certifique-se de alterar as senhas antes de usar em um ambiente de produção.
- Leia e entenda completamente o código dos scripts antes de executá-los para evitar problemas indesejados.
- Esta documentação foi criada com base no código fornecido até a data de corte do conhecimento desta IA (setembro de 2021). Certifique-se de verificar se houve alguma alteração nos comandos ou procedimentos desde então.
- Sempre faça backup dos dados importantes antes de executar scripts que possam modificar o sistema.
