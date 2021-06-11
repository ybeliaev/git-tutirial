# GIT shot tutirial
## Сокращенный вывод статуса
`git status -s`
* `??` новые неотслеживаемые файлы 
* `A`  файлы добавленные в отслеживаемые  
* `M`  отредактированные файлы 

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

