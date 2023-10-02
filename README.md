# Практическая работа №1
## Базовые команды консоли
### Навигация
* `pwd` (от англ. print working directory, «показать рабочую папку») — покажи, в какой я папке;
* `ls` (от англ. list directory contents, «отобразить содержимое директории») — покажи файлы и папки в текущей папке;
* `ls -a` покажи также скрытые файлы и папки, названия которых начинаются с символа `.`;
* `cd first-project` (от англ. change directory, «сменить директорию») — перейди в папку `first-project`;
* `cd first-project/html` - перейди в папку 'html', которая находится в папке 'first-project' ;
* `cd ..` — перейди на уровень выше, в родительскую папку;
* `cd ~` — перейди в домашнюю директорию (`/Users/Username`);
* `cd /` — перейди в корневую директорию.
### Работа с файлами и папками
#### Создание
* `touch index.html` (англ. touch, «коснуться») — создай файл `index.html` в текущей папке;
* `touch index.html style.css script.js` если нужно создать сразу несколько файлов, можно напечатать их имена в одну строку через пробел;
* `mkdir second-project` (от англ. make directory, «создать директорию») — создай папку с именем `second-project` в текущей папке.

#### Копирование и перемещение
* `cp file.txt ~/my-dir` (от англ. copy, «копировать») — скопируй файл в другое место;
* `mv file.txt ~/my-dir` (от англ. move, «переместить») — перемести файл или папку в другое место.

#### Чтение
* `cat file.txt` (от англ. concatenate and print, «объединить и распечатать») — распечатай содержимое текстового файла `file.txt`.

#### Удаление
* `rm about.html` (от англ. remove, «удалить») — удали файл `about.html`;
* `rmdir images` (от англ. remove directory, «удалить директорию») — удали папку `images`;
* `rm -r second-project` (от англ. remove, «удалить» + recursive, «рекурсивный») — удали папку `second-project` и всё, что она содержит.

## Хеш — идентификатор коммита
В процессе работы с Git вам будет часто встречаться понятие «хеш коммита». Эти странные строчки с бессмысленным (на первый взгляд) набором букв и цифр вы могли видеть, когда вызывали команду `git log` и выводили историю коммитов.

![alt text](image(1).png)

### Что такое хеш. Хеширование коммитов
**Хеширование** (от англ. hash, «рубить», «крошить», «мешанина») — это способ преобразовать набор данных и получить их «отпечаток» (англ. fingerprint).
Информация о коммите — это набор данных: когда был сделан коммит, содержимое файлов в репозитории на момент коммита и ссылка на предыдущий, или **родительский** (англ. parent), коммит.
Git хеширует (преобразует) информацию о коммите с помощью алгоритма **SHA-1** (от англ. Secure Hash Algorithm — «безопасный алгоритм хеширования») и получает для каждого коммита свой уникальный хеш — результат хеширования.
Обычно хеш — это короткая (40 символов в случае SHA-1) строка, которая состоит из цифр 0--9 и латинских букв A—F (неважно, заглавных или строчных). Она обладает следующими важными свойствами:
* если хеш получить дважды для одного и того же набора входных данных, то результат будет гарантированно одинаковый;
* если хоть что-то в исходных данных поменяется (хотя бы один символ), то хеш тоже изменится (причём сильно).

Чтобы убедиться в этом, можно поэкспериментировать с SHA-1 на этом сайте — попробуйте ввести в поле **input** (англ. «ввод») разные символы, слова или предложения и понаблюдайте, как меняется хеш в поле **output** (англ. «вывод»).

### Хеш — основной идентификатор коммита
Git хранит таблицу соответствий `хеш → информация о коммите`. Если вы знаете хеш, вы можете узнать всё остальное: автора и дату коммита и содержимое закоммиченных файлов. Можно сказать, что хеш — основной идентификатор коммита.
При работе с Git хеши будут встречаться вам регулярно. Их можно будет передавать в качестве параметра разным Git-командам, чтобы указать, с каким коммитом нужно произвести то или иное действие.
Все хеши и таблицу `хеш → информация о коммите` Git сохраняет в служебные файлы. Они находятся в скрытой папке `.git` в репозитории проекта.

## Исследуем лог

В этом уроке рассмотрим подробнее, из каких элементов состоит описание коммита, а также как вывести сокращённый лог (от англ. log — «журнал [записей]»). Сокращённый лог полезен, если нужно быстро найти нужный коммит среди сотни других.
### Элементы описания коммита
После вызова `git log` появляется список коммитов.
![alt text](image(2).png)
Разберём элементы, из которых состоит описание:
* строка из цифр и латинских букв после слова commit — это хеш коммита;
* Author — имя автора и его электронная почта;
* Date — дата и время создания коммита;
* в конце находится сообщение коммита.
### Получить сокращённый лог — `git log --oneline`
Получить сокращённый лог можно с помощью команды `git log` с флагом `--oneline` (англ. «одной строкой»). В терминале появятся только первые несколько символов хеша каждого коммита и их комментарии.
![alt text](image(3).png)

Сокращённый лог полезен, если в репозитории уже много коммитов — например, сотни или тысячи. В этом случае можно быстро найти нужный по описанию.
Сокращённый хеш (то есть первые несколько символов полного) можно использовать точно так же, как и полный. Для этого команда `git log --oneline` автоматически подбирает такую длину сокращённых хешей, чтобы они были уникальными в пределах репозитория и Git всегда мог понять, о каком коммите идёт речь.

## HEAD — всему голова
При вызове команды `git log` вы также могли заметить надпись `(HEAD -> master)` после хеша одного из коммитов. В этом уроке расскажем, что она означает.

![alt text](image(4).png)

### Файл `HEAD`

Файл `HEAD` (англ. «голова», «головной») — один из служебных файлов папки `.git`. Он указывает на коммит, который сделан последним (то есть на самый новый).
В этом можно убедиться с помощью терминала. Перейдите в папку `.git` командой `cd`. Посмотрите содержимое файла `HEAD` командой `cat`. 

```
$ pwd # посмотрели, где мы
/Users/user/dev/first-project

$ cd .git/
$ ls # посмотрели, какие есть файлы
COMMIT_EDITMSG  ORIG_HEAD  description  index  logs/     refs/
HEAD            config     hooks/       info/  objects/

$ cat HEAD # команда cat показывает содержимое файла
ref: refs/heads/master # в файле вот такая ссылка
```

Внутри `HEAD` — ссылка на служебный файл: `refs/heads/master` (или `refs/heads/main` в зависимости от названия ветки). Если заглянуть в этот файл, можно увидеть хеш последнего коммита.

