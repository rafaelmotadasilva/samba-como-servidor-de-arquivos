# Samba como servidor de arquivos

Uma das maneiras mais comuns de conectar computadores Ubuntu e Windows em rede é configurar o Samba como um *servidor de arquivos.*

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
[compartilhamento]
    comment = Compartilhamento
    path = /srv/samba/compartilhamento
    browsable = yes
    guest ok = yes
    read only = no
    create mask = 0755
 ```
 * comment
 Uma breve descrição do compartilhamento. Ajuste para atender às suas necessidades.

 * path
 O caminho para o diretório que você deseja compartilhar.

 >**Nota:**
 Este exemplo usa **/srv/samba/nome-de-compartilhamento** porque, de acordo com o *Filesystem Hierarchy Standard (FHS)*, **/srv** é onde os dados específicos do site devem ser servidos. Tecnicamente, os compartilhamentos do Samba podem ser colocados em qualquer lugar do sistema de arquivos, desde que as permissões estejam corretas, mas é recomendável aderir aos padrões.

 * browsable
 Permite que clientes Windows naveguem no diretório compartilhado usando o Windows Explorer.