## Глобальный .gitignore

На машине разработчика должен быть настроен глобальный гит игнор, в который вносятся данные специфичные для его 
окружения (ОС, используемой ide и проч.), чтобы в файле проекта не было лишних записей, только то что относится к проекту. 
Как это сделать:

Создать файл `.gitignore` не в папке проекта (`~/.gitignore` или в папке со всеми проектами), например:

```
# phpstorm project files
.idea

# netbeans project files
nbproject

# zend studio for eclipse project files
.buildpath
.project
.settings

# windows thumbnail cache
Thumbs.db

# Mac DS_Store Files
.DS_Store

# phpunit itself is not needed
phpunit.phar

#ignore codeception phar archive
codecept.phar
```

Назначить глобальным (комманды даны с расчетом что файл вы положиле в домашнюю папку пользователя от которого выполняете команды):

*nix:
```
git config --global core.excludesfile '~/.gitignore'
```
Windows git bash:
```
git config --global core.excludesfile '~/.gitignore'
```
Windows cmd:
```
git config --global core.excludesfile "%USERPROFILE%\.gitignore"
```

## Ветки

Произойти может всё что угодно, поэтому коммиты сразу в master под запретом, а сама ветка master по умолчанию защищена 
от удаления и форс пуша. Любые изменения предлагаются через пулреквесты.

### Именование

Для единообразия и не избежания путаницы ветки именуются номером задачи, без дополнительных префиксов: 

* %issue_number% — разделения на новый функционал и исправления нет.

Любые исправления уже выкаченой на бой задачи оформляются в отдельную, на основании которой создается ПР.

Дополнительная ветка hotfix, в нее заливаются быстрые заплатки.

## Работа с кодом

### Коммиты

Один коммит решает одну небольшую задачу, а не объединяет под собой несколько. Так гораздо проще следить за изменениями 
и восстановить ход работы при необходимости.

К сообщению коммита нужно прикрепить номер задачи (2349. Fixed file upload.).

Если коммит не привязан к задаче, например вы заливаете быстрофикс в ветку hotfix, в комментарии максимально 
развернуто объяснить что он делает.

## Подготовка кода к пул-реквесту

Перед отправкой кода на проверку в ПР, нужно его подготовить, разрешить все конфликты с текущим состоянием ветки `master`. Для этого нужно:

1. Обновить всю информацию о репозитории: 

```git fetch --all```

2. Обновить текущую ветку до мастера:

```git rebase -i origin/master```

Если необходимо — схлопнуть выбранные коммиты (`squash`) и оставить (`pick`). Например:

```
pick f7f3f6d 3548_fix
squash 310154e 3548_change
squash a5f4a0d 3548_change

# Rebase 710f0f8..a5f4a0d onto 710f0f8
#
# Commands:
#  p, pick = use commit
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#
# If you remove a line here THAT COMMIT WILL BE LOST.
# However, if you remove everything, the rebase will be aborted.
#
```

Теперь гит находится в состоянии ребейза о чем свидетельствует статус:

```
$ git status

interactive rebase in progress; onto 52e4b371
Last commands done (9 commands done):
   squash 8e56a9b6 3569. Working parser, but some trash in article text.
   squash 3cbbbc27 3569. Working parser, start tests.
  (see more in file .git/rebase-merge/done)
Next commands to do (4 remaining commands):
   squash 7c905aa6 3569. Added Gazetaru parser, test for ContentSaverHandler, update test config.
   squash d7c0836d 3569. Fixed test, reformat Content saver.
  (use "git rebase --edit-todo" to view and edit)
You are currently rebasing branch 'feature_3569' on '52e4b371'.
  (fix conflicts and then run "git rebase --continue")
  (use "git rebase --skip" to skip this patch)
  (use "git rebase --abort" to check out the original branch)

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   commands/CloneController.php
	modified:   library/cloning/agents/cryptocurrency/Base.php
	new file:   library/cloning/agents/svpressa/CleanHandler.php
	modified:   library/cloning/agents/svpressa/Parser.php
	modified:   library/cloning/base/PageListParser.php
	modified:   library/cloning/base/Parser.php
	new file:   library/cloning/base/exceptions/CloningExitException.php
	modified:   library/cloning/handlers/ContentCrawlerHandler.php
	modified:   library/cloning/handlers/ContentSaveHandler.php
	new file:   tests/unit/library/cloning/svpressa/CleanerTest.php

Unmerged paths:
  (use "git reset HEAD <file>..." to unstage)
  (use "git add <file>..." to mark resolution)

	both modified:   config/test.php
	both modified:   tests/unit/_bootstrap.php
```

В процессе ребейза могут возникнуть конфликты, после их решения нужно сделать:

```git rebase --continue```

После чего комиты сольются в один и нужно будет выполнить force push своей ветки:

```git push -f origin %task_number%```

Теперь можно создавать пулл реквест.