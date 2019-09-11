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
code --install-extension alefragnani.Bookmarks
code --install-extension baterson.copy-django-model-fields
code --install-extension batisteo.vscode-django
code --install-extension bibhasdn.django-snippets
code --install-extension bigonesystems.django
code --install-extension ChakrounAnas.turbo-console-log
code --install-extension CoenraadS.bracket-pair-colorizer
code --install-extension DavidAnson.vscode-markdownlint
code --install-extension dbaeumer.vscode-eslint
code --install-extension donjayamanne.jupyter
code --install-extension donjayamanne.python-extension-pack
code --install-extension dracula-theme.theme-dracula
code --install-extension eamodio.gitlens
code --install-extension ecmel.vscode-html-css
code --install-extension formulahendry.code-runner
code --install-extension hnw.vscode-auto-open-markdown-preview
code --install-extension humao.rest-client
code --install-extension jevakallio.vscode-hacker-typer
code --install-extension keesschollaart.vscode-home-assistant
code --install-extension Kelvin.vscode-sshfs
code --install-extension lkytal.pomodoro
code --install-extension magicstack.MagicPython
code --install-extension minhthai.vscode-todo-parser
code --install-extension ms-python.python
code --install-extension ms-vscode.cpptools
code --install-extension oderwat.indent-rainbow
code --install-extension platformio.platformio-ide
code --install-extension rafaelmaiolla.remote-vscode
code --install-extension redhat.vscode-yaml
code --install-extension ritwickdey.live-sass
code --install-extension ritwickdey.LiveServer
code --install-extension shamanu4.django-intellisense
code --install-extension streetsidesoftware.code-spell-checker
code --install-extension streetsidesoftware.code-spell-checker-portuguese-brazilian
code --install-extension thebarkman.vscode-djaneiro
code --install-extension thekalinga.bootstrap4-vscode
code --install-extension Tyriar.shell-launcher
code --install-extension victorzevallos.vscode-theme-django
code --install-extension VisualStudioExptTeam.vscodeintellicode
code --install-extension vscode-icons-team.vscode-icons
code --install-extension wholroyd.jinja
code --install-extension wmaurer.change-case
code --install-extension xabikos.JavaScriptSnippets
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
