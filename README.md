# Samba como servidor de arquivos
Desde 1992 , o Samba fornece serviços de arquivo e impressão seguros, estáveis ​​e rápidos para todos os clientes que usam o protocolo SMB/CIFS, como todas as versões de DOS e Windows, OS/2, Linux e muitos outros.

 *******
 
 ## Instale o Samba
*sudo apt install samba*

## Configure o Samba como um servidor de arquivos

Primeiro, edite o parâmetro **workgroup** na seção **[global] /etc/samba/smb.conf** e altere-o para melhor corresponder ao seu ambiente:

*workgroup = EXAMPLE*

Crie uma nova seção na parte inferior do arquivo ou remova o comentário de um dos exemplos para o diretório que deseja compartilhar:

O arquivo de configuração principal do Samba está localizado em **/etc/samba/smb.conf**

* *O arquivo de configuração **smb.conf** usado como exemplo está disponível [aqui](#)*

## Habilite a nova configuração
*sudo systemctl restart smbd.service nmbd.service*

