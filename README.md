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

## O shell script
#!/bin/bash  
####################################  
#  
# Backup to NFS mount script.  
#  
####################################  
    
# What to backup.  
backup_files="/home /var/spool/mail /etc /root /boot /opt"  
    
# Where to backup to.  
dest="/mnt/backup"  
    
# Create archive filename.  
day=$(date +%A)  
hostname=$(hostname -s)  
archive_file="$hostname-$day.tgz"  
    
# Print start status message.  
echo "Backing up $backup_files to $dest/$archive_file"  
date  
echo  
    
# Backup the files using tar.  
tar czf $dest/$archive_file $backup_files  
    
# Print end status message.  
echo  
echo "Backup finished"  
date  
    
# Long listing of files in $dest to check file sizes.  
ls -lh $dest  

## Habilite a nova configuração
*sudo systemctl restart smbd.service nmbd.service*

