# Deploy de projetos NodeJS utilizando chaves SSH e pm2 em VPS

## Teste e funcionamento em (até o momento):

- Google Cloud Platform (GCP)

## Requisitos

- Sistema Linux Ubuntu e derivados
- Repositório git/github
- PM2 (node_module)
- Chaves SSH (open-server-ssh)
- Nginx (proxy reverso)

(*) Seguir passos abaixo

## Como funciona:

Para acesso remoto, servidor faz o cruzamento de chaves SSH públicas e privadas configuradas pelo admin e apenas IPs/chaves validados conseguem fazer o acesso.

Para requisições HTTP/HTTPS, o Nginx funciona como o servidor web e proxy reverso, isto é, toda vez que o projeto for acessado via ip/domínio, o Nginx faz a tradução para o porta HTTP/HTTPS que foi configurado e redireciona para o /index do projeto.

## Configuração

### > Chaves SSH
- ssh-keygen -f ~/.ssh/<nome_da_chave> -t rsa -b 4096 (gerar par de chaves)
- cat ~/.ssh/<nome_da_chave>.pub (visualizar chave pública)
- ssh -i ~/.ssh/<nome_da_chave> <usuario_local>@<ip/dominio_do_server> (realizar acesso remoto)

### > Nginx
- sudo apt install nginx (instalação)
- cd /etc/nginx/sites-enabled (arquivos de configuração do proxy-reverso - vide arquivos)

### PM2
- sudo npm i -g pm2 (instalação)
- pm2 start /<dir_do_projeto>/server.js --name <nome_do_projeto>
- pm2 save (salva estado dos processos atuais)
- pm2 list (listagem de processos)
- pm2 startup (configura pm2 com inicialização do S.O.)