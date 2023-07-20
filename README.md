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
* Изначально Git помечает новые файлы в локальном репозитории как *untracked* - неотслеживаемые, поэтому необходимо указать файлы, состояние которых будет отслеживаться.<br>
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
* Информация о последнем коммите содержит так же фразу *HEAD->master*, которая содержит ссылку на этот коммит.<br>
* Файл HEAD хранится в скрытом каталоге *.git*. Командой `cd renoName` перейдём в необходимый репозиторий, а затем выведем на экран содержимое HEAD.<br>
* Команда `cat HEAD` выведет на экран *ref: refs/heads/master или main*. Это ссылка на служебный файл, заглянув в который, мы увидим хеш последнего коммита<br>
* Выполним `cat refs/heads/master или main`, получив, к примеру,  *e007f5035f113f9abca78fe2149c593959da5eb7*.<br>
* Файл HEAD обновляет ссылку каждый раз при появлении нового коммита.<br>
## Статусы файлов в Git
* Каждый файл, находящийся в репозитории, может иметь один (или несколько) статусов:<br>
  * Untracked (неотслеживаемый). Файл был создан, Git знает о его наличии, но не отслеживает его изменения.<br>
  * Staged (добавленный для отслеживания). Файл был добавлен с помощью команды `git add fileName`, и теперь Git следит за его состоянием.<br>
  * Tracked (отслеживаемый). Это файл, состояние которого было сохранено хот бы раз (*commit*).<br>
  * Modified (изменённый). Это добавленный для отслеживания файл, состояние которого было изменено (до или после коммита).<br>
* Замечания:
  * Любой *Staged* файл является и *Tracked* одновременно.<br>
  * *Modified* файлом может быть только файл, имеющий статус *Staged*.<br> 
* Ниже приведена схема для более наглядного понимания:<br>

```mermaid
graph LR;
  untracked --"git add" --> staged;
  staged -- "git commit" --> tracked;
  staged --"add some changes" --> modified;
  tracked --"add some changes" --> modified;
  modified -- "git add" --> staged;
```

