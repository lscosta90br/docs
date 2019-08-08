# Configurando o VsCode no Windows 10

## Adicionado temas e extensions

Tema

* Dracula Oficial

Extensions

* Material Icon Theme

Extensions JS

* Rocketseat ReactJS
* Rocketseat React Native

## Terminal do zsh com tema dracula

``` code
https://blog.rocketseat.com.br/terminal-com-oh-my-zsh-spaceship-dracula-e-mais/
```

## Personalização de extensions

### Geral

```code
code --list-extensions
dracula-theme.theme-dracula
PKief.material-icon-theme

# Fonte utilizada:
# Fire code - https://github.com/tonsky/FiraCode

Configurando personalização
File / Preferences / Settings / settings.json
```

Personalizando fontes e configurações

```vscode
    // Configura tamanho e familia da fonte
    "editor.fontSize": 18,
    "editor.lineHeight": 24,
    "editor.fontFamily": "Fire Code" ,
    "editor.fontLigatures": true,

    // Aplicar linhas verticais para lembrar de quebrar linhas em códigos
    "editor.rulers": [80, 120],
    "editor.formatOnSave": false,
    "terminal.integrated.fontFamily": "Consolas, 'Courier New', monospace",
```

### Listar extensions JavaScript

```code
 code --list-extensions
rocketseat.RocketseatReactJS
rocketseat.RocketseatReactNative
```

### Instalando as extensions

```code
REM - GERAL
code --install-extension dracula-theme.theme-dracula
code --install-extension PKief.material-icon-theme

REM - JAVASCRIPT
code --install-extension rocketseat.RocketseatReactJS
code --install-extension rocketseat.RocketseatReactNative

REM - PYTHON e  DJANGO
code --install-extension cstrap.flask-snippets
code --install-extension eamodio.gitlens
code --install-extension formulahendry.code-runner
code --install-extension ms-python.anaconda-extension-pack
code --install-extension ms-python.python
code --install-extension redhat.vscode-yaml
code --install-extension shardulm94.trailing-spaces
code --install-extension thebarkman.vscode-djaneiro


# Customizacoes
code --install-extension CoenraadS.bracket-pair-colorizer
code --install-extension oderwat.indent-rainbow
code --install-extension ritwickdey.LiveServer

#Java script
code --install-extension dbaeumer.vscode-eslint
```

### Extensões que não estão instaladas

```code
# Marcacao para achar codigo
code --install-extension alefragnani.Bookmarks

# Django
code --install-extension baterson.copy-django-model-fields
code --install-extension batisteo.vscode-django
code --install-extension bibhasdn.django-snippets
code --install-extension bigonesystems.django
code --install-extension shamanu4.django-intellisense
code --install-extension victorzevallos.vscode-theme-django

#Java script
code --install-extension ChakrounAnas.turbo-console-log
code --install-extension streetsidesoftware.code-spell-checker
code --install-extension streetsidesoftware.code-spell-checker-portuguese-brazilian

# Python
code --install-extension donjayamanne.jupyter
code --install-extension donjayamanne.python-extension-pack
code --install-extension magicstack.MagicPython

#Git
code --install-extension eamodio.gitlens

# HTML CSS Support
code --install-extension ecmel.vscode-html-css

#outros
code --install-extension formulahendry.code-runner
code --install-extension jevakallio.vscode-hacker-typer
code --install-extension keesschollaart.vscode-home-assistant
code --install-extension Kelvin.vscode-sshfs
code --install-extension minhthai.vscode-todo-parser
code --install-extension lkytal.pomodoro
code --install-extension ms-vscode.cpptools
code --install-extension platformio.platformio-ide
code --install-extension rafaelmaiolla.remote-vscode
code --install-extension ritwickdey.live-sass
code --install-extension thekalinga.bootstrap4-vscode
code --install-extension wholroyd.jinja
code --install-extension wmaurer.change-case
code --install-extension Tyriar.shell-launcher
code --install-extension VisualStudioExptTeam.vscodeintellicode
code --install-extension vscode-icons-team.vscode-icons

#REST Client allows you to send HTTP request and view the response in Visual Studio Code directly.
code --install-extension humao.rest-client

```
