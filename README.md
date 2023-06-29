# Шпаргалка по работе с Git.<br>  
## Установка и начало работы<br>
1. Перейдите на [сайт](https://git-scm.com/downloads) и скачайте Git для вашей ОС.<br>
2. Установите Git с помощью диалогового окна.<br>
3. Для работы с Git в консольном режиме запустите **Git bash**.<br>
## Навигация<br>
* Корневая директория - `/`<br>
* Домашняя директория - `~`<br>
* Вывести на экран список файлов текущей директории - `ls`<br>
  * Вывести на экран список всех файлов текущей директории (в том числе скрытых) - `ls -a`<br>
  * Вывести на экран список файлов с дополнительной информацией - `ls -l`<br>
* Перейти в нужную директорию - `cd имя_директории/имя_поддиректории/...`<br>
## Работа с файлами и папками<br>
* Создать файл - `touch fileName`<br>
* Просмотреть содержимое файла - `cat fileName`<br>
* Создать папку - `mkdir dirName`<br>
* Создать дерево папок - `mkdir -p dirOne/dirTwo/dirThree/...`<br>
* Удалить файл - `rm fileName`<br>
* Удалить пустую директорию `rmdir dirName`<br>
* Удалить директорию, содержащую файлы - `rm -r`<br>
* Копировать файл - `cp fileName directoryToStoreFile`<br>
* Переместить файл/папку - `mv fileOne, folderOne,... directoryToStoreFilesAndFolders`<br>
## Создание удалённого репозитория
1. Зарегистрироваться на сайте [GitHub]("https://github.com/")<br>
2. Создать репозиторий, присвоить ему имя, определить права доступа (*private, public*)<br>
## Создание локального репозитория
1. Создать папку с названием проекта, например `mkdir first-project`<br>
2. Переместиться в неё `cd first-project`<br>
3. Ввести в консоли команду `git init`.
4. Убедиться, что локальный репозиторий создан, можно по созданию папки **.git** внутри директории *first-project*.<br>
5. Введя команду `ls -a`, мы убедимся, что папки **.git** создана.<br>
6. Если репозиторий инициализирован по ошибке, то командой `rm -rf .git` мы удаляем его.<br>
## Генерация SSH ключей
* SSH (*secure shell protocol*) представляет из себя протокол для удалённого управления операционной системой<br>
* Для работы с этим протоколом необходимо сгенерировать пару ключей (*public - private*)<br>
* С помощью *private* ключа мы шифруем информацию. Данный ключ должен храниться только у нас.<br>
* С помощью *public* ключа мы расшифровывем информацию. Данным ключом можно делиться с теми, кто будет иметь в доступ к информации.
* Для генерации пары ключей воспользуемся утилитой **ssh-keygen**, предварительно перейдя в домашнюю директорию `cd ~`.<br>
* `ssh-keygen -t ed25519 -C "Электронная почта, к которой привязан аккаунт на GitHub`<br>
* *ed25519* - это алгоритм генерации ключей. Можно воспользоваться другим алгоритмом из числа тех, с которыми работает ОС.<br>
* После генерации ключей будет предложено ввести имя директории для их сохранения и пароль для последующего соединения с удалённым репозиторием.<br>
* Убедимся, что ключи сгенерированы. Командой `ls -la ~/.ssh` мы проверяем наличие не только самой папки *.ssh* (она скрыта, поэтому используется ключ **-a**), но и файлов внутри неё.
* Мы должны увидеть два файла вида *id_ed25519* и *id_ed25519.pub*.
## Передача публичного ssh-ключа.
1. На сайте GitHub в настройках своего аккаунта найти вкладку *Settings* и перейти на неё.<br>
2. В меню слева найти вкладку *SSH and GPG keys* и перейти на неё.<br>
3. В поле *SSH keys* добавить содержимое публичного ключа (*id_ed25519.pub*).<br>
## Привязка локального репозитория к удалённому
* Для того, чтобы загружать сохранённые файлы на удалённый репозиторий, нам необходимо связать локальный репозиторий с удалённым.<br>
  * Делается это с помощью команды `git remote add origin urlOfYourRemoteRepo`<br>
    * *origin* - имя удалённого репозитория по умолчанию.<br>
    * *urlOfYourRemoteRepo* - ссылка на удалённый репозиторий, которую мы можем найти в только что созданном удалённо репозитории.<br>
    * Например, `git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git`<br>
  * Проверяем, что оба репозитория связаны командой `git remote -v`. Должны наблюдать следующие две записи:<br>
    *origin    `git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (fetch)`<br>
    *origin    `git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (push)`<br> 
## Сихронизируем локальный и удалённый репозитории
* Изначально Git помечает новые файлы в локальном репозитории как *untrackted* - неотслеживаемые, поэтому необходимо указать файлы, состояние которых будет отслеживаться.<br>
  * Команда `git add` не сохраняет файлы, а подготавливает их для дальнейшего сохранения. После выполнения `git add` Git начнёт отслеживать состояние указанных файлов.<br>
  * Командой `git add --all` мы добавим для отслеживания все файлы в данной директории.<br>
  * Так же мы можем добавлять файлы поимённо `git add fileNameOne fileNameTwo ...`<br>
* Командой `git status` мы проверяем состояние локального репозитория в данный момент: новые неотслеживаемые файлы, добавленные для отслеживания, сохранённые.<br> 
* Подготовленные к сохранению файлы мы можем *закоммитить*, т.е. сохранить их текущее состояние в репозитории Git.<br>
  * Командой `git commit -m "*Message about commit*"' мы сохраняем состояние файлов в локальном репозитории.<br>
    * Флаг `-m` - *message*. По каждому коммиту необходимо написать сопровождающее сообщение о том, что было сделано, чтобы коллегам было проще понять суть изменений.<br>
* Если необходимо посмотреть историю коммитов, то командой `git log` мы можем увидеть все сделанные до этого момента коммиты. Самый верхний коммит - самый последний.<br>
* Для отправки изменённых файлов на удалённый репозиторий мы используем команду `git push`.<br>
  * `git push -u origin master` при первом коммите или `git push` для всех остальных.<br>
    * Флаг `-u` свяжет локальную ветку с одноимённой удалённой.<br>
    * *origin* - имя удаённого репозитория.<br>
    * *master* или *main* - название начальной ветки по умолчанию.<br> 
## Hash коммита. Что? Для чего нужен?
* Хеш коммита (основной идентификатор коммита) представляет из себя набор чисел от 0 до 9 и букв A-F фиксированной длины, в котором зашифрована информация о коммите.<br>
  * Информация о коммисте содержит: имя автора, ссылка на предыдущий коммит, дату и время коммита, содержимое файлов в репозитории.<br>
  * Информация, указанная выше, преобразуется в хеш с помощью алгоритма SHA-1 (Secure Hash Algorithm).<br>
  * Алгоритм преобразования устроен таким образом, что изменение даже одного символа ведёт к сильному изменению в хеше.<br>
  * Существует таблица соответствий *хеш -> информация о коммите* Git хранит эту таблицу в скрытой папке **.git**. <br>
## История коммитов
 * Командой `git log` мы можем посмотреть историю коммитов в формате "самый верхний коммит - самый последний".<br>
   * Данная команда выводит следующую информацию:<br>
     * Хеш коммита;<br>
     * Автора коммита и его e-mail;<br>
     * Дату и время коммита;<br>
     * Краткое сообщение о том, что сделано в коммите.<br> 
* Если коммитов много, то чтение такой информации становится неудобным.<br>
* Поэтому команда `git log --oneline` выводит список коммитов с самой нужной информацией:<br>
  * Сокращённый хеш коммита (но такой, чтобы в списке он был уникальным);<br>
  * Краткое сообщение о коммите;<br>
* Данный способ позвоялет легче ориентироваться в проектах с большим числом коммитов.<br>
## HEAD файл
* Информация о последнем коммите содержит так же фразу *HEAD->master*, которая содержим ссылку на этот коммит.<br>
* Файл HEAD хранится в скрытом каталоге *.git*. Командой `cd renoName` перейдём в необходимый репозиторий, а затем выведем на экран содержимое HEAD.<br>
* Команда `cat HEAD` выведет на экран *ref: refs/heads/master или main*. Это ссылка на служебный файл, заглянув в который, мы увидим хеш последнего коммита<br>
* Выполним `cat refs/heads/master или main`, получив, к примеру,  *e007f5035f113f9abca78fe2149c593959da5eb7*.<br>
* Файл HEAD обновляет ссылку каждый раз при появлении нового коммита.<br>

