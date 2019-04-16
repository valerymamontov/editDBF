## Небольшой обработчик DBF-файла
![Image alt](https://github.com/valerymamontov/screenshots/blob/master/EditDBF.png)

Обработчик писался под Windows Server 2003 (x86).

Для работы программы необходимо установить компонент Microsoft OLE DB Provider for Visual FoxPro 9.0.
Без него DBF-файл не обработается, появится ошибка, что "Поставщик VFPOLEDB.1 не зарегистрирован на локальном компьютере".

Ссылка на компонент (поставщик) - https://www.microsoft.com/en-us/download/details.aspx?id=14839

### Механизм работы
 1. Программа открывает DBF-файл, переносит из него все строки в DataSet. 
 2. Редактирует данные и записывает их в новый Dataset.
 3. Сохраняет в новый файл.

### Проблемы с ODBC и OLEDB
Сначала для обработки DBF-файла я использовал ODBC и OLEDB, но столкнулся с несколькими проблемами. 
Если путь к исходному файлу содержал пробелы, то при открытии DBF появлялась ошибка.
Если длина имени DBF-файла содержала более восьми символов, тоже появлялась ошибка.
Чтобы обойти эти ошибки, приходилось копировать DBF-файл в директорию без пробелов и обрезать имя файла.

И в итоге я решил остановиться на VFPOLEDB.

### Полезные ссылки
 1. [Если имя таблицы более восьми символов, то возникает ошибка](https://social.msdn.microsoft.com/Forums/ru-RU/06a350bb-4447-4893-8cf8-ed2bbdedfe37/-dbf-oledbconnection?forum=fordesktopru)
 2. [В конце таблицы создаёт пустую колонку "_NullFlags"](https://stackoverflow.com/questions/30886730/adding-data-to-dbf-file-adds-column-nullflags)