## Оформление сообщений к коммитам
* Сообщение о коммите пишется после флага `-m` в команде `git commit`.<br>
* Должно быть коротким, но информативным. Есть несколько подходов к оформлению таких сообщений.<br>
  * Название действия пишется через инфинитив (*доработать, поправить, изменить*) + над чем проводилось действие подробно;<br>
  * Название действия пишется через существительные (*доработки, поправка, изменение*) + над чем проводилось действие подробно;<br>
  * В больших компаниях в начале сообщения может указыватья буквенно-цифровой номер задачи `"LGS32: + что сделано"`. Так коллегам будет проще понять, к какой задаче относится коммит.<br>
  * Так же, можно указать номер задачи через её номер. Например `"Доработать метод по задаче #1"`. В этом случае GitHub свяжет коммит и выполняемую задачу.<br>
  * Можно обратиться к стандарту [Conventional Commits](https://www.conventionalcommits.org/ru/v1.0.0-beta.4/#%D1%81%D0%BF%D0%B5%D1%86%D0%B8%D1%84%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D1%8F), если работа ведётся с исходным кодом.<br>
## Исправление коммита
* Git предоставляет возможность исправить коммит, дополнив его файлами, которые мы забыли синхронизировать.<br>
* Командой `git commit --ammend` мы можем закоммитить недостающие файлы в послдений коммит.<br>
  * Флаг `--no-edit` говорит о том, что сообщение о коммите не меняется.
  * Если же есть необходимость изменить сообщение последнего коммита, то после команды `git commit --ammend -m "Новое сообщение"` мы дополняем коммит недостающими файлами + обновляем сообщение о коммите.<br>
* Если команда `git commit --amend` вызвана без флагов выше, то откроется текстовый редактор, который попросит написать сообщение о коммите.<br>
* **Важно отметить**, что команда `amend` работает только с последним коммитом.<br>
## Как "откатиться" назад
1. Если файл находится в статусе *modified*, и мы хотим отменить изменения в файле до предыдущего сохранённого состояния (последнее после команды `git add` или `git commit`), то командой `git restore fileName` мы вернём файл в предыдущее состояние.<br>
   * Если мы хотим отменить изменения во всех файлах, то командой `git restore .` мы вернём все *modified* файлы в предыдущее сохраннённое состояние.<br>
2. Если файл находится в *staging area*, и мы передумали его туда добавлять, то командой `git restore --staged fileName` выведет файл из *staging area* обратно в *untracked area*.<br>
   * Если мы передумали добавлять все файлы в *staging area*, то командой `git restore --staged ." выведет все файлы обратно в *untracked area*.<br>
3. Если мы хотим "откатиться" до какого-то конкретного коммита, удалив все коммиты после него, то командой `git reset --hard <hash коммита, на который "откатываемся">` перенесёт *HEAD* на указанный коммит, забыв о тех, что шли выше.<br>
## Просмотр изменений в файлах
* Команда `git diff` позволяет просмотреть разницу между последней закоммиченной версией файла и текущей изменённой.<br> 	
  * Вывод изменений в файле содержит:<br>
    * Исходный файл (помечается знаками "---"), изменённый файл (помечается знаками "+++").<br>
    * Добавленные и удалённые строки, которые отмечены знаками "+" и "-" соответственно. Так же они могут быть окрашены в зелёный и красный цвета соответственно.<br>
    * Количество строк, попавших в вывод. Строка вида `@@ -1,2 +1,2 @@` сообщает о том, что в исходном (`-`) и текущем (`+`) файлах выведены по две строки начиная с первой.<br>
* По умолчанию команда `git diff` не показывает изменения в *staged* файлах, только в *modified*. Если изменения всё же необходимо просмотреть, то `git diff --staged` выведет изменения между *staged* файлом и закоммиченным.<br>
## Добавление строки в файл
* Строку в файл можно добавить через команду `echo`, которая выводит на экран всё, что поступает ей на вход, и символы перенаправления вывода `>>`.<br>
  * `echo "Useless string" >> file.txt` добавит строку *"Useless string"* в файл *file.txt*.<br>
* В случае использования `>` содержимое файла будет сначала удалено, а затем добавлена новая строка.<br>
  * `echo "Useless string" > file.txt` удалить содержимое файла *file.txt*, а затем добавит строку *"Useless string"*.<br>
## Игнорирование файлов в Git
* Часто в репозитории есть файлы, отслеживание и добавление которых не требуется. С помощью созданного в репозитории файла `.gitignore` мы можем перечислить те файлы, которые будут 
проигнорированы.<br>
* Можно перечислять файлы как поимённо по одному на строку, так и их шаблоны, что значительно упростит процесс составления `.gitignore` файла.<br>
* Правила, перечисленные в `.gitignore`, применяются только к *untracked* Файлам. Если файлы уже попали в *staging area*, то правила на них не распространяются.<br>
* Некоторые правила составления `.gitignore` файлов:<br>
  * Если необходимо проигнорировать все файлы с названием *debug.info* во всех папках и подпапках репозитория, то мы пишем название файла и его расширение.<br>
    * Если необходимо игнорировать файлы с именем *debug* независимо от расширения, то мы просто пишем его имя.<br>
  * Для игнорирования файлов с конкретным расширением, используется `*`. Например, `*.jpeg` проигнорирует все файлы с расширением *.jpeg* во всём репозитории.<br>
  * Так же символ `*` может использоваться и для обозначения количества папок (не более одной). Например, `folder/*/bump.txt` сообщит Git о необходимости проигнорировать файл 
*bump.txt*, который располагается в любой из сабдиректорий `folder`. (`folder/temp/bump.txt`, `folder/subf/bump.txt`. **НО** `folder/one/two/bump.txt` правилу не подчиняется.<br>
  * Для того, чтобы проигнорировать файл в любой сабдиректории, как бы 
глубоко в репозитории он не лежал, используется символ `**`. Например, `user/**/bump.txt` проигнорирует файл 
*bump.txt* как бы глубоко в поддиректориях он не находился.<br>
  * Правила `*` и `**` работают так же и для папок. 
  * Для формирования исключения из правила, мы ставим восклицательный знак. Например, файл `!car.jpeg` не будет проигнорирован, не смотря на то, что все остальные файлы с таким 
расширением игнорируются.<br>
  * Символом `[]` мы обозначаем вариативность части имени файла. Например `file[0-2].txt` сообщает Git о том, что файлы *file0.txt, file1.txt, file2.txt* необходимо 
проигнорировать.<br>
  * Символ `?` обозначает любой одинарный символ. С помощью него мы так же указываем на вариативность имени файла. Например `file?.txt` сообщит Git о необходимости проигнорировать все 
файлы, в имени которых есть *file + один символ + расширение .txt*.<br>
  * Слеш `/` относится к папкам. Если шаблон в *.gitignore* начинается с 
косой черты, то Git проигнорирует файлы или каталоги только в корневой 
директории. Например, `/file.txt` будет игнорироваться только в корневой 
директории, папка `build/` (но не файл с таким же именем) так же будет 
игнорироваться только в корневой директории.<br>
* Игнорируемые файлы не отображаются при выводе команды `git status`, но 
если их всё же необходимо просмотреть, то ключ `--ignored` даёт такую 
возможность. `git status --ignored` выведет все исключённые файлы и 
директории.<br>
* **Сам же файл .gitignore необходимо предварительно закоммитить, чтобы 
от не отображался в выводе.<br>
## Ветвление в Git
* Ветка - это отдельный поток разработки. В ней можно тестировать свои идеи, не мешая при этом основной разработке.<br>
* Фактически, ветка - это указатель на определённый коммит.
* По умолчанию главная ветка проекта называется *master* или *main*. Туда попадет уже проверенный, оттестированный и принятый командой код.<br>
* Командой `git branch` мы можем посмотреть список локальных веток репозитория. Текущая ветка обозначена символом `*`.<br>
## Создание веток
* Создать ветку можно с помощью команды `git branch branchName`. Будет создана ветка *branchName* от текущей ветки.<br>
  * Название ветки может содержать символы */.-_*. Например, *feature/fix-bug*, или *feature-fix-bug*, или *feature_fix_bug*.<br>
  * Называть ветки следует так, чтобы команда могла понять, что в ней происходит.<br>
  * Обычно, сначала идёт ключевое слово, обозначающее суть (*feature, fix*), а затем уже что конкретно делается (*add_branch_info*).<br>
## Переключение веток
* Переключиться с одной ветки на другую можно двумя способами:<br>
  * Если ветка уже создана, то командой `git checkout branchName` мы переключимся на ветку *branchName*.<br>
  * Если ветка ещё не создана, то командой `git checkout -b branchName` мы создадим ветку *branchName* и затем переключимся на неё.<br>
## Сравненине веток
* Сравнить ветки - `git diff branch1 branch2`.<br>
* Сравнивать ветки можно не только по их имени, но и два коммита между собой (ведь каждая ветка - это по сути указатель на последний коммит).<br>
  * Удобнее эти сравнения производить с помощью **суффикса навигации - `~`**. Он обозначает колличество коммитов, отсчитанных назад от текущего.<br>
  * Например, `git diff HEAD~2 HEAD` сравнит последний коммит в текущей ветке (*HEAD*) со вторым коммитом до него. **Нумерация начинается с 0**. Таким образом, `HEAD~0 - сам коммит, HEAD~1 - предыдущий коммит, HEAD~2 - предшествующий предыдущему коммит`.<br>
  * Есть специальное сокращение `HEAD~` - также значит *текущий коммит*.<br>
## Объединяем и удаляем ветки
* Процесс объединения своих наработок с основной веткой проекта называется *слиянием веток*, или *merge*.<br>
* Чтобы выполнить слияние, необходимо сделать два шага:<br>
  1. Переключить на ту ветку, **в которую** будет проводиться слияние.<br> 
  2. Выполнить слияние с другой веткой с помощью команды - `git merge branchToMerge`, где *branchToMerge* - имя ветки, которую мы сливаем.<br>
* После того, как мы слили обе ветки в одну, *branchToMerge* можно спокойно удалить. Делается это одной из двух команд:<br>
  * `git branch -d branchName`, если ветка *branchName* является частью основной ветки (была от неёё образована).<br>
  * `git branch -D branchName`, если ветка *branchName* не является частью основной ветки.<br>
* Если в момент удаление ветки мы находимся в ней же, то Git сообщит об ошибке *can not delete branch*.<br>
## Конфликты
* Когда сразу несколько членов команды работают над одним и тем же фрагментом проекта в разных ветках, при слиянии могут происходить конфликты.<br>
* Если Git не может провести слияние изменений автоматически, он сообщает о конфликте. Конфликт — это ситуация, в которой один или несколько человек модифицировали один и тот же файл. При этом результаты таких модификаций оказались несовместимы и разобраться в том, какой из вариантов правильный, может только человек.<br>
* Во время слияния Git сам подсвечивает файлы, которые не смог объединить. Чтобы разобраться в ситуации, нужно сделать следующее:<br>
  1. Заглянуть в файл, где произошёл конфликт.<br>
  2. Изучить обе стороны конфликта — вашу версию и версию вашего коллеги. Ваша задача — правильно собрать две версии в итоговую, так чтобы изменения обеих сторон не потерялись. Новая версия станет текущей актуальной.<br>
  3. Вручную удалить или подправить неактуальные изменения, если они есть.<br>
  4. Подготовить изменения к сохранению и сделать коммит.<br>
## Отправить локальную ветку в удалённый репозиторий
* Командой `git push` отправляем изменения в локальной ветке в удалённый репозиторий.<br>
* Сначала необходимо привязать локальный репозиторий к удалённому (при `git clone` происходит автоматически) командой `git remote add origin git@github.com:%ИМЯ_АККАУНТА%/git-branches.git`.<br>
* Командой `git push -u origin master` свяжем основную ветку в локальном репозитории с основной в удалённом.<br>
  * Запушить локальную ветку в удалённый репозиторий, где она **ещё не создана**: `git push -u origin branchName`.<br>
## Создание pull request
* В процессе командной работы следует внимательно следить за изменениями в файлах. Нельзя просто внести правки в своей ветке и сразу залить её в основную. Сначала ваши коллеги должны убедиться, что предложенные вами изменения логичны и эффективны.<br>
* Для этого используют механизм pull request (англ. «запрос на изменения»; буквально: «запрос на подтягивание»). В обиходе его обычно так и называют — «пул-реквест», или ещё короче — ПР или PR. Алгоритм такой:<br>
  * Вы трудитесь над задачей в своей ветке — например, пишете код новой функциональности.<br>
  * Вы заканчиваете работу, а затем создаёте пул-реквест.<br>
  * Ваши коллеги проверяют, что код выглядит аккуратно и лаконично, а программа работает корректно; также оставляют комментарии. Этот процесс называют code review (англ. «рассмотрение кода»), или просто ревью.<br>
  * После финального согласования вы заливаете свою ветку в основную.<br>
* Из чего состоит pull request и чем он может обернуться<br>
* У каждого пул-реквеста есть:<br>
  * **Название** — краткое описание предлагаемых изменений. Например: Адаптивный заголовок сайта, Замена альбома на галерею и так далее.<br>
  * **Описание** — развёрнутое описание изменений. Это поле заполнять необязательно, но желательно.<br>
  * **Исходная ветка** — та, в которой вы работали. Например, feature/merge-request.<br>
  * **Целевая ветка** — основная ветка проекта, в которую вы хотите внести изменения.<br>
* Также у каждого пул-реквеста может быть два исхода:<br>
  * **merge** (англ. «соединить») — предлагаемые изменения приняты; код вливается в целевую ветку; пул-реквест закрывается.<br>
  * **close** (англ. «закрыть») — пул-реквест закрывается без слияния изменений.<br>
## Забрать изменения из удалённого репозитория
* Командой `git pull` сделает две вещи: заберёт новые коммиты с удалённого репозитория и сольёт их с веткой *main/master*.<br>
* Когда над проектом работает целая команда, то основная ветка, как правило, успевает "убежать" на некоторое количество коммитов вперёд.<br>
* Поэтому перед тем, как создавать *pull request*, необходимо подтянуть изменения с удалённого репозитория в ветку *main* и слить её с той веткой, в которой работает разработчик, разрешив возможные конфликты. Делается это в несколько шагов:<br>

```bash

$ git checkout main # перешли в main

$ git pull # подтянули новые изменения в main

$ git checkout my-branch # вернулись в рабочую ветку my-branch

$ git merge main # влили main в новую ветку my-branch

$ git push -u origin my-branch # отправили ветку my-branch в удалённый репозиторий

```
