# Автоматическое обновление представлений при реорганизации

1. В TX, в диалоге "Изменение настроек информационной базы" на закладке "Общие" включаю опцию
   "Запустить SQL-скрипт после реорганизации базы".
2. В папке `T9\Data\<ИмяБазы>\SQLScripts` (появится после включения опции) создаю файл `RefreshViews.sql` содержащий
```
--select name, modify_date from sys.views
declare @view sysname
declare cViews cursor for 
select name from sys.views 
open cViews
fetch next from cViews into @view
while @@FETCH_STATUS = 0 begin
        exec sp_refreshview @view
        fetch next from cViews into @view
end
close cViews
deallocate cViews
```
3. В папке `T9\Data\<ИмяБазы>` создаю файл `SQLScripts.xml` содержащий
```xml
<?xml version="1.0" encoding="windows-1251"?>
<AfterRebuild>
  <SQLScript Base="" File="RefreshViews.sql"/>
</AfterRebuild>
```

После следующей реорганизации (любой) отработать скрипт, обновляющий все вьюшки всех подключенных к инфобазе баз данных.
Чтобы проверить, что обновление вьюшек прошло успешно, можно выполнив запрос `select name, modify_date from sys.views`, и убедиться что `modify_date` вьюшек соответствует дате реорганизации.
