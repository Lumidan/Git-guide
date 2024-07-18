# Git Guide
## Базовы команды
1. pwd - print working directory - показать рабочую папку
2. cd - change directory - сменить директорию
3. ls - list directory - отобразить содержимое директории
4. touh %имяФайла% - создать файл
5. mkdir %имяДиректории% - создать директорию
6. cp %что_копируем куда_копируем% - copy - копировать файл
7. mv  %что_перемещаем куда_перемещаем% - move - переместить
8. cat %имя_файла% - concatenate and print - чтение файлов
9. rm %имя_файла% - remove - удалить файл
10. rmdir %имя_папки% - remove directory - удалить директорию
11. git config --global user.name - configuration - указание имени
12. git config --global user.email - configuration - указание почты
13. git init - initialize - инициализировать Git-репозиторий
14. git status - состояние репозитория
15. git add - подготовить файлы в репозитории к сохранению
16. git commit -m - сделать коммит(сохранение) с сообщением 
17. git log - log - журнал - посмотреть историю коммитов
18. git push -u %имя_удаленного_репозитория% %название ветки% - push - толкать - синхронизация изменений с удаленным репозиторием (1 раз с флажком `-u`)
----
## Полезная информация
- Команды не обязательно выполнять по одной. Вместо этого можно воспользоваться амперсандами (&&)
- В самом терминале можно переключаться по буферу с помощью стрелочек, тем самым экономя время
- Также в терминале можно использовать клавишу Tab для автозаполнения и поиска нужных команд/папок по первым символам
- символ ~ обозначает домашнюю директорию; символ . обозначает текущую директорию; символ .. обозначает верхнюю в иерархии директорию
- / - корневая дирректория для UNIX. Диски с:/ и тп. - корневая директория для Windows
- Все глобальные настройки Git хранит в файле .gitconfig в домашней директории. Чтобы убедиться в этом, можно вызвать команду для чтения файлов.
```
{
    $ cat ~/.gitconfig
}
```
- `ls -a` - показывает также скрытые файлы и папки, названия которых начинаются с символа '.'
- `rm -r %имя_директории%` - Удаление с флагом рекурсии т.е. удаление папки и всего содержиомго
- Если вы случайно сделали Git-репозиторием не ту папку, её можно «разгитить». Для этого нужно удалить скрытую подпапку .git
```
{
    rm -rf .git #r - recursive, f - force - заставить
}
```
- флаг `-all` позволяет обратиться ко всему (например в git add)
- 

