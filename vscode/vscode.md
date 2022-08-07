# Microsoft Visual Studio Code Map:

## Layout VSCode
![](https://github.com/lscosta90br/docs/blob/master/img/vsCode-layout.png)

## Tabela teclas de atalho VSCode

|  Recurso            | Combinação de teclas                  | Descrição                                     |
|---------------------|---------------------------------------|-----------------------------------------------|
| busca: arq. corrent | CTRL+F                                | busca no arquivo que esta em foco             |
| busca arq. solucao  | CTRL+P                                | buscar um arquivo dentro da solution          |
| copiar linha        | ALT+SHIFT+Seta cima/baixo             | duplica a linha                               |
| comentario bloco    | "Marcar o block", CTRL+;              | comenta um block                              |
| deleta linha        | CTRL+SHIFT+K                          | apaga linha do código                         |
| explorer: ir        | CTRL+ALT+E                            | Vai para o explorer do vs code                |
| Git: chama o git    | CTRL+SHIFT+G                          | vai para interface do git                     |
| mover linha         | ALT+Seta cima/baixo                   | mover linha entre cóodigo                     |
| navega: tabs        | CTRL+P (selecione tab)                | Navega entre arquivos do projeto              |
| seleção multipla    | CTRL+SHIFT+L                          | selecione um texto e depois utilize as teclas |
| seleção vertical    | SHIFT+ALT+MOUSE                       | seleção vertical no código                    |
| terminal: fechar    | CTRL+SHIFT+P (View: Close em Panel)   | fecha a janela do terminal                    |
| terminal: ir        | CTRL+SHIFT+P (View: Focus into Panel) | vai para seleção do terminal                  |
| terminal: ir        | CTRL+"                                | vai para terminal                             |
| todas opções        | CTRL+SHIFT+P                          | para executar qualquer comando via localizar  |
| Multi seleção       | CTRL+D                                | selecione uma palavra /depois pressione ctrl+D|
| Multi seleção total | CTRL+F2                               | selecione todas as palavras                   |
| Executa codigo      | Ctrl+Alt+N                            | executa codigo na console                     |



Uma outra opção é selecionar a palavra que quer, depois pressionar alt+D, cada vez que apertar alt+D ele vai selecionando essa palavra por todo seu projeto, ai depois é só digitar a nova que ele substitui em tudo.

No meu caso eu mudei o padrão do VSCode para ficar igual ao sublime text, troquei o ALT pelo CTRL. isso você faz nas configurações do VSCode

_tabela gerada pelo site_: http://www.tablesgenerator.com/markdown_tables

## Atalhos teclados:

| Recurso                | Combinação de teclas       | Descrição                  |
|------------------------|----------------------------|----------------------------|
| final de linha         | END                        | vai para o final da linha  |
| inicio da linha        | HOME                       | vai para o inicio da linha |
| navegar entre palavras | CTRL+seta esqu./dir.       | vai pulando entre palavras |
| selecao de palavras    | CTRL+SHIFT+setal esq./dir. | marca entre palavras       |
| apagar palavra         | CTRL+BACKSPACE             | apagar palavras            |
| indentação             | TAB                        | faz a indentação do texto  |
| tirar identação        | TAB+SHIFT                  | tira a indentação do texto |

_tabela gerada pelo site_: http://www.tablesgenerator.com/markdown_tables



# Configurações

## 1. Dicas:

1. Etapas para desativar o modo de visualização**

    **Critério**:

     * Se você quiser desabilitar o modo de visualização todos em uma unica tab, isto é:

     * acessando o arquivo através do menu lateral.
     * abrindo o menu aberto rápido usando Ctrl+ P.
  
     **Solução**:

     * Abra a Paleta de Comandos usando o atalho Ctrl+ Shift+ P.
     * Configurações. Pesquise workbench.editor.enablePreviewe desmarque a caixa de seleção. (as alterações são salvas automaticamente e indicadas com uma borda azul esquerda)
  
   **Adicional:**

     * Se você quiser desativar apenas o modo de visualização no menu de abertura rápida, desmarque a caixa para workbench.editor.enablePreview From QuickOpen.

## Comando para listar extensão:
```
#UNIX:
code --list-extensions | xargs -L 1 echo code --install-extension

#Windows
code --list-extensions | % { "code --install-extension $_" }
```

## Extensão que utilizo:
```
❯ code --list-extensions | xargs -L 1 echo code --install-extension
code --install-extension abdelaziz18003.quasar-snippets
code --install-extension alefragnani.Bookmarks
code --install-extension baterson.copy-django-model-fields
code --install-extension batisteo.vscode-django
code --install-extension bceskavich.theme-dracula-at-night
code --install-extension be5invis.toml
code --install-extension bibhasdn.django-snippets
code --install-extension bradlc.vscode-tailwindcss
code --install-extension codezombiech.gitignore
code --install-extension Dart-Code.dart-code
code --install-extension Dart-Code.flutter
code --install-extension dbaeumer.vscode-eslint
code --install-extension dracula-theme.theme-dracula
code --install-extension esbenp.prettier-vscode
code --install-extension formulahendry.code-runner
code --install-extension frenco.vscode-notion
code --install-extension GitHub.copilot
code --install-extension golang.go
code --install-extension Gruntfuggly.todo-tree
code --install-extension hollowtree.vue-snippets
code --install-extension IronGeek.vscode-env
code --install-extension jamiewoodio.cisco
code --install-extension johnpapa.winteriscoming
code --install-extension mechatroner.rainbow-csv
code --install-extension ms-azuretools.vscode-docker
code --install-extension MS-CEINTL.vscode-language-pack-pt-BR
code --install-extension ms-python.python
code --install-extension ms-python.vscode-pylance
code --install-extension ms-toolsai.jupyter
code --install-extension ms-toolsai.jupyter-keymap
code --install-extension ms-toolsai.jupyter-renderers
code --install-extension ms-vscode-remote.remote-containers
code --install-extension ms-vscode-remote.remote-ssh
code --install-extension ms-vscode-remote.remote-ssh-edit
code --install-extension Nash.awesome-flutter-snippets
code --install-extension octref.vetur
code --install-extension oderwat.indent-rainbow
code --install-extension Perkovec.emoji
code --install-extension philxor.iosxr
code --install-extension PKief.material-icon-theme
code --install-extension ritwickdey.LiveServer
code --install-extension rocketseat.theme-omni
code --install-extension samuelcolvin.jinjahtml
code --install-extension Shan.code-settings-sync
code --install-extension stuart.unique-window-colors
code --install-extension Tyriar.lorem-ipsum
code --install-extension vscode-icons-team.vscode-icons
code --install-extension wayou.vscode-todo-highlight
```

### Extensão simplificada:
```
code --install-extension CoenraadS.bracket-pair-colorizer
code --install-extension cstrap.flask-snippets
code --install-extension DavidAnson.vscode-markdownlint   
code --install-extension dbaeumer.vscode-eslint
code --install-extension dracula-theme.theme-dracula      
code --install-extension formulahendry.code-runner        
code --install-extension ms-python.anaconda-extension-pack
code --install-extension ms-python.python
code --install-extension oderwat.indent-rainbow
code --install-extension PKief.material-icon-theme        
code --install-extension redhat.vscode-yaml
code --install-extension ritwickdey.LiveServer
code --install-extension rocketseat.RocketseatReactJS     
code --install-extension rocketseat.RocketseatReactNative 
code --install-extension shardulm94.trailing-spaces       
code --install-extension thebarkman.vscode-djaneiro       
code --install-extension thekalinga.bootstrap4-vscode   
```
# Referencias:

https://medium.com/@raullesteves/github-como-fazer-um-readme-md-bonit%C3%A3o-c85c8f154f8

https://docs.microsoft.com/pt-br/visualstudio/ide/tips-and-tricks-for-visual-studio?view=vs-2019

https://medium.com/@programadriano/hoje-irei-apresentar-o-vs-code-visual-studio-code-para-quem-ainda-n%C3%A3o-teve-contato-com-ele-6a0d6bd3baec

https://code.visualstudio.com/docs/editor/command-line
