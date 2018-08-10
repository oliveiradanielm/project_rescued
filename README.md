# project_rescued
Project rescued after `git add .` and `git reset --hard`


Após adicionar todos os arquivos, resolvi removê-los para selecionar apenas alguns arquivos.
Resolvi executar o comando `git reset --hard`, então todos os arquivos foram excluídos, restando apenas os que foram ignorados pelo `.gitignore`.

Após algumas pesquisas, localizei o comando `git fsck --lost-found` que lista os arquivos que já estiveram em stage.
Então naveguei até a pasta git do projeto `.git/lost-found/other` e localizei os arquivos excluídos anteriormente, fiz uma cópia e adicionei a extensão `.txt` para facilitar a busca.
