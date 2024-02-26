# Configurando o Samba como Servidor de Arquivos

O Samba facilita o compartilhamento de arquivos em redes com sistemas Ubuntu e Windows. Este guia demonstra como configurá-lo como servidor de arquivos no Ubuntu, permitindo acesso e compartilhamento de arquivos pelos clientes Windows.

## Visão Geral

Este guia oferece instruções passo a passo para configurar o Samba como servidor de arquivos em um ambiente Ubuntu. Ele abrange desde a instalação do pacote Samba até a configuração dos compartilhamentos de diretórios.

## Requisitos

* Sistema operacional Ubuntu instalado.
* Acesso ao terminal com privilégios de superusuário para executar comandos.

## Instruções

1. [Instalação do Samba](#instalação-do-samba)
2. [Configurando o Samba como Servidor de Arquivos](#configurando-o-samba-como-servidor-de-arquivos)
3. [Criando o Diretório Compartilhado](#criando-o-diretório-compartilhado)
4. [Ativando a Nova Configuração](#ativando-a-nova-configuração)
5. [Conclusão](#conclusão)

## Instalação do Samba

Comece instalando o pacote `samba`. Abra um terminal e digite o seguinte comando:

```
sudo apt install samba
```

## Configurando o Samba como Servidor de Arquivos

O arquivo de configuração principal do Samba está localizado em `/etc/samba/smb.conf`. Abra este arquivo em um editor de texto de sua preferência e ajuste as configurações conforme necessário. Aqui estão algumas configurações essenciais que você pode personalizar na seção *[global]*:

**workgroup**: Define o nome do grupo de trabalho.  
**security**: Define o nível de segurança do Samba.

Para compartilhar diretórios específicos, adicione seções no arquivo `smb.conf` para cada diretório desejado, conforme o exemplo abaixo:

```
[compartilhamento]
    comment = Descrição do Compartilhamento
    path = /srv/samba/compartilhamento
    browsable = yes
    guest ok = yes
    read only = no
    create mask = 0755
 ```

**comment**: Uma breve descrição do compartilhamento.  
**path**: O caminho para o diretório que você deseja compartilhar.  
**browsable**: Permite que clientes naveguem no diretório compartilhado usando o Windows Explorer.  
**guest ok**: Permite que os clientes se conectem ao compartilhamento sem fornecer uma senha.
**read only**: Determina se o compartilhamento é somente leitura ou se são concedidos privilégios de gravação.
**create mask**: Determina as permissões que novos arquivos terão quando criados.

 ### Criando o Diretório Compartilhado

Antes de reiniciar o serviço Samba, certifique-se de criar os diretórios que deseja compartilhar e ajustar as permissões. Use os seguintes comandos no terminal:

 ```
sudo mkdir -p /srv/samba/compartilhamento
sudo chown nobody:nogroup /srv/samba/compartilhamento
 ```

### Ativando a Nova Configuração

Após editar o arquivo `smb.conf` e criar o diretório compartilhado, reinicie os serviços Samba para aplicar as alterações:

```
sudo systemctl restart smbd.service nmbd.service
```

## Conclusão

Parabéns! Você configurou com sucesso o Samba como servidor de arquivos no seu Ubuntu. Agora, os clientes Windows na rede podem acessar e compartilhar arquivos conforme necessário.

## Contribuição

Se você tiver sugestões de melhorias ou correções para este guia, sinta-se à vontade para enviar uma pull request.

## Referências

* [Documentação oficial do Ubuntu: Configurando um Servidor de Arquivos com Samba](https://ubuntu.com/server/docs/samba-file-server)

## Licença

Este projeto está licenciado sob a Licença MIT.