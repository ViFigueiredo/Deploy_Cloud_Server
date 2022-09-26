# Deploy de projetos NodeJS utilizando chaves SSH e pm2 em VPS

## Teste e funcionamento em (até o momento):

- GCP

## Requisitos

- Sistema Linux Ubuntu*
- Repositório git/github
- PM2 (node_module)
- Chaves SSH (open-server-ssh)
- Nginx (proxy reverso)
- Banco de dados*

(*) Seguir passos abaixo

## Como funciona:

Para acesso remoto, servidor faz o cruzamento de chaves SSH públicas e privadas configuradas pelo admin e apenas IPs/chaves validados conseguem fazer o acesso.

Para requisições HTTP/HTTPS, o Nginx funciona como o servidor web e proxy reverso, isto é, toda vez que o projeto for acessado via ip/domínio, o Nginx faz a tradução para o porta HTTP/HTTPS que foi configurado e redireciona para o /index do projeto.

## Configuração

### > Chaves SSH
- ssh-keygen -f ~/.ssh/<nome_da_chave> -t rsa -b 4096
- cat ~/.ssh/<nome_da_chave>.pub
- ssh -i ~/.ssh/<nome_da_chave> <usuario_local>@<ip/dominio_do_server> (acesso remoto)

### > Nginx