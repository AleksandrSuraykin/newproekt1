# Работа с Git

## 1. Инициализация нового пустого репозитория кода
> Перейдите в папку проекта и выполните команду в консоли (Терминале):
> 
```bash
$ git init
```
Добавим файл .gitignore в корень проекта
```bash
touch .gitignore
```
С содержимым
```.gitignore
.idea/
.vscode/

node_modules/
package-lock.json

.DS_Store
Thumbs.db
desktop.ini
```
```bash
touch .gitattributes
```
```.gitattributes
# Common settings that generally should always be used with your language specific settings
# Auto detect text files and perform LF normalization
*  text=auto

#
# The above will handle all files NOT found below
#

# Documents
*.bibtex   text diff=bibtex
*.doc      diff=astextplain
*.DOC      diff=astextplain
*.docx     diff=astextplain
*.DOCX     diff=astextplain
*.dot      diff=astextplain
*.DOT      diff=astextplain
*.pdf      diff=astextplain
*.PDF      diff=astextplain
*.rtf      diff=astextplain
*.RTF      diff=astextplain
*.md       text diff=markdown
*.mdx      text diff=markdown
*.tex      text diff=tex
*.adoc     text
*.textile  text
*.mustache text
*.csv      text
*.tab      text
*.tsv      text
*.txt      text
*.sql      text

# Graphics
*.png      binary
*.jpg      binary
*.jpeg     binary
*.gif      binary
*.tif      binary
*.tiff     binary
*.ico      binary
# SVG treated as text by default.
*.svg      text
# If you want to treat it as binary,
# use the following line instead.
# *.svg    binary
*.eps      binary

# Scripts
*.bash     text eol=lf
*.fish     text eol=lf
*.sh       text eol=lf
*.zsh      text eol=lf
# These are explicitly windows files and should use crlf
*.bat      text eol=crlf
*.cmd      text eol=crlf
*.ps1      text eol=crlf

# Serialisation
*.json     text
*.toml     text
*.xml      text
*.yaml     text
*.yml      text

# Archives
*.7z       binary
*.gz       binary
*.tar      binary
*.tgz      binary
*.zip      binary

# Text files where line endings should be preserved
*.patch    -text

#
# Exclude files from exporting
#

.gitattributes export-ignore
.gitignore     export-ignore
.gitkeep       export-ignore
```

## 2. Конфигурация Git для вашего компьютера
Необходимо задать свой пароль и имя от которых вы будете делать фиксацию изменений
```bash
$ git config --global user.name "Ваше имя"
$ git config --global user.email "ваша@почта"
```

## 3. Рабочий процесс
1) Внести изменения в рабочий каталог
2) Проиндексировать изменения
```bash
$ git add название_файла
```
Добавить все файлы, кроме конфигурационных
```bash
$ git add *
```
Добавить все файлы и конфигурационные в индексируемые (Staging Area)
```bash
$ git add .
```
3) Зафиксировать изменения
```bash
$ git commit -m "Ваше сообщение"
```

Если нужно убрать из индексации ошибочно добавленные изменения(обратное действие команде `git add`), то вы можете выполнить команду:
```bash
$ git reset название_файла
```

Просмотр статуса изменений 
```bash
$ git status
```
Отмена изменений в коде файла
```bash
$ git restore имя_файла
```

Просмотр статуса изменений 
```bash
$ git status
```
Отмена изменений в коде файла
```bash
$ git restore имя_файла
```
Если вы случайно удалили файл, но не делали фиксации изменений, его можно быстро вернуть командой:
```bash
$ git checkout HEAD название файла
```

## 4. Ветки
```bash
$ git branch
```
Перейти на другую ветку
```bash
$ git checkout название_ветки
```

> Для создания новой ветки из кода текущей активной с одновременным переходом на новую:
```bash
$ git checkout -b название_новой_ветки
```

### Наименование веток (договоренности)
* `main` или  `master` - название основной ветки. Она неприкосновенна, в ней только фиксируются релизы готовых и прошедших тестирование функциональностей
* `develop` - ветка в которой ведется фиксация изменений разработки проекта
* `release/` - ветка сбора функциональностей из `develop` в релиз с последующим слиянием в `master` 
* `feature/` - ветка новой функциональности
* `hotfix/` - ветка быстрого исправления

Если вы удалили файл и зафиксировали изменения, то вы можете вернуть файл из предыдущего коммита:
```bash
$ git reset --hard HEAD~1
```

## 5. Сляиние изменений между ветками
1) Вам нужно перейти на ветку в которую вы хотите сделать слияние
```bash
$ git checkout main
```
2) Выполните команду 
```bash
$ git merge develop
```

### Сохранить изменения во временное хранение без фиксации, чтобы позднее их достать
```bash
$ git stash
```
Вытащить спрятанный код
```bash
$ git stash apply
```

## Подключение внешнего репозитория
1) Создать учетную запись во внешнем сервисе/репозитории
2) Создать там пустой проект
4) В вашем локальном репозитории на компьютере выполнить команду:
```bash
$ git remote add название_внешнего_репозитория путь_до_репозитория
$ git remote add origin https://......
```
Проверим задан ли внешний репозиторий кода:
```bash
$ git remote -v
```
Отправить наши локальные изменения на внешний сервер:
```bash
$ git push -u название_внешнего_репозитория название_ветки
$ git push -u origin main
```