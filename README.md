# Samba como servidor de arquivos
 Uma das maneiras mais comuns de compartilhamento de arquivos, diretórios, entre outros, com máquinas que rodam o Windows.

 *******
 
 ## Instale o Samba
*sudo apt install samba*

## Configure o Samba como um servidor de arquivos

Primeiro, edite o parâmetro **workgroup** na seção **[global] /etc/samba/smb.conf** e altere-o para melhor corresponder ao seu ambiente:

*workgroup = EXAMPLE*

Crie uma nova seção na parte inferior do arquivo ou remova o comentário de um dos exemplos para o diretório que deseja compartilhar:

O arquivo de configuração principal do Samba está localizado em **/etc/samba/smb.conf**

* [smb.conf](#)

*******

*[publica]*

   *comment = Pública*

   *path = /srv/samba/share/publica*

   *writable = yes*

   *guest ok = yes*

   *guest only = yes*

*[financeiro]*

   *comment = Financeiro*

   *path = /srv/samba/share/financeiro*

   *writable = yes*

   *valid users = @financeiro*

   *force group = financeiro*

   *directory mask = 0770*

   *create mask = 0770*

   *force directory mode= 0770*

   *force create mode= 0770*

*[suporte]*

   *comment = Suporte*

   *path = /srv/samba/share/suporte*

   *writable = yes*

   *valid users = @suporte*

   *force group = suporte*

   *directory mask = 0770*

   *create mask = 0770*

   *force directory mode= 0770*

   *force create mode= 0770*

*******

## Habilite a nova configuração
sudo systemctl restart smbd.service nmbd.service

