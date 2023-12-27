# Samba como servidor de arquivos
Desde 1992 o Samba é uma das maneiras mais comuns de compartilhamento de arquivos, diretórios, entre outros, com máquinas que rodam o Windows.

 *******
 
 ## Instale o Samba
*sudo apt install samba*

## Configure o Samba como um servidor de arquivos

Primeiro, edite o parâmetro **workgroup** na seção **[global] /etc/samba/smb.conf** e altere-o para melhor corresponder ao seu ambiente:

*workgroup = EXAMPLE*

Crie uma nova seção na parte inferior do arquivo ou remova o comentário de um dos exemplos para o diretório que deseja compartilhar:

O arquivo de configuração principal do Samba está localizado em **/etc/samba/smb.conf**

* *O arquivo de configuração **smb.conf** usado como exemplo está disponível [aqui](https://github.com/rafaelmotadasilva/samba-file-server/blob/main/smb.conf)*

## Habilite a nova configuração
*sudo systemctl restart smbd.service nmbd.service*

