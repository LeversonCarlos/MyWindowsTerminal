# Powershell Settings
Apenas um local para eu me lembrar como reconfigurar meu powershell do jeito que gosto sempre que preciso. 


## Powershell Core
O Windows 10 já possui o Powershell 5.1 instalado por padrão e isso, via de regra, seria suficiente. Porém o powershell foi re-escrito como uma ferramenta opensource e multiplataforma, chamado agora de [Powershell Core](https://github.com/PowerShell/PowerShell). A forma mais fácil de instalá-lo é através da [Microsoft Store](https://www.microsoft.com/store/productId/9MZ1SNWT0N5D), com isso as atualizações serão aplicadas automaticamente. 


## Git
Fazer o download e executar o pacote de instalação através do [site oficial](https://git-scm.com). Logo após, registrar o usuário e email que será associado aos commits com os seguintes comandos:
```ps1 
git config --global user.name "Seu Nome"
git config --global user.email "seuEmail@seuProvedor.com"
```
### Git Credential Manager
A instalação do [visual studio](https://visualstudio.microsoft.com/pt-br) já fará a instalação do [Git Credential Manager](https://github.com/Microsoft/Git-Credential-Manager-for-Windows) que será responsável pela autenticação nos repositórios.  
O processo deverá acontecer automaticamente ao fazer o primeiro `git push`, solicitando autenticação através do navegador.


## Git Aliases
Esse módulo vai prover aliases para comandos Git baseados no pluging [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/git).  
Rode o seguinte comando para instalar o módulo no powershell: 
```ps1
Install-Module -Name git-aliases
```
Para ativar o módulo, editar seu perfil com: `code $PROFILE` e adicionar a seguinte linha:
```ps1
Import-Module git-aliases -DisableNameChecking
```
Posteriormente, para atualizar o módulo quando houver atualizações, rode o comando:
```ps1
Update-Module git-aliases
```
### Aliases
Abaixo, alguns dos aliases que serão disponibilizados. A lista completa pode ser consultada no [repositório do plugin](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/git).
| Alias                | Command                                                                                                                          |
|:---------------------|:---------------------------------------------------------------------------------------------------------------------------------|
| g                    | git                                                                                                                              |
| ga                   | git add                                                                                                                          |
| gb                   | git branch                                                                                                                       |
| gbl                  | git blame -b -w                                                                                                                  |
| gc                   | git commit -v                                                                                                                    |
| gcmsg                | git commit -m                                                                                                                    |
| gco                  | git checkout                                                                                                                     |
| gcm                  | git checkout $(git_main_branch)                                                                                                                |
| gcd                  | git checkout develop                                                                                                             |
| gd                   | git diff                                                                                                                         |
| gdw                  | git diff --word-diff                                                                                                             |
| gf                   | git fetch                                                                                                                        |
| gfa                  | git fetch --all --prune                                                                                                          |
| gfo                  | git fetch origin                                                                                                                 |
| gl                   | git pull                                                                                                                         |
| ggl                  | git pull origin $(current_branch)                                                                                                |
| gp                   | git push                                                                                                                         |
| ggp                  | git push origin $(current_branch)                                                                                                |
| gpsup                | git push --set-upstream origin $(git_current_branch)                                                                             |
| glg                  | git log --stat                                                                                                                   |
| glo                  | git log --oneline --decorate                                                                                                     |
| glog                 | git log --oneline --decorate --graph                                                                                             |
| gloga                | git log --oneline --decorate --graph --all                                                                                       |
| gm                   | git merge                                                                                                                        |
| grb                  | git rebase                                                                                                                       |
| gss                  | git status -s                                                                                                                    |
| gst                  | git status                                                                                                                       |
| gts                  | git tag -s                                                                                                                       |



## Windows Terminal

<img src="./images/windows-terminal.gif" title="Windows Terminal" width="280" align="right" /> 

Primeiro vamos falar do Windows Terminal, que é uma especie de IDE agregadora de terminais. Com ele é possível abrir múltiplas abas de terminais distintos como o *Command Prompt* e o próprio *Powershell*, além dos ambientes linux com o *WSL*. Instale o Windows Terminal através desse [link](https://www.microsoft.com/en-us/p/windows-terminal-preview/9n0dx20hk701?activetab=pivot:overviewtab) da Windows Store.  

### Background
Pra definir uma imagem, com transparência, como fundo da tela, abra as configurações do windows terminal com `ctrl`+`,` e adicione as seguintes tags ao perfil desejado: 
```json 
   "backgroundImage": "ms-appdata:///roaming/Matrix1920.gif",
   "backgroundImageOpacity": 0.15,
   "backgroundImageStretchMode": "uniformToFill",
```

A imagem a ser usada para o fundo precisa ser disponibilizada dentro do *sandbox* em que o windows terminal tem acesso e é descrita por esse prefixo `ms-appdata:///roaming/`.  
Copie a imagem disponibilizada [aqui](./backgrounds/Matrix1920.gif) (ou a sua imagem de preferência), para a seguinte pasta: `%LOCALAPPDATA%\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\RoamingState`.   


## Posh-Git
O [posh-git](https://github.com/dahlbyk/posh-git) é um módulo do PowerShell que integra o *Git* ao Powershell provendo informações de status e contexto do Git que pode ser exibido diretamente no prompt de comando. Além de disponibilizar autocomplete para os comandos Git, nomes de branch, e muito mais.  

### Instalação 
Para instalar o módulo execute o seguinte comando:
``` powershell
Install-Module posh-git -Scope CurrentUser
```
Pode ser necessário autorizar pacotes vindos da *Galeria do Powershell*. Responda sim para que a instalação prossiga.  
Se voce receber um erro de *Install-Module* sobre o NuGet precisando interagir com *Repositório NuGet*, execute os comandos a seguir para inicializar o provedor de Nuget:
``` powershell
Install-PackageProvider NuGet -Force
Import-PackageProvider NuGet -Force
```

### Atualizações
Depois de instalado, você poderá sempre atualizar o módulo através do comando: 
``` powershell
Update-Module posh-git
``` 

### PSReadline
Se você estiver utilizando o Powershell Core, será preciso instalar o módulo [PSReadline](https://docs.microsoft.com/en-us/powershell/module/psreadline/?view=powershell-6&WT.mc_id=-blog-scottha) para poder customizar o ambiente do prompt de commando no Powershell. Isso pode ser feito através do comando:
``` powershell
Install-Module -Name PSReadLine -AllowPrerelease -Scope CurrentUser -Force -SkipPublisherCheck
``` 

## Oh-My-Posh
Até aqui já seria possível usufruir das funcionalidades que o posh-git traz e até mesmo escrever o seu prório *tema* para o prompt de comando seguindo a documentação. Mas para facilitar um pouco mais, vamos instalar o módulo [oh-my-posh](https://github.com/JanDeDobbeleer/oh-my-posh) que, basicamente, disponibiliza deversos desses temas, já prontos para uso. 

### Instalação
Instalaremos o módulo com o comando:
``` powershell
Install-Module oh-my-posh -Scope CurrentUser
``` 

## Profile
Sempre que abrir uma sessão do PowerShell, será preciso *ativar* os módulos que deseja usar, a saber o *posh-git* e/ou *oh-my-posh*. Para fazer essa ativação automaticamente, vamos editar o arquivo do seu perfil do Powershell e preencher com os comandos que desejamos executar sempre que iniciarmos uma sessão. 

### Editar o Perfil
Vamos abrir o arquivo do perfil com o comando:
``` powershell
code $PROFILE
``` 
E então, simplesmente adicione as seguintes linhas:
``` powershell
Import-Module posh-git
Import-Module oh-my-posh
Set-Theme Paradox
``` 
Salve o arquivo e pronto. Novas sessões já serão inicializadas com os módulos carregados e o tema *Paradox* ativado. 

### Ajustar o Encoding
Quando começar a executar comandos git e visualizar logs de commits, possivelmente encontrará comentários utilizando acentuações. Para que o terminal os exiba corretamente, vamos editar novamente o arquivo do perfil com: `code $PROFILE`, e acrescentar a seguinte linha:
``` powershell
$env:LC_ALL='C.UTF-8'
``` 

### Ocultar o usuário
Por padrão o usuário corrente será exibido como parte do prompt de comando. Para ocultá-lo precisamos preencher a variável que indica quem é o usuário padrão. Os temas verificam se o usuário corrente for o definido nessa variável e em caso afirmativo não o exibe. Vamos editar mais uma vez o arquivo do perfil com: `code $PROFILE`, e acrescentar a seguinte linha:
``` powershell
$DefaultUser = '{substitua com o seu nome de usuário}'
``` 

### Definir mensagem
Por fim, para sempre começar com uma tela limpa vamos editar o perfil com: `code $PROFILE`, e acrescentar as seguintes linhas:
``` powershell
Clear-Host
Write-Host "Olá... foco no código"
``` 

## Fonte
Os temas utilizados podem precisar de uma fonte que tenha suporte a *glyphos* e *ligaduras*. Uma boa sugestão é a [Cascadia Code](https://github.com/microsoft/cascadia-code) que é opensource e tem o suporte necessário à *[Powerline](# https://docs.microsoft.com/pt-br/windows/terminal/tutorials/powerline-setup)*.  
Basta acessar a área de release do repositório e baixar a versão *Cascadia Code PL*. Adicionalmente estou disponibilizando [aqui](./fonts/CascadiaCodePL.ttf) a última versão que usei. Após baixar, clique na mesma com o botão direito e selecione *instalar*.  
Na sequencia, abra as configurações do windows terminal com `ctrl`+`,` e adicione a seguinte tag ao perfil desejado:
``` json
   "fontFace":  "Cascadia Code PL"
```

## Temas disponibilizados
Os temas disponíveis podem ser consultados [aqui](https://github.com/JanDeDobbeleer/oh-my-posh#themes).

#### Agnoster
![Agnoster Theme](https://github.com/JanDeDobbeleer/oh-my-posh/raw/master/img/agnoster.png)

#### Paradox
![Paradox Theme](https://github.com/JanDeDobbeleer/oh-my-posh/raw/master/img/paradox.png)

#### Sorin
![Sorin Theme](https://github.com/JanDeDobbeleer/oh-my-posh/raw/master/img/sorin.png)

#### Darkblood
![Darkblood Theme](https://github.com/JanDeDobbeleer/oh-my-posh/raw/master/img/darkblood.png)

#### Avit
![Avit Theme](https://github.com/JanDeDobbeleer/oh-my-posh/raw/master/img/avit.png)

#### Honukai
![Honukai Theme](https://github.com/JanDeDobbeleer/oh-my-posh/raw/master/img/honukai.png)

#### Fish
![Fish Theme](https://github.com/JanDeDobbeleer/oh-my-posh/raw/master/img/fish.png)

#### Robbyrussell
![Robbyrussell Theme](https://github.com/JanDeDobbeleer/oh-my-posh/raw/master/img/robbyrussel.png)

#### Pararussel
![Pararussel Theme](https://github.com/JanDeDobbeleer/oh-my-posh/raw/master/img/pararussel.png)

#### Material
![Material Theme](https://github.com/JanDeDobbeleer/oh-my-posh/raw/master/img/material.png)
![Material Theme](https://github.com/JanDeDobbeleer/oh-my-posh/raw/master/img/material2.png)

#### Star
![Star Theme](https://github.com/JanDeDobbeleer/oh-my-posh/raw/master/img/star.png)

#### Zash
![Star Theme](https://github.com/JanDeDobbeleer/oh-my-posh/raw/master/img/zash.png)

#### Lambda
![Lambda Theme](https://github.com/JanDeDobbeleer/oh-my-posh/raw/master/img/lambda.png)


## Tema Customizado
Os temas disponibilizados pelo módulo *oh-my-posh* nada mais são que um arquivo de script com instruções e comandos disponibilizados pelo módulo *posh-git*. Partindo como exemplo do tema [Honukai](https://github.com/JanDeDobbeleer/oh-my-posh/blob/master/Themes/Honukai.psm1) e seguindo a [documentação](https://github.com/dahlbyk/posh-git#git-status-summary-information), fiz algumas adequações para compor um tema que mais me agradasse e o estou disponibilizando [aqui](./themes/Elesse.psm1).  

### Ativação
Para ativar esse tema, editar o perfil com: `code $PROFILE` e mencionar o caminho completo onde o gravou, como:
``` powershell
Set-Theme C:\Sources\Personal\powershell-settings\themes\Elesse.psm1
```
Opcionalmente, seria possível disponibilizar esse tema na pasta de temas do *oh-my-posh* que normalmente se encontra em: `C:\Users\{seu nome de usuario}\Documents\PowerShell\Modules\oh-my-posh`


## Aliases para Comandos Git baseados nos aliases do plugin para zsh
No lugar de escrever e disponibilizar os aliases da forma descrita acima, uma alternativa seria utilizar os aliases já padronizados pelo pluging do [ohmyzsh](https://github.com/ohmyzsh/ohmyzsh). 
Para isso vamos instalar o módulo [powershell-git-aliases](https://github.com/gluons/powershell-git-aliases) com o seguinte comando:
   ``` powershell
   Install-Module git-aliases -Scope CurrentUser -AllowClobber
   ```
E vamos ativá-lo editando o perfil com: `code $PROFILE` e adicionando a seguinte linha:
   ``` powershell
   Import-Module git-aliases -DisableNameChecking
   ```

## Conclusão
Seu terminal não precisa ser boring.
