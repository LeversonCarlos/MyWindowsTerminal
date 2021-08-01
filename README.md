# Introdução
Apenas um local para eu me lembrar como reconfigurar meu windows terminal do jeito que gosto e preciso. 

- [Powershell](./powershell/readme.md)
- [Git](./git/readme.md)

# Oh-My-Posh
O [Oh-My-Posh](https://ohmyposh.dev) é um engine de temas para o prompt, criado sob inspiração do [Oh-My-Zsh](https://ohmyz.sh).  

Instalaremos o módulo com o comando:
```ps1
Install-Module oh-my-posh -Scope CurrentUser
``` 

E vamos ativá-lo, editando o perfil com: `code $PROFILE` e adicionar a seguinte linha:
```ps1
Import-Module oh-my-posh -DisableNameChecking
```

Uma série de [temas](https://github.com/JanDeDobbeleer/oh-my-posh/tree/main/themes) serão disponibilizados e podem ser consultados com o comando:  
```ps1
Get-PoshThemes
```

Para ativar o tema desejado (agnoster, no exemplo), edite o perfil com: `code $PROFILE` e adicione a seguinte linha:
```ps1
Set-PoshPrompt -Theme agnoster
```

Adicionalmente, poderíamos seguir a [documentação](https://ohmyposh.dev/docs/configure) e escrever um tema personalizado. Eu tomei o tema paradox como exemplo, fiz pequenos ajustes e disponibilizei [aqui](./themes/custom-paradox.omp.json). Para ativá-lo devemos mencionar o caminho completo, por exemplo:
```ps1
Set-PoshPrompt -Theme Set-PoshPrompt -Theme c:\MyWindowsTerminal\themes\custom-paradox.omp.json
```


# Mensagem de apresentação
Novas instâncias do powershell são apresentadas com as boas vindas do powershell. Prefiro limpar a tela e apresentar algumas instruções que podem ser mais úteis como no exemplo abaixo. Para isso, editar o perfil com: `code $PROFILE`, e acrescentar as seguintes linhas:
```ps1
cd \Sources
Clear-Host
Write-Host 'PowerShell:'
Write-Host ' => '($PSVersionTable.PSVersion.Major,$PSVersionTable.PSVersion.Minor,$PSVersionTable.PSVersion.Patch -join ".")
Write-Host 'Profile:'
Write-Host ' => code $PROFILE'
Write-Host "Themes:"
Write-Host ' => Get-PoshThemes'
Write-Host ''
``` 


# Windows Terminal

<img src="./images/windows-terminal.gif" title="Windows Terminal" width="280" align="right" /> 

Por fim vamos falar do Windows Terminal, que é uma especie de IDE agregadora de terminais. Com ele é possível abrir múltiplas abas de terminais distintos como o *Command Prompt* e o próprio *Powershell*, além dos ambientes linux com o *WSL*. Instale o Windows Terminal através desse [link](https://www.microsoft.com/store/productId/9N0DX20HK701) da Windows Store.  

## Background
Pra definir uma imagem, com transparência, como fundo da tela, abra as configurações do windows terminal com `ctrl`+`,` e adicione as seguintes tags ao perfil desejado: 
```json 
   "backgroundImage": "ms-appdata:///roaming/Matrix1920.gif",
   "backgroundImageOpacity": 0.15,
   "backgroundImageStretchMode": "uniformToFill",
```

A imagem a ser usada para o fundo precisa ser disponibilizada dentro do *sandbox* em que o windows terminal tem acesso e é descrita por esse prefixo `ms-appdata:///roaming/`.  
Copie a imagem disponibilizada [aqui](./backgrounds/Matrix1920.gif) (ou a sua imagem de preferência), para a seguinte pasta: `%LOCALAPPDATA%\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\RoamingState`.   


## Fonte
Vamos precisar de uma fonte que tenha suporte a *glyphos* e *ligaduras*. O portal [NerdFonts](https://www.nerdfonts.com) possui uma boa biblioteca de fontes com diversas opções. Eu costumo alternar entre essas: 
- [FiraCode NF](https://github.com/ryanoasis/nerd-fonts/releases/download/v2.1.0/FiraCode.zip)
- [MesloLGSDZ NF](https://github.com/ryanoasis/nerd-fonts/releases/download/v2.1.0/Meslo.zip)  
- [Cascadia Code PL](https://github.com/microsoft/cascadia-code)

Basta fazer o download, abrir o pacote, clicar com o botão direito e selecionar *instalar*.  

Para ativar, abra as configurações do windows terminal com `ctrl`+`,` e adicione a seguinte tag ao perfil desejado (ou na sessão `defaults` para refletir a todos os perfis):
``` json
   "fontFace":  "FiraCode NF"
```


# Linux no Windows

## Ativar o Linux
Para ativar o subsistema linux para windows, basta seguir o [tutorial oficial](https://docs.microsoft.com/pt-br/windows/wsl/install-win10), mas basicamente iremos:
- Usando o menu iniciar, pesquisar por `ativar ou desativar recursos do windows`
- Marcar as opções `plataforma de máquina virtual` e `subsistema do windows para linux`
- Após instalação desses recursos, atualizar o wsl1 para wsl2 com [esse pacote de atualização](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi), ou [consultar a 4a etapa](https://docs.microsoft.com/pt-br/windows/wsl/install-win10#step-4---download-the-linux-kernel-update-package) do tutorial para outras opções.
- Definir a versão padrão do wsl para o wsl2 com o seguinte comando: 
  ```ps1
  wsl --set-default-version 2
  ```
- Será possível conferir a versão corrente com o seguinte comando:
  ```ps1
  Get-ItemPropertyValue `
     -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\Lxss `
     -Name DefaultVersion
  ``` 
- Instalar [uma das distribuição linux](https://aka.ms/wslstore) através da loja. Os próximos passos levarão em conta o Ubuntu
- Utilizando o menu iniciar, executar a primeira vez a distribuição instalada para concluir o processo
  - Será criado usuário com senha
  - Será criado perfil no windows terminal

## Zsh
- Abrir sua sessão do ubuntu pelo windows terminal
- Atualizar lista de pacotes e instalar o shell zsh com os comandos:
  ```bash
  sudo apt update
  sudo apt install zsh
  ```
- Definir o zsh como o shell padrão com:
  ```bash
  chsh -s $(which zsh)
  ```  
- Fechar a sessão e reabrir, selecionando a opção `2` para popular os arquivos de configuração com valores padrão

## Oh-My-Zsh
- Instalar o plugin com o comando:
  ```bash
  sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
  ```
- Defir o [tema desejado](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes) editando o arquivo de configurações do zsh com:
  ```bash
  nano ~/.zshrc
  ```  
- Substituir `ZSH_THEME="robbyrussell"` por (por exemplo) `ZSH_THEME="agnoster"`
- Para não apresentar o segmento usuario@hostName no prompt, defina o usuário corrente como _usuário padrão_ acrescentando a seguinte linha ao final do arquivo:
  ```bash
  DEFAULT_USER=$USER
  ```
- Sair gravando as mudanças com `ctrl`+`x`

## Diretório Inicial
- Mover para a pasta raiz com:
  ```bash
  cd /
  ```
- Criar diretório `sources` (ou o que preferir) com:
  ```bash
  sudo mkdir sources
  ```  
- Modificar o proprietário do diretório `sources` para seu usuário (lcjohnny no meu caso) com:
  ```bash
  sudo chown lcjohnny /sources
  ```  
- Editar o arquivo de configurações do zsh com:
  ```bash
  nano ~/.zshrc
  ```  
- Mover até o final do arquivo e acrescentar a linha:  
  ```bash
  cd /sources
  ```  
- Sair gravando as mudanças com `ctrl`+`x`

## Mensagem de apresentação
- Editar o arquivo de configurações do zsh com:
  ```bash
  nano ~/.zshrc
  ```  
- Mover até o final do arquivo e acrescentar as seguintes linhas (ou algo mais pertinente):  
  ```bash
  echo 'Profile:'
  echo ' => nano ~/.zshrc'
  echo ''
  ```  
- Sair gravando as mudanças com `ctrl`+`x`