----
## инструкция по созданию репозитория на GitHub
1. Зайдите в свой профиль по ссылке https://github.com/username, где username — имя, которое вы указали при регистрации.
2. Создайте репозиторий. Для этого перейдите на вкладку Repositories (англ. «репозитории»), а затем нажмите на зелёную кнопку New (англ. «новый») справа.
3. Открылось окно создания нового репозитория. Назовите его как пожелаете. Смело нажимайте на зелёную кнопку Create repository (англ. «создать репозиторий») внизу.
Готово! Далее по инструкции от самого GitHub нужно связать удаленный репозиторий с локальным. Но прежде, чтобы упростить работу с GitHub и сделать её более безопасной, нужно сгенерировать SSH-ключи 
----
## инструкция по генерации SSH-ключа
1. Для генерации SSH-пары можно использовать программу `ssh-keygen`. Откройте терминал и введите одну из команд.
```
{
    $ ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"
    $ ssh-keygen -t rsa -b 4096 -C "электронная почта, к которой привязан ваш аккаунт на GitHub" 
}
```
2. Укажите место хранения ключей. Простой вариант — сделать домашний каталог пользователя путём по умолчанию. Для этого нажмите `Enter`. Теперь в указанной директории появится пара ключей.
3. Программа запросит кодовую фразу (англ. passphrase) для доступа к SSH-ключу. Вы можете оставить поле пустым. Для этого нажмите `Enter`, а затем ещё раз `Enter` для подтверждения.
4. Готово! Теперь осталось проверить, что ключи действительно сгенерировались. Для этого вызовите эту команду:
```
{
    ls -a ~/.ssh 
}
```
На экране должны появиться два файла — один с расширением `.pub`, другой — без. Файл в `.pub` — публичный, им можно делиться с веб-сайтами или коллегами. Файл без расширения `.pub` — приватный. Ни в коем случае не передавайте его никому! 
----
## Привязываем SSH-ключ к GitHub
1. После выполнения команды ssh-keygen из предыдущего урока в директории `~/.ssh` будет создано два файла — `id_ed25519` и `id_ed25519.pub` (или `id_rsa` и `id_rsa.pub` — в зависимости от того, какой алгоритм вы использовали). Скопируйте содержимое файла с публичным ключом в буфер обмена.
```
{
    $ clip < ~/.ssh/id_rsa.pub
    # для ed25519:
    $ clip < ~/.ssh/id_ed25519.pub
}
```
Если `clip` не сработает, выведите содержимое файла с помощью `cat ~/.ssh/id_rsa.pub` или `cat ~/.ssh/id_ed25519.pub` и скопируйте вывод в буфер обмена из консоли.
2. Перейдите на GitHub и выберите пункт **Settings** (англ. «настройки») в меню аккаунта.
3. В меню слева нажмите на пункт **SSH and GPG keys**.
4. В открывшейся вкладке выберите **New SSH key** (англ. «новый SSH-ключ»).
5. В поле **Title** (англ. «заголовок») напишите название ключа. Например, **Personal key** (англ. «личный ключ»).
6. В поле **Key type** (англ. «тип ключа») должно быть **Authentication Key** (англ. «ключ аутентификации»).
7. В поле **Key** скопируйте ваш ключ из буфера обмена.
8. Нажмите на кнопку **Add SSH key** (англ. «добавить SSH-ключ»). 
9. Проверьте правильность ключа с помощью следующей команды:
```
{
    $ ssh -T git@github.com
}
```
Если это первый раз, когда вы используете Git, чтобы поделиться проектом на GitHub, появится похожее предупреждение:
```
{
    The authenticity of host 'github.com (140.82.121.4)' can't be established. ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU. This key is not known by any other names. Are you sure you want to continue connecting (yes/no/[fingerprint])?
}
```
##
Это предупреждение сообщает, что вы никогда не соединялись с сервером GitHub. Поэтому Git не может гарантировать, что сервер является тем, за кого он себя выдаёт.
Для подтверждения подлинности сервер генерирует и публикует ключи SHA256. Вы можете проверить ключи GitHub по [этой ссылке](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints). Если ключ в предупреждении совпадает с тем, что вы видите на сайте, значит, сервер является действительным. Введите `yes`, чтобы продолжить. Вы увидите приветствие на экране.
---
## Привязать удалённый репозиторий к локальному - `git remote add`
- Перейдите на страницу удалённого репозитория, выберите тип SSH и скопируйте URL. Кнопка справа позволит сделать это мгновенно.
- Откройте консоль, перейдите в каталог локального репозитория и введите команду git remote add (от англ. remote — «удалённый» и add — «добавить»). Команде необходимо передать два параметра: имя удалённого репозитория и его URL. В качестве имени используйте слово `origin`. А URL вы скопировали со страницы удалённого репозитория.
```
{
    $ cd ~/dev/first-project
    $ git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git
}
```
### Убедиться, что репозитории связаны, — `git remote -v`
Отлично: вы связали локальный репозиторий с удалённым. Осталось убедиться, что всё работает, с помощью следующей команды:
```
{
    $ git remote -v
    origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (fetch)
    origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (push)
}
```
В выводе вы должны увидеть две строчки, аналогичные тем, что показаны выше.
Флаг `-v` — короткая форма флага `--verbose` (англ. «подробный»). Он позволяет показать больше информации в выводе.

# На этом краткая инструкция окончена!