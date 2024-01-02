# Samba como servidor de arquivos

Uma das maneiras mais comuns de conectar computadores UbuntLinux e Windows em rede é configurar o Samba como um *servidor de arquivos.*

## Instale o Samba

O primeiro passo é instalar o pacote samba. Em um terminal, digite:

```
sudo apt install samba
```
## Configure o Samba como um servidor de arquivos

O arquivo de configuração principal do Samba está localizado em **/etc/samba/smb.conf**.

Primeiro, edite o **workgroup** parâmetro na seção *[global]* **/etc/samba/smb.conf** e altere-o para melhor corresponder ao seu ambiente:

```
workgroup = EXEMPLO
```
Crie uma nova seção na parte inferior do arquivo ou remova o comentário de um dos exemplos para o diretório que deseja compartilhar:

```
[publica]
    comment = Pública
    path = /srv/samba/publica
    browsable = yes
    guest ok = yes
    read only = no
    create mask = 0755
 ```