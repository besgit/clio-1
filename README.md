Bpmonline Command Line Interface (bpmcli)
=============================

Проект предназначен для интеграции систем разработки и CI/CD
c платформой bpmonline версии 7.13.0 и выше

Возможности bpmcli:
* Перезапуск приложения
* Формирование пакета из файловой системы
* Установка пакета в приложение
* Загрузка/выгрузка пакета в приложение при работе в РФС
* Установка пакета из архива
* Сжатие проекта в пакет

INSTALLATION
---------------------

Для установки bpmcli необходимо выполнить регистрационный файл register.cmd
входящий в пакет поставки. Если нет необходимости получить глобальную команду
bpmcli можно пользоваться командой для запуска dotnet #Path to cli#bpmcli.dll и 
передать необходимые аргументы

COMMANDS
---------------------

### Перезапуск приложения

Перезапуск приложения с выгрузкой домена

```powershell
bpmcli restart
```
### Настройка окружения

Создание нового окружения: имя , путь к сайту, логин и пароль для подключения
```powershell
bpmcli cfg -e dev -u http://mysite.bpmonline.com -l user -p pa$$word
```
Установка окружения по умолчанию
```powershell
bpmcli cfg -a dev
```
Измененение параметра существущего окружения
```powershell
bpmcli cfg -e dev -p pa$$word
```

Удаление окружения
```powershell
bpmcli remove -e dev
```

Использование неосновного окружения при вызове команд

```powershell
bpmcli restart -e dev
```

### Использование в CI\CD

В системах CI\CD можно не использовать файл конфигурации и передавать параметры
напрямую при каждом вызове команды

```powershell
bpmcli restart -u http://mysite.bpmonline.com -l administrator -p pa$$word
```

### Сжатие проекта в архив пакета

Для подготовки пакета в формате gz для установки в целевую среду, необходимо
выполнить операцию compress, параметры  -s путь к папке пакета, -d имя файла
результирующего архива

```powershell
bpmcli compress -s C:\bpmonline\src\mypackage -d C:\bpmonline\pkg\mypackage.gz
```

### Установка пакета из архива

Для уcтановки пакета в формате gz необходимо воспользоваться командой install

```powershell
bpmcli install -f C:\bpmonline\pkg\mypackage.gz
```
Для загрузки контента пакета из файловой системы в приложение

### Загрузка/выгрузка конента пакета в приложение

Для загрузки контента пакета в приложения из файловой системы


```powershell
bpmcli fetch -o upload -p PackageName
```

Для выгрузки контента пакета из приложения в файловую систему

```powershell
bpmcli fetch -o download -p PackageName
```