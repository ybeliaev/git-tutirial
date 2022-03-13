# GIT shot tutirial
## Сокращенный вывод статуса
`git status -s`
* `??` новые неотслеживаемые файлы 
* `A`  файлы добавленные в отслеживаемые  
* `M`  отредактированные файлы 

## SSH key
* Get to settings->SSH and GPG keys->generating SSH keys
* `$ ssh-keygen -t rsa  -b 4096 -C "comment or title here"` in console
* выбор места сохранения ключа
* при вводе пароля его потом будут постоянно спрашивать - пропуск дважды
* [Ввод ключа](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) публич часть - id_rsa.pub

# Файл .gitignore
### https://git-scm.com/docs/gitignore
### https://www.atlassian.com/git/tutorials/saving-changes/gitignore
### https://www.w3schools.com/git/git_ignore.asp
* Исключить все файлы с расширением .a
`*.a`

* Но отслеживать файл lib.a даже если он подпадает под исключение выше
`!lib.a`

* Исключить файл TODO в корневой директории, но не файл в subdir/TODO
`/TODO`

* Игнорировать все файлы в директории build/
`build/`

* Игнорировать файл doc/notes.txt, но не файл doc/server/arch.txt
`doc/*.txt`

* Игнорировать конкретный файл text.doc
`text.doc`

* Игнорировать любой файл с названием от 1 до 9
`[1-9].doc`

* Игнорировать все .txt файлы в директории doc/ на любой глубине
`doc/**/*.txt`
# Изменения действий, работа с `git reset`
### https://git-scm.com/docs/git-reset
### https://www.freecodecamp.org/news/save-the-day-with-git-reset/
### 💬 Для справки `git add .` добавляет файлы в `stage`
### 💬 Для справки `git log` -  просмотр истории коммитов
* `git reset` вернёт файлы в состояние `unstage`
* `git reset --hard HEAD` - удалит все предидущие изменения
>
> `--hard` - опция указывает на не просто понижение на уровень, а удаление
> 
> `HEAD` - обязательная в данном случае опция указывает до какого коммита нужно откатиться - это указатель на последний коммит. 
> 
## Внесение изменений в существующий коммит:
### 💡 Команды, меняющие git-историю нужно вызывать ДО отправки изменений на сервер!
* `git reset soft HEAD~1` дальше по классике `git add .` `git commit -m "..."`
>
> `--soft` - бережная распаковка, а не удаление предидущего коммита
> 
> `HEAD~1` - `~1` - следующий начиная с `HEAD` коммит

## Изменение названия существующего коммита
* `git commit --amend`
> Запустит редактор для изменения названия последнего коммита
> https://dev.to/biancapower/how-to-change-your-default-text-editor-for-git-and-avoid-vim-fk0 - как сменить редактор
>>  `git config --global core.editor "code --wait"`

### 💬 Для справки: коммиты НЕ мутабельны, т.е создасться новый коммит

## Изменения `stage` предидущего коммита
* какие то действия
* `git add .`
* `git --amend`
* В результате `stage` ПРЕДИДУЩЕГО или последнего коммита будет изменён

# `git stash`
### https://opensource.com/article/21/4/git-stash
* команда для сохранения изменений "на потом"(все изменения прячутся в позицию списка stash)
### базовое применение
>`git add`
>`git stash` 
>`git stash list` - просмотр списка `stash`
>`git stash save "name of stash"` - именование позиции вместо генерированного названия
### 💬 Для справки: новая запись кладётся под индекс `0` - `stash@{0}`
## `git stash pop`
* позиция из `stash` удаляется а изменения попадают в рабочую директорию
## `git stash apply stash@{0}`
* `apply` - не удалит элемент из списка `stash`, вытянет указанный (`stash@{0}`)

# `cherry-pick`
* позволяет взять любой коммит и переместить на мою ветку
* базовое использование:
> `git cherry-pick 111111` - `111111` это первые шесть цифр идентификатора\хэша нужного коммита
 
# `revert`
> `git revert 111111` - действия коммита с указанным хэшов будут отменены

# `rebase` - работа с историей
* ![rebase vs merge](https://github.com/ybeliaev/git-tutirial/blob/main/rebase.png)


# Ветки. Создание и переключение
### просмотр веток
* `git branch`
* `git branch -v` просмотр веток с начальными числами идентификатора
### создание веток
`git branch <branch_name>`
### переключение веток
`git checkout <branch_name>`
### И создание и переключение ветки
`git checkout -b <branch_name>`
### `PUSH` в выбранную ветку
`git push origin "branch_name"`
### `PULL`
* предположим, мы совершили мёрдж на отдалённом репозитории. Как получить изменения на локальный?
* `git pull origin master ` `master` - в данном случае название ветки, с которой хочу получить данные

## Переименование файла
`git mv <file_from> <file_to>`
* Переименует и проиндексирует
## Удаление файлов и папок
`git rm -r <directory>`
* флаг `-r` про удаление директории
`git rm <file>` удаление файла
## Удаление из индекса
`git rm -r --cached <directory>`
## Отмена коммита
`git commit --amend`
## Частичное добавление изменений
`git add -p <file name>`
* предложены будут флаги для применения к каждому изменению в файле
## Быстрое сохранение файлов
`git commit -am 'message'`
* но `git commit -a` сработает только для проиндексированных файлов, т.е которые git уже отслеживает
## Выборочный commit файлов
`git commit -m 'message' <file name>` 
* сработает только для файлов, которые git уже отслеживает


