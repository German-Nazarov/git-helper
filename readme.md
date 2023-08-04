# Инструкция по Git и GitHub (для Linux) 

## Базовые команды в *Terminal* (применение и расшифровки)

### Навигация

- ``` pwd ``` (от англ. *print working directory*, "показать рабочую директорию";
- ``` ls ``` (от англ. *list directory content*, "отобразить содержимое директории");
- ``` ls -a ``` - показать также скрытые файлы и папки название которы начинаются с символа ``` . ```;
- ``` cd git-helper ``` (от англ. *change directory*, "сменить директорию") - перейти в папку ``` git-helper ```;
- ``` cd git-helper/for-students ``` - перейти в папку ``` for-students ```, которая находится в папке ``` git helper ```;
- ``` cd .. ``` - перейти на уровень выше, в родительскую папку;
- ``` cd ~ ``` - перейти в домашнюю директорию ```home/username/ ```;
- ``` cd / ``` - перейти в корневую директорию.

### Работа с файлами и папками

#### Создание

- ``` touch readme.md ``` (англ. *touch*, "коснуться") - создать файл ``` readme.md ``` в текущей папке;
- ``` touch readme.md calibration.txt albedo-processing.py albedo-report.odt ``` - если нужно создать сразу несколько файлов, можно напечатать и имена в одну строку через пробел;
- ``` mkdir lab3-albedo ``` (от англ. *make directory*, "создать директорию") - создать папку с именем ``` lab3-albedo ``` в текущей папке.

#### Копирование и перемещение

- ``` cp data.txt ~/main-dir ``` (от англ. *copy*, "копировать") - скопируй файл в другое место;
- ``` mv data.txt ~/main-dir ``` (от англ. *move*, "переместить") - переместить файл или папку в другое место.

#### Чтение

- ``` cat data.txt ``` (от анг. *concatenate and print*, "объединить и распечатать") - распечатать содержимое текствого файла.

#### Удаление

- ``` rm logo.png ``` (от англ. *remove*, "удалить") - удалить файл ``` logo.png ```;
- ``` rmdir images ``` (от англ. *remove directory*, "удалить директорию") - удалить пустую папку ``` images ```;
- ``` rm -r first-project ``` (от англ. *remove*, "удалить" + *recursive*, "рекурсивный") - удалить папку ``` first-project ``` и всё, что она содержит.

### Всякие полезности

- Команды необязательно печатать и выполнять по очереди. Можно указать их списком - разделить двумя амперсандами (``` && ```).
- Чтобы не вводить название файла или папки полностью, можно набрать первые символы имени и дважды нажать ``` Tab ```. Если файл или папка есть в текущей директории, командная строка допишется сама.

----

## Подготовка локального репозитория

### Несколько слов про Git

Git - это система контроля версий, которая помогает отслеживать изменения в проекте. Этот инструмент можно использовать как для индивидуальной, так и для командной работы.

Git позволяет сохранять изменения локально и при необходимости возвращаться к предыдущим версиям проекта. Также можно создать удаленную копию на хостинг-платформе, которая работает с Git, и поделиться результатом с другими. 

### Инициализация Git-репозитория

#### Сделать папку репозиторием - ```git init```

Чтобы Git начал отслеживать изменения в проекте, папку с файлами этого проекта нужно сделать **Git-репозиторием** (от англ. *repository* - "хранилище"). Для этого нужно переместиться в папку (вашего проекта) в терминале и ввести команду ```git init``` (от англ. *initialize* - "инициализировать").

Если всё прошло успешно, то ```git init``` выведет сообщение вида ```Initialized empty Git repository in <*ваша папка с проектом*>/.git/``` (инициализирован пустой Git-репозиторий). При этом будем создана подпапка ```.git```, хранящая всю служебную информацию. Данную подпапку можно увидеть, если отображать содержимое директории вместе со скрытыми файлами, команда ```ls -a```, имеющаяся в блоке **Навигация**.

#### Как "разгитить" папку, если что-то пошло не так?! - ```rm -rf .git```

Если вы случайно сделали Git-репозиторием не ту папку, её можно "разгитить". Для этого нужно удалить скрытую папку ```.git```.

```bash

$ cd <ваша папка с репозиторием>	#перешли в папку

$ rm -rf .git	#удалили подпапку .git 

```

Подробно о том, что такое ```-rf```:

- ключ ```-r``` (от анг. *recursive* - "рекурсивный") позволяет удалять папки вместе с их содержимым;
- ключ ```-f``` (от анг. *force* - "заставить") избавит вас от вопросов вроде "Вы точно хотите удалить этот файл? А ещё вот этот? И тот тоже?".

#### Проверка состояния репозитория - ```git status```

После инициализации репозитория можно запустить команду ```git status``` - она показывает текущее состояние репозитория.

Команда ```git status``` выведет:

- название текущей ветки: ```On branch master``` (или ```On branch main```);
- сообщение о том, что в репозитории ещё нет коммитов (если вы только что создали этот репозиторий): ```No commits yet```;
- сообщение, которое объясняет: "чтобы что-нибудь закоммитить (то есть зафиксировать), нужно сначала это создать" - ```nothing to commit (create/copy files and use "git add" to track).

#### Подготовить файлы к сохранению - ```git add```

Если вы создали какой-либо файл, пусть ```todo.txt```, запустите ```git status```. Тогда Git сообщит, что в папке есть ```untracked files``` (от англ. *track* — «следить», untracked — «неотслеженный», «неотслеживаемый») - ещё не отслеживаемый файл ```todo.txt```.

Состояние ```untracked``` значит, что Git ещё не хранит информацию о версиях файла и не может отследить, как он изменялся.

Чтобы отслеживать состояние объектов, можно добавлять их по одному, либо сразу все с ключом ```--all```

Если всё получилось, то файлы, которые отмечены зелёным, теперь отслеживаются и готовы к сохранению. Но сохранения пока не произошло, потому что команда ```git add``` только запоминает текущее содержимое (контент) файла.

**Отличие запоминания от сохраения**:  Команда ```git add``` не сохраняет содержимое файлов в репозитории. Само сохранение, или фиксацию состояния файлов, называют коммитом (от англ. *commit* — «совершать», «фиксировать»). «Сделать коммит» значит сохранить текущую версию файла. Если провести аналогию, команду git add можно сравнить с добавлением товаров в корзину в интернет-магазине, а коммит — с оформлением и оплатой заказа.

Если сейчас отредактировать любой из «зелёных» файлов в папке, он перейдёт в состояние *modified* (англ. «изменённый») и будет и в «зелёном», и в «красном» списках. При повторном сохранении и вызове ```git status``` зеленым будет отмечена пустая версия файла - в таком виде он был во время последнего запуска команды ```git add```; красным отмечена новая версия. Чтобы запомнить новое состояние файла, нужно снова ввести команду ```git add```. Теперь файл(ы) снова готов(ы) к сохранению.

#### Выполнить коммит - ```git commit```

Сделать коммит можно командой ```git commit``` c ключом -m (от англ. *message* — «сообщение»), который присваивает коммиту сообщение.

Обычно в таком сообщении поясняется, в чём именно состояли изменения. Это как заметки на полях: благодаря им проще читать и понимать текст. Сообщение коммита выполняет те же функции — улучшает понимание и упрощает навигацию. Оно пишется после ключа -m в кавычках.

```bash

$ git commit -m ‘Добавлен файл readme.md.’

```

Команда ```git commit``` выведет информацию о коммите. 

* ```[master (root-commit) baa3b6e]``` значит: 
	* коммит был в ветке ```master```
   	* ```root-commit``` - это самый первый коммит в ветке, у следующих коммитов такой надписи не будет;
   	* ```baa3b6e``` - сокаращенный индентификатор коммита
* ```x files changed, y insertion(+)``` значит:
	* изменились x файлов;
	* y строк были добавлены.
* Строки вида ```create mode 100644 todo.txt``` - это более подробная информация о новых файлах.
	* ```create``` говороит о том, что файл создан (или ```delete``` - удален);
	* ```mode 100644``` сообщает, что это обычный файл. Также возможны варианты ```100755``` для исполняемых файлов (например, ```что-нибудь.exe```).

#### Просмотреть историю коммитов — ```git log```

Обратите внимание, что по умолчанию ```git log``` выводит коммиты в обратном хронологическом порядке — последние коммиты оказываются первыми сверху. В этом можно убедиться, если посмотреть на дату и время их создания.

## Создание SSH-ключа

## Соединение локального и удаленного репозиториев 
