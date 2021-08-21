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

## Файл .gitignore
* Исключить все файлы с расширение .a
`*.a`

* Но отслеживать файл lib.a даже если он подпадает под исключение выше
`!lib.a`

* Исключить файл TODO в корневой директории, но не файл в subdir/TODO
`/TODO`

* Игнорировать все файлы в директории build/
`build/`

* Игнорировать файл doc/notes.txt, но не файл doc/server/arch.txt
`doc/*.txt`

* Игнорировать все .txt файлы в директории doc/
`doc/**/*.txt`

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
# Ветки. Создание и переключение
### просмотр веток
* `git branch`
* `git branch -v` просмотр веток с начальными числами идентификатора
### создание веток
`git branch <branch_name>`
### переключение веток
`git checkout <branch_name>`
### ! и создание и переключение веток
`git checkout -b <branch_name>`
### `PUSH` в выбранную ветку
`git push origin "branch_name"`
### Команда `checkout` при незакоммиченных изменениях
#### Ситуация: работаю на ветке `features` и не закоммитил недоделанную работу, т.к нужно переключиться на `master`
* `git checkout -f master` - незакоммич. изменения на  `features` пропадут
* `git checkout -f master`  - если я и был на `master` то всё откатится до состояния пред. коммита
 Но, если файлы в ветках одни и те же, то сделав не закоммич. изменение на `features`, затем переключ. на `master` и сделать `commit` - изменения из `features` попадут в `master`. Сигнал, что это может иметь место - литера `М` с названием модифиц. файла при `git checkout <branch_name>`
* `git checkout -f ` - сокращённая форма, откат изменений на ветке, где нахожусь
* `git stash` - архивирует изменения в файле (визуально пропадают)
* `git stash pop` - применить ранее отложенные изменения ( ВНИМАНИЕ - сделает это на любой ветке где я нахожусь )
### Перенос незакоммиченных изменений
Если при работе на `master` появился не закоммич. код, который и не сохранить и терять нельзя, то 
`git checkout -b <branch_name>`
* Т.к разницы между файлами нет, то не закоммич. код не пропадёт.
* Последующий коммит на `<branch_name>` продолжит работу на этой ветке
### Если `commit` не в той ветке
* Создать ветку `git branch <branch_name>`
* `git checkout -B master 45a32`, где 45a32 - id коммита ветки мастер, куда нужно откатиться
### Состояние отделённой HEAD
`git checkout 1914` - `checkout`на `commit`. Только для просмотра состояния, далее переключ. на ветку, не коммитив ничего перед этом.
### Восстановление предыдущих версий файлов
#### Задача: нужно откатиться на пару коммитов назад
* `git checkout 45a32 <file_name or dir>` or `git checkout <branch> <file_name or dir>`
* `git reset  <file_name>` сброс индекса
#### Если незакоммич. то `git checkout <file_name>`
### Просмотр истории 
* `git log`
* `git show <branch>~` - на 1 коммит назад
* `git show <branch>~~` - на 2 коммит назад
* `git show <branch>~2` - тоже самое
### Слияние веток "перемоткой"( основная ветка перемотается на id доп. ветки )
* `git checkout master` - перейти на ветку, в которую производить слияние
* `git merge <branch_name>`
* `cat .git/ORIG_HEAD` вывод последнего id перед слиянием, т.е
* `cat branch -f master ORIG_HEAD` вернёт все как было до слияния с `master`
### Удаление веток
* `git branch -d <branch_name>` - работает только (!!!) если две ветки объединены
* `git branch -D <branch_name>` - удаление неслитой ветки (но какое то время коммиты ещё есть в базе)
* `git branch -D <branch_name> <id>` - возврат ветки
### История переключений веток: лог ссылок reflog
* `git reflog`
* * `git reflog --date=iso` - добавление дат в лог
* `git branch <branch_name> HEAD@{N}` - переключение на коммит. `N` - номер `HEAD` в логе или дата как строка. `HEAD@{N}` возможно потребуется обернуть в кавычки 
* `git checkout @{-1}` - переключение на послед. коммит пред. ветки
### Удаление "лишних" файлов и незакоммиченных изменений
* `git checkout -f `
* or
* `git reset --hard`
Но эти команды не затронут неотслежтваемые файлы. Есть спец команда исключительно для таких файлов
* `git clean -df` `d` - не только файлы, но и папки, `x` - также файлы ,что игнорятся через `.gitignore`, `f` - без него не сработает
### Жесткий `reset --hard:` отмена изменений, удаление коммитов
* `git reset  --hard -@~` - на 1 коммит назад
* or
* `git reset  --hard 12r5` - откат на указанный id
* `git reset  ORIG_HEAD` - вернёт всё как было
