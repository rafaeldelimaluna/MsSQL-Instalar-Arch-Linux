# Com o gerenciador de pacotes: PAMAC
## Baixando / Instalando Pacotes
- `pamac install mssql-server`
- `pamac install mssql-tools`
- `pamac install odbc`
## Configurando
- `sudo /opt/mssql/bin/mssql-conf setup`;
- Insira: `systemctl status mssql-server --no-pager`, para verificar se o serviço está sendo executado corretamente;
### Caso queira utilizar sessões interativas
- `echo 'export PATH="$PATH:/opt/mssql-tools18/bin"' >> ~/.bash_profile`
- `echo 'export PATH="$PATH:/opt/mssql-tools18/bin"' >> ~/.bashrc`
- `echo 'export PATH="$PATH:/opt/mssql-tools18/bin"' >> ~/.<<seu interpretador (.zshrc, .bashrc ...>>`
# Configurando parte 2
- `sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true`
- `sudo systemctl restart mssql-server`
## Utilizando
- `sqlcmd -S localhost -U <user> -P <suaSenha>`
- Pode também omitir a senha, ficando: `sqlcmd -S localhost -U <user>`;
- O <user>, pode ser tanto o `sa`, quanto o usuario da máquina; tente ambos;
### caso encontre:
`Sqlcmd: Error: Microsoft ODBC Driver 18 for SQL Server : SSL Provider: [error:0A000086:SSL routines::certificate verify failed:self-signed certificate].`
`Sqlcmd: Error: Microsoft ODBC Driver 18 for SQL Server : Client unable to establish connection. For solutions related to encryption errors, see https://go.microsoft.com/fwlink/?linkid=2226722.`
- Remova a encriptação: `sqlcmd -No -S localhost -U <user>`
### Criando um Database
- `localhost -S localhost -U <user> -Q <Query>`
- Como exemplo: <Query> = 'CREATE DATABASE SampleDB'

# Configurações Adicionais
## Mudar a senha
- Entre no console sqlcmd (`sqlcmd -S localhost -P "suaSenha" -No`);
- utilize o comando `sp_password @new='nova_senha',@loginame='nome_da_conta'` e em seguida: `go`;
- Para sair do console, aplique: `exit`
*ATENÇÃO para @LOGINAME, não é LOGIN + NAME a justaposição dessas palavras e sim LOGIN + AME. Pode 
soar estranho, mas é um erro muito comum de acontecer, então escreva `@loginame` e não `@loginname`.*
