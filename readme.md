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

----

## Создание удалённого репозитория и SSH-ключа

### Несколько слов про GitHub

Предыдущий раздел содержал подробное описание **локального** использования Git, но одно из самых главных его преимуществ - удобство командной работы над файлами. Для того, чтобы поделиться репозитоием, нужно завести его **удалённую** версию. Соответственно, одна из самых популярных платформ для удаленной командной работы - ```GitHub```, на котором вы и читаете эту шпаргалку.

**GitHub** — платформа для хранения IT-проектов и совместной работы над ними с использованием Git. По сути, это сайт, куда можно загрузить файлы своего проекта для обмена с другими людьми.

К тому же **GitHub** — это социальная сеть для разработчиков. С момента своего возникновения в 2008 году она, согласно статистике, объединила десятки миллионов человек, дала им возможность для реализации идей и сотрудничества.

**ОЧЕНЬ ВАЖНО ПОНИМАТЬ!** ```Git``` и ```GitHub``` — это два разных проекта, которые развиваются независимо друг от друга. 

**Git**:
- консольный инструмент для работы с локальными и удалёнными репозиториями;
- проект с открытым исходным кодом.

**GitHub**:
- платформа для размещения удалённых репозиториев;
- принадлежит компании Microsoft.
Кроме GitHub, есть и другие платформы для командной работы. Например, *GitLab* и *Bitbucket*, которые тоже позволяют работать с **Git**. У каждой из этих платформ свои особенности и дополнительная функциональность.

### Создаем удалённый репозиторий

Для создания удалённого репозитория можно следовать пошаговой инструкции:

- Зайдите в свой профиль по ссылке ```https://github.com/username```, где ```username``` — имя, которое вы указали при регистрации.
- Создайте репозиторий. Для этого перейдите на вкладку **Repositories**, а затем нажмите на зелёную кнопку **New** справа. 
- Открылось окно создания нового репозитория. Назовите его так как считаете нужным. Название удалённого репозитория необязательно должно совпадать с именем папки проекта у вас на компьютере. Но чтобы не путаться, обычно называют их одинаково. В конце смело нажимайте на зелёную кнопку **Create repository** внизу.

### Генерируем SSH-ключ

#### Что такое SSH?!

Когда компьютеры обмениваются данными в сети, они следуют **сетевым протоколам** (англ. *network protocols*) — правилам обмена данными между компьютерами.

Один из наиболее распространённых сетевых протоколов — **SSH** (от англ. *Secure Shell Protocol*). Он обеспечивает безопасный обмен данными в сети. С помощью этого протокола можно получать данные с удалённого компьютера или отправлять их на него. Трафик шифруется, поэтому протокол безопасен.

SSH использует пару ключей для обеспечения безопасности — публичный и приватный: 

    Приватный ключ хранится только на вашем компьютере и не должен передаваться кому-либо ещё. Он используется для расшифровки данных.
    Публичный ключ доступен всем и используется для шифрования данных. Они могут быть расшифрованы парным приватным ключом.

Только вы можете расшифровать данные с помощью приватного ключа, но любой владелец публичного ключа может их для вас зашифровать. Эти два ключа связаны и образуют **SSH-пару**. 

#### Где обычно хранятся SSH-ключи?

Обычно SSH-ключи находятся в директории ```.ssh/.``` Проверить наличие этой директории и файлов в ней можно с помощью следующей команды:

```bash

$ cd ~	# перешли в домашнюю директорию 

$ ls -la .ssh/	# вывели список созданных ключей 

```

#### Инструкция по генерации SSH-ключа

- Для генерации SSH-пары можно использовать программу ```ssh-keygen```. Откройте терминал и введите следующую команду.

```bash

$ ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub" 

	#если вы увидели сообщение об ошибке, то ваша система, вероятно, не поддерживает указанный алгоритм шифрования, попробуйте следующую команду...
	
$ ssh-keygen -t rsa -b 4096 -C "электронная почта, к которой привязан ваш аккаунт на GitHub" 

```
	 После ввода отобразится такое сообщение:

```bash

> Generating public/private rsa key pair. # сгенерированы публичный и приватный ключи 

```

- Укажите место хранения ключей. Простой вариант — сделать домашний каталог пользователя путём по умолчанию. Для этого нажмите ```Enter```.
- Теперь в указанной директории появится пара ключей. Программа запросит **кодовую фразу** (англ. *passphrase*) для доступа к SSH-ключу. Вы можете оставить поле пустым. Для этого нажмите ```Enter```, а затем ещё раз ```Enter``` для подтверждения.
- Готово! Теперь осталось проверить, что ключи действительно сгенерировались. Для этого вызовите эту команду:

```bash

ls -a ~/.ssh 

```

На экране должны появиться два файла — один с расширением ```.pub```, другой — без. Файл в ```.pub``` — публичный, им можно делиться с веб-сайтами или коллегами. Файл без расширения ```.pub``` — приватный. Ни в коем случае не передавайте его никому! 

### Привязываем SSH-ключ к GitHub

- После выполнения команды ```ssh-keygen``` из предыдущего блока в директории ```~/.ssh``` будет создано два файла — ```id_ed25519``` и ```id_ed25519.pub``` (или ```id_rsa``` и ```id_rsa.pub``` — в зависимости от того, какой алгоритм вы использовали). Теперь скопируйте содержимое файла с публичным ключом в буфер обмена, для этого можно распечатать файл на экран с помощью ```cat ~/.ssh/id_rsa.pub``` и скопировать его вручную.
- Перейдите на GitHub и выберите пункт **Settings** в меню аккаунта.
- В меню слева нажмите на пункт **SSH** and **GPG keys**.
- В открывшейся вкладке выберите **New SSH key**.
- В поле **Title** напишите название ключа. Например, **Personal key**.
- В поле **Key type** должно быть **Authentication Key**.
- В поле **Key** скопируйте ваш ключ из буфера обмена.
- Нажмите на кнопку **Add SSH key**.
- Проверьте правильность ключа с помощью следующей команды:

```bash

$ ssh -T git@github.com 

```

Если это первый раз, когда вы используете Git, чтобы поделиться проектом на GitHub, появится похожее предупреждение:

```bash

The authenticity of host 'github.com (140.82.121.4)' can't be established. ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU. This key is not known by any other names. Are you sure you want to continue connecting (yes/no/[fingerprint])?

```

Это предупреждение сообщает, что вы никогда не соединялись с сервером GitHub. Поэтому Git не может гарантировать, что сервер является тем, за кого он себя выдаёт.
Введите ```yes```, чтобы продолжить. Вы увидите приветствие на экране:

```bash

Hi %ВАШ_АККАУНТ%! You've successfully authenticated, but GitHub does not provide shell access.

```

## Соединение локального и удаленного репозиториев 
