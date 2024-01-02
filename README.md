# Samba como servidor de arquivos

Uma das maneiras mais comuns de conectar computadores Ubuntu e Windows em rede é configurar o Samba como um *servidor de arquivos.* Pode ser configurado para compartilhar arquivos com clientes Windows, como veremos nesta seção.

O servidor será configurado para compartilhar arquivos com qualquer cliete da rede sem solicitar senha.

## Instale o Samba

O primeiro passo é instalar o pacote samba. Em um terminal, digite:

```
sudo apt install samba
```
Isso é tudo; agora você está pronto para configurar o Samba para compartilhar arquivos.

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

 * guest ok

 Permite que os clientes se conectem ao compartilhamento sem fornecer uma senha.

 * read only

 Determina se o compartilhamento é somente leitura ou se são concedidos privilégio de gravação. Os privilégios de gravação são permitidos somente quando o valor é *no*, como é visto neste exemplo. Se o valor for *yes*, o acesso ao compartilhamento será somente leitura.

 * create mask

 Determina as permissões que novos arquivos terão quando criados.