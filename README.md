# Samba como servidor de arquivos
Desde 1992 o Samba é uma das maneiras mais comuns de compartilhamento de arquivos, diretórios, entre outros, com máquinas que rodam o Windows.

<img align="right" src="SambaLogo.png">
 
 ## Instale o Samba
 O primeiro passo é instalar o samba. Em um terminal, digite:

*sudo apt install samba*

## Configure o Samba como um servidor de arquivos
Primeiro, edite o parâmetro **workgroup** na seção **[global]** em **/etc/samba/smb.conf** e altere-o para melhor corresponder ao seu ambiente:

*workgroup = EXAMPLE*

Crie uma nova seção na parte inferior do arquivo ou remova o comentário de um dos exemplos para o diretório que deseja compartilhar:

O arquivo de configuração principal do Samba está localizado em **/etc/samba/smb.conf**

* *O arquivo de configuração **smb.conf** usado como exemplo está disponível [aqui](https://github.com/rafaelmotadasilva/samba-file-server/blob/main/smb.conf)*

## Executando o script

O arquivo **samba-file-server.sh** deve ser tornado executável:

*chmod u+x samba-file-server.sh*

Em seguida, em um terminal, execute o seguinte comando:

*sudo ./samba-file-server.sh*

* *O arquivo de configuração **samba-file-server.sh** usado como exemplo está disponível [aqui](https://github.com/rafaelmotadasilva/samba-file-server/blob/main/samba-file-server.sh)*

## Habilite a nova configuração
*sudo systemctl restart smbd.service nmbd.service*