# Samba como servidor de arquivos

Uma das maneiras mais comuns de conectar computadores Ubuntu e Windows em rede é configurar o Samba como um *servidor de arquivos.* Pode ser configurado para compartilhar arquivos com clientes Windows, como veremos nesta seção.

O servidor será configurado para compartilhar arquivos com qualquer cliente da rede sem solicitar senha.

## Instale o Samba

O primeiro passo é instalar o pacote `samba`. Em um terminal, digite:

```
sudo apt install samba
```
Isso é tudo; agora você está pronto para configurar o Samba para compartilhar arquivos.

## Configure o Samba como um servidor de arquivos

O arquivo de configuração principal do Samba está localizado em `/etc/samba/smb.conf`.

Primeiro, edite o `workgroup` parâmetro na seção *[global]* `/etc/samba/smb.conf` e altere-o para melhor corresponder ao seu ambiente:

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
 * **comment**

 Uma breve descrição do compartilhamento. Ajuste para atender às suas necessidades.

 * **path**

 O caminho para o diretório que você deseja compartilhar.

 >**Nota**:
 
 Este exemplo usa `/srv/samba/nome-de-compartilhamento` porque, de acordo com o *Filesystem Hierarchy Standard (FHS)*, **/srv** é onde os dados específicos do site devem ser servidos. Tecnicamente, os compartilhamentos do Samba podem ser colocados em qualquer lugar do sistema de arquivos, desde que as permissões estejam corretas, mas é recomendável aderir aos padrões.

 * **browsable**

 Permite que clientes Windows naveguem no diretório compartilhado usando o Windows Explorer.

 * **guest ok**

 Permite que os clientes se conectem ao compartilhamento sem fornecer uma senha.

 * **read only**

 Determina se o compartilhamento é somente leitura ou se são concedidos privilégio de gravação. Os privilégios de gravação são permitidos somente quando o valor é *no*, como é visto neste exemplo. Se o valor for *yes*, o acesso ao compartilhamento será somente leitura.

 * **create mask**

 Determina as permissões que novos arquivos terão quando criados.

 ### Crie o diretório

 Agora que o Samba está configurado, o diretório precisa ser criado e as permissões alteradas. Em um terminal execute os seguintes comandos:

 ```
 sudo mkdir -p /srv/samba/compartilhamento
 sudo chown nobody:nogroup /srv/samba/compartilhamento
 ```
A opção `-p` informa ao `mkdir` para criar a árvore de diretórios inteira, se ela ainda não existir.

### Habilite a nova configuração

Por fim, reinicie os serviços Samba para habilitar a nova configuração executando o seguinte comando:

```
sudo systemctl restart smbd.service nmbd.service
```

A partir de um cliente Windows, agora você poderá navegar até o servidor de arquivos Ubuntu e ver o diretório compartilhado. Se o seu cliente não mostrar o seu compartilhamento automaticamente, tente acessar o seu servidor pelo seu endereço IP, por exemplo `\\192.168.1.1`, em uma janela do Windows Explorer. Para verificar se tudo está funcionando, tente criar um diretório no Windows.

Para compartilhamentos adicionais, basta criar novas seções *[nome-de-compartilhamento]* em `/etc/samba/smb.conf` e reiniciar o *Samba*. Apenas certifique-se que o diretório que você deseja compartilhar realmente exista e que as permissões estejam corretas.

O compartilhamento de arquivo denominado *[compartilhamento]* e o caminho `/srv/samba/nome-de-compartilhamento` neste exemplo podem ser ajustados para se adequar ao seu ambiente. É uma boa ideia nomear um compartilhamento com o nome de um diretório no sistema de arquivos.
