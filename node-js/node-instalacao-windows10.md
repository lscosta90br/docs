# Instalando NODE no Windows 10

## Tirando restricao de rodar powershell no windows 10

Verificando se o powershel esta restritivo para rodar scripts
```
PS C:\> Get-ExecutionPolicy
Restricted
```

Liberando o powershel rodar scripts sem restricao
```
PS C:\> Set-ExecutionPolicy Unrestricted

Alteração da Política de Execução
A política de execução ajuda a proteger contra scripts não confiáveis. A alteração da política de execução pode
implicar exposição aos riscos de segurança descritos no tópico da ajuda about_Execution_Policies em
https://go.microsoft.com/fwlink/?LinkID=135170. Deseja alterar a política de execução?
[S] Sim  [A] Sim para Todos  [N] Não  [T] Não para Todos  [U] Suspender  [?] Ajuda (o padrão é "N"): s

PS C:\> Get-ExecutionPolicy
Unrestricted
```

## Instalando Chocolatey via PoweShell como admistrator


```
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```
Referências:
    https://chocolatey.org/install#install-with-cmdexe
    
## Instalando node.js via PoweShell como admistrator

Instalando:
```
PS C:\> cinstall nodejs.install --version 10.16.1
```

Verificando se foi instalando:
```
rem verificar se foi instalado:
rem obs: precisa abrir uma nova seção do powershell

PS C:\> node -v
v10.16.1

PS C:\> npm -v
6.9.0
```

## Instalado o yarn no Windows 10

baixando o pacote no site: https://yarnpkg.com/lang/pt-br/docs/install/#windows-stable
ou 
fazer a instalação utilizando o chocolatey
```
PS C:\> choco install yarn
Chocolatey v0.10.15
Installing the following packages:
yarn
By installing you accept licenses for the packages.
Progress: Downloading yarn 1.17.3... 100%

yarn v1.17.3 [Approved]
yarn package files install completed. Performing other installation steps.
The package yarn wants to run 'chocolateyinstall.ps1'.
Note: If you don't run this script, the installation will fail.
Note: To confirm automatically next time, use '-y' or consider:
choco feature enable -n allowGlobalConfirmation
Do you want to run the script?([Y]es/[A]ll - yes to all/[N]o/[P]rint): y

Downloading yarn
  from 'https://yarnpkg.com/downloads/1.17.3/yarn-1.17.3.msi'
Progress: 100% - Completed download of C:\Users\Cybelle\AppData\Local\Temp\chocolatey\yarn\1.17.3\yarn-1.17.3.msi (1.57 MB).
Download of yarn-1.17.3.msi (1.57 MB) completed.
Hashes match.
Installing yarn...
yarn has been installed.

rem verificar se foi instalado:
rem obs: precisa abrir uma nova seção do powershell
PS C:\WINDOWS\system32> yarn -v
1.17.3
```










