**git sparse-checkout** сокращает локальный каталог до подмножества отслеживаемых файлов

#### Пример
Чтобы из репозитория Isola.TX взять только пару нужных проектов делаю
```
git clone --sparse https://github.com/turbotechnology/Isola.TX.git
cd repo Isola.TX
git sparse-checkout set FrameWork/Base/hISOLABase FrameWork/Lib/IsolaBlender
```
Обратить внимание на слеши в команде `git sparse-checkout set`.  

#### Основные команды

Включить `git sparse-checkout init --cone`  
Так же этот режим может быть включен при клонировании `git clone --sparse <URL>`

Добавить каталог `git sparse-checkout add src/frontend`

Установить список каталогов `git sparse-checkout set каталог1 каталог2`

Просмотр списка каталогов `git sparse-checkout list`

Отключить `git sparse-checkout disable`

Список отслеживаемых каталогов находится в файле `.git/info/sparse-checkout`

Для `git clone` есть параметр `--filter=blob:none` сокращающий объём выкачеваемого. 
Его не использую, т.к. с ним Git Extensions даёт ошибку unable to update remote pushurl.
Но при работе через командную строку он может быть полезен.
