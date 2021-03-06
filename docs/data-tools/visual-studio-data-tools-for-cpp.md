---
title: Visual Studio data tools для C++
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CPP
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
- cplusplus
ms.openlocfilehash: fe50ecd01b8f3112340510a78f76d6e380ec3136
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/29/2018
ms.locfileid: "37117034"
---
# <a name="visual-studio-data-tools-for-c"></a>Visual Studio data tools для C++

Часто, когда вы обращаетесь к источникам данных для машинного кода C++ можно обеспечивают наибольшую производительность. Тем не менее данные, инструментарий для приложений на C++ в Visual Studio не полна, как и для приложений .NET. Например windows источников данных не может использоваться для перетаскивания источников данных в область конструктора C++. Если вам нужна объектно реляционного слоя, имеется возможность использовать сторонние продукты или написать собственный.  То же самое касается функциональность привязки к данным, несмотря на то, что приложения, использующие библиотеку классов Microsoft Foundation можно использовать некоторые классы баз данных вместе с документами и представлениями, для хранения данных в памяти и отображения ее пользователю. Дополнительные сведения см. в разделе [доступ к данным в Visual C++](/cpp/data/data-access-in-cpp).

Чтобы подключиться к базам данных SQL, приложений C++ неуправляемого кода можно использовать драйверы ODBC и OLE DB и поставщик ADO, входят в состав Windows. Они могут подключиться к любой базе данных, который поддерживает эти интерфейсы. Драйвер ODBC является стандартом. OLE DB предоставляется для обеспечения обратной совместимости. Дополнительные сведения о технологии этих данных, см. в разделе [Windows Data Access Components](https://msdn.microsoft.com/library/windows/desktop/aa968814.aspx).

Чтобы воспользоваться преимуществами пользовательские функциональные возможности в SQL Server 2005 и более поздней версии, используйте [собственный клиент SQL Server](/sql/relational-databases/native-client/sql-server-native-client). Собственный клиент также содержит, драйвер ODBC для SQL Server и поставщика SQL Server OLE DB в одну собственную динамическую библиотеку (DLL). Они поддерживают приложений, использующих API машинного кода (ODBC, OLE DB и ADO) для Microsoft SQL Server.  Собственный клиент SQL Server устанавливается вместе с SQL Server Data Tools. Руководство по программированию находится здесь: [программирование SQL Server Native Client](/sql/relational-databases/native-client/sql-server-native-client-programming).

## <a name="to-connect-to-localdb-through-odbc-and-sql-native-client-from-a-c-application"></a>Для подключения к localDB через ODBC и собственный клиент SQL из приложения C++

1.  Установка SQL Server Data Tools.

2.  Если вам требуется образец базы данных SQL для подключения к, скачайте базы данных Northwind и распакуйте его в новое расположение.

3.  Используйте SQL Server Management Studio для присоединения распакованный *Northwind.mdf* файл в localDB. При запуске SQL Server Management Studio подключитесь к (localdb) \MSSQLLocalDB.

     ![Диалоговое окно подключения SSMS](../data-tools/media/raddata-ssms-connect-dialog.png)

     Затем щелкните правой кнопкой мыши на узле localdb в области слева и выберите **Attach**.

     ![SSMS присоединения базы данных](../data-tools/media/raddata-ssms-attach-database.png)

4.  Загрузите образец ODBC Windows SDK и распакуйте его в новое расположение. Этот образец показывает основные команды ODBC, которые используются для подключения к базе данных и отправлять запросы и команды. Дополнительные сведения об этих функциях в [Microsoft Open Database Connectivity (ODBC)](/sql/odbc/microsoft-open-database-connectivity-odbc). При первой загрузке решения (он находится в папке C++), Visual Studio предложит установить обновление решения до текущей версии Visual Studio. Нажмите кнопку **Да**.

5.  Чтобы использовать собственный клиент, необходимо сначала его *заголовок* файл и *lib* файл. Эти файлы содержат функции и определений, относящихся к SQL Server, за пределами функции ODBC, определенные в sql.h. В **проекта** > **свойства** > **каталоги VC ++**, добавьте каталог включаемых следующее:

**%ProgramFiles%\Microsoft SQL Server\110\SDK\Include**

И этот каталог библиотеки:

**%ProgramFiles%\Microsoft SQL Server\110\SDK\Lib**

6.  Добавьте следующие строки в *odbcsql.cpp*. #Define предотвращает несоответствующие определений OLE DB из компиляции.

    ```cpp
    #define _SQLNCLI_ODBC_
    #include <sqlncli.h>
    ```

    Обратите внимание, что пример не использует любые возможности собственного клиента, поэтому описанные выше шаги не обязательны для того, чтобы скомпилировать и запустить. Но теперь проект настроен для использования этой функции. Дополнительные сведения см. в разделе [программирование собственного клиента SQL Server](/sql/relational-databases/native-client/sql-server-native-client).

7.  Укажите, какой драйвер следует использовать в подсистеме ODBC. Образец передает атрибут строки подключения ДРАЙВЕРА в качестве аргумента командной строки. В **проекта** > **свойства** > **Отладка**, добавьте следующий аргумент команды:

    ```cpp
    DRIVER="SQL Server Native Client 11.0"
    ```

8.  Нажмите клавишу **F5**, чтобы выполнить сборку приложения и запустить его. Вы увидите диалоговое окно, в драйвер, который необходимо ввести базы данных. Введите `(localdb)\MSSQLLocalDB`и проверьте **использовать доверительное соединение**. Нажмите клавишу **ОК**. Вы должны увидеть консоли с помощью сообщений, указывающих успешное подключение. Вы также увидите командную строку для ввода в инструкции SQL. На следующем рисунке показано пример запроса и результаты:

     ![Выходные данные запроса пример ODBC](../data-tools/media/raddata-odbc-sample-query-output.png)

## <a name="see-also"></a>См. также

- [Доступ к данным в Visual Studio](../data-tools/accessing-data-in-visual-studio.md)