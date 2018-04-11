---
title: Исправление необнаруживаемых динамических параметров в веб-тесте производительности в Visual Studio | Документы Майкрософт
ms.date: 10/19/2016
ms.topic: article
helpviewer_keywords:
- walkthroughs, load tests
- load tests, walkthroughs
- load tests, correlating dynamic parameters
ms.assetid: 92dff25c-36ee-4135-acdd-315c4962fa11
author: gewarren
ms.author: gewarren
manager: ghogen
ms.technology: vs-ide-test
ms.openlocfilehash: dc92b65ba26b11fe65919fd94ac16c8480427f6b
ms.sourcegitcommit: 900ed1e299cd5bba56249cef8f5cf3981b10cb1c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/19/2018
---
# <a name="fix-non-detectable-dynamic-parameters-in-a-web-performance-test"></a>Исправление необнаруживаемых динамических параметров в веб-тесте производительности

Некоторые веб-сайты используют динамические параметры для обработки части веб-запросов. Динамический параметр — это параметр, значение которого воссоздается при каждом выполнении приложения пользователем. Примером динамического параметра является идентификатор сеанса. Идентификатор сеанса обычно изменяется каждые 5 — 30 минут. Средство записи веб-тестов производительности и модуль воспроизведения автоматически обрабатывают самые распространенные типы динамических параметров.

-   Значения динамических параметров, устанавливаемые в значении cookie. Модуль веб-тестов производительности автоматически обрабатывает эти параметры при воспроизведении.

-   Значения динамических параметров, устанавливаемые в скрытых полях на HTML-страницах, например состояние представления ASP.NET. Эти параметры автоматически обрабатываются средством записи, добавляющим в тест правила извлечения скрытых полей.

-   Значения динамических параметров, устанавливаемые в качестве строки запроса или параметров отправки формы. Эти параметры обрабатываются через обнаружение динамических параметров после записи веб-теста производительности.

Некоторые типы динамических параметров не обнаруживаются. Необнаруженный динамический параметр может приводить к ошибкам при выполнении веб-тестов производительности, поскольку динамические значения чаще всего изменяются при каждом запуске теста. Для правильной обработки этих параметров можно вручную добавить в веб-тесты производительности правила извлечения динамических параметров.

## <a name="create-and-run-a-web-app-with-dynamic-parameters"></a>Создание и запуск веб-приложения с динамическими параметрами

Чтобы проиллюстрировать обнаруживаемые и необнаруживаемые динамические параметры, мы создадим простое веб-приложение ASP.NET с тремя веб-формами с несколькими элементами управления и пользовательским кодом. Затем мы рассмотрим способы изоляции и обработки динамических параметров.

1.  Создайте новый проект ASP.NET DynamicParamaterSample.

     ![Создание пустого проекта веб-приложения ASP.NET](../test/media/web_test_dynamicparameter_aspproject.png "Web_Test_DynamicParameter_ASPProject")

2.  Добавьте веб-форму Querystring.aspx.

3.  В конструкторе перетащите HiddenField на страницу и затем измените значение свойства (ID) на HiddenFieldSessionID.

     ![Добавление элемента HiddenField](../test/media/web_test_dynamicparameter_hiddenfield.png "Web_Test_DynamicParameter_HiddenField")

4.  Перейдите к представлению исходного кода страницы Querystring и добавьте следующий выделенный код ASP.NET и JavaScript, используемый для моделирования динамических параметров идентификатора сеанса:

    ```html
    <head runat="server">
    <title>JavaScript dynamic property correlation sample</title><script type="text/javascript" language="javascript">    <!--        function jScriptQueryString()         {            var Hidden = document.getElementById("HiddenFieldSessionID");            var sessionId = Hidden.value;            window.location = 'JScriptQuery.aspx?CustomQueryString=jScriptQueryString___' + sessionId;         }    //--></script>
    </head>
    <body>
        <form id="form1" runat="server">
        <div>
             <a name="QuerystringHyperlink" href="ASPQuery.aspx?CustomQueryString=ASPQueryString___<%= Session.SessionID %>">Dynamic querystring generated by ASP.net</a>         <br/>         <br/>         <a href="javascript:jScriptQueryString()">Dynamic querystring generated by javascript </a>
        </div>
        <asp:HiddenField ID="HiddenFieldSessionID" runat="server" />
        </form>
    </body>
    </html>
    ```

5.  Откройте файл Querystring.aspx.cs и добавьте следующий выделенный код в метод Page_Load:

    ```csharp
    public partial class Querystring : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            Session.Add("Key", "Value");HiddenFieldSessionID.Value = Session.SessionID;
        }
    }
    ```

6.  Добавьте вторую веб-форму с именем ASPQuery.aspx.

7.  В конструкторе перетащите элемент Label на страницу и измените значение его свойства (ID) на IndexLabel.

     ![Добавление надписи в веб-форму](../test/media/web_test_dynamicparameter_label.png "Web_Test_DynamicParameter_Label")

8.  Перетащите элемент HyperLink на страницу и измените значение его свойства Text на Back.

     ![Добавление гиперссылки в веб-форму](../test/media/web_test_dynamicparameter_hyperlink.png "Web_Test_DynamicParameter_Hyperlink")

9. Нажмите кнопку (…) для свойства NavigationURL.

     ![Редактирование свойства NavigateURL](../test/media/web_test_dynamicparameter_hyperlink_navurl.png "Web_Test_DynamicParameter_Hyperlink_NavURL")

     Выберите Querystring.aspx.

     ![Выбор URL-адреса Querystring.aspx](../test/media/web_test_dynamicparameter_hyperlink_navurl2.png "Web_Test_DynamicParameter_Hyperlink_NavURL2")

10. Откройте файл ASPQuery.aspx.cs и добавьте следующий выделенный код в метод Page_Load:

    ```csharp
    protected void Page_Load(object sender, EventArgs e)
            {
                int index;            string qstring;            string dateportion;            string sessionidportion;            qstring = Request.QueryString["CustomQueryString"];            index = qstring.IndexOf("___");            dateportion = qstring.Substring(0, index);            index += 3;            sessionidportion = qstring.Substring(index, qstring.Length - index);            if (sessionidportion != Session.SessionID)            {                Response.StatusCode = 401;                IndexLabel.Text = "Failure!  Invalid querystring parameter found.";            }            else            {                IndexLabel.Text = "Success.  Dynamic querystring parameter was found.";            }            IndexLabel.Text += "<br>\r\n";
            }
    ```

11. Добавьте третью веб-форму с именем JScriptQuery.aspx.

     Как и для второй страницы, перетащите метку в форму, задав свойству (ID) значение IndexLabel, а затем перетащите гиперссылку в форму, задав свойству Text значение Back, а свойству NavigationURL — Querystring.aspx.

     ![Добавление и настройка третьей веб-формы](../test/media/web_test_dynamicparameter_addwebform3.png "Web_Test_DynamicParameter_AddWebForm3")

12. Откройте файл JScriptQuery.aspx.cs и добавьте следующий выделенный код в метод Page_Load:

    ```csharp
    protected void Page_Load(object sender, EventArgs e)
            {
                int index;            string qstring;            string dateportion;            string sessionidportion;            qstring = Request.QueryString["CustomQueryString"];            index = qstring.IndexOf("___");            dateportion = qstring.Substring(0, index);            index += 3;            sessionidportion = qstring.Substring(index, qstring.Length - index);            if (sessionidportion != Session.SessionID)            {                Response.StatusCode = 401;                IndexLabel.Text = "Failure!  Invalid querystring parameter found.";            }            else            {                IndexLabel.Text = "Success.  Dynamic querystring parameter was found.";            }            IndexLabel.Text += "<br>\r\n";
            }
    ```

13. Сохраните проект.

14. В обозревателе решений выберите Querystring.aspx в качестве начальной страницы.

     ![Задание начальной страницы в Querystring.aspx](../test/media/web_test_dynamicparameter_setstartpage.png "Web_Test_DynamicParameter_SetStartPage")

15. Нажмите сочетание клавиш CTRL+F5, чтобы запустить веб-приложение в браузере. Скопируйте URL-адрес. Он потребуется при записи теста.

16. Попробуйте обе ссылки. Обе должны открывать сообщение "Успех. Dynamic querystring parameter found".

     ![Запуск веб-приложения](../test/media/web_test_dynamicparameter_runapp.png "Web_Test_DynamicParameter_RunApp")

     ![Успешный запуск](../test/media/web_test_dynamicparameter_runapp2.png "Web_Test_DynamicParameter_RunApp2")

## <a name="create-a-web-performance-test"></a>Создание веб-теста производительности

1.  Добавьте в решение проект веб-тестов производительности и нагрузочных тестов.

     ![Добавление проекта веб-тестов производительности и нагрузочных тестов](../test/media/web_test_dynamicparameter_addtestproject.png "Web_Test_DynamicParameter_AddTestProject")

2.  Переименуйте WebTest1.webtest в DynamicParameterSampleApp.webtest.

     ![Переименование веб-теста производительности](../test/media/web_test_dynamicparameter_renametest.png "Web_Test_DynamicParameter_RenameTest")

3.  Запишите тест.

     ![Запись веб-теста производительности](../test/media/web_test_dynamicparameter_recordtest.png "Web_Test_DynamicParameter_RecordTest")

4.  Скопируйте URL-адрес с тестируемого веб-сайта в браузер.

     ![Вставка URL-адреса с тестируемого веб-сайта](../test/media/web_test_dynamicparameter_recordtest2.png "Web_Test_DynamicParameter_RecordTest2")

5.  Выполните какие-либо переходы в веб-приложении. Выберите ссылку ASP.NET, ссылку "Назад", а затем ссылку "JavaScript" и ссылку "Назад".

     Средство записи веб-тестов отображает URL-адреса HTTP-запроса и ответа по мере навигации по веб-приложению.

6.  Нажмите кнопку "Стоп" в средстве записи тестов.

     В диалоговом окне обнаружения динамических параметров отображается индикатор выполнения, показывающий состояние обнаружения параметров в полученных HTTP-ответах.

7.  Динамический параметр для CustomQueryString на странице ASPQuery обнаруживается автоматически. При этом динамический параметр для CustomQueryString на странице JScriptQuery не обнаружен.

     Нажмите кнопку "ОК", чтобы добавить правило извлечения в Querystring.aspx, привязав его к странице ASPQuery.

     ![Повышение уровня обнаруженного динамического параметра](../test/media/web_test_dynamicparameter_promotedialog.png "Web_Test_DynamicParameter_PromoteDialog")

     Правило извлечения добавляется в первый запрос для Querystring.aspx.

     ![Правило извлечения, добавленное в запрос](../test/media/web_test_dynamicparameter_autoextractionrule.png "Web_Test_DynamicParameter_AutoExtractionRule")

     В дереве запросов страницы ASPQuery.aspx разверните второй запрос и обратите внимание, что значение параметра CustomQueryString привязано к правилу извлечения.

     ![CustomQueryString, привязанная к правилу извлечения](../test/media/web_test_dynamicparameter_autoextractionrule2.png "Web_Test_DynamicParameter_AutoExtractionRule2")

8.  Сохраните тест.

## <a name="run-the-test-to-isolate-the-non-detected-dynamic-parameter"></a>Выполнение теста с изоляцией неопределенного динамического параметра

1.  Запустите тест.

     ![Запуск веб-теста производительности](../test/media/web_test_dynamicparameter_runtest.png "Web_Test_DynamicParameter_RunTest")

2.  Четвертый запрос страницы JScriptQuery.aspx заканчивается ошибкой. Перейдите к веб-тесту.

     ![Ошибка динамического параметра в результатах теста](../test/media/web_test_dynamicparameter_runresults.png "Web_Test_DynamicParameter_RunResults")

     Узел запроса страницы JScriptQuery.aspx выделен в редакторе. Разверните узел и обратите внимание, что часть "1v0yhyiyr0raa2w4j4pwf5zl" в CustomQueryString кажется динамической.

     ![Потенциальный динамический параметр в CustomQueryString](../test/media/web_test_dynamicparameter_runresults2.png "Web_Test_DynamicParameter_RunResults2")

3.  Вернитесь в средство просмотра результатов веб-тестов производительности и выберите страницу JScriptQuery.aspx, на которой произошла ошибка. Перейдите на вкладку запроса, убедитесь, что снят флажок отображения необработанных данных, прокрутите вниз и выберите быстрый поиск в CustomQueryString.

     ![Использование быстрого поиска для локализации динамического параметра](../test/media/web_test_dynamicparameter_runresultsquckfind.png "Web_Test_DynamicParameter_RunResultsQuckFind")

4.  Из редактора тестов известно, что параметру CustomQueryString запроса страницы JScriptQuery.aspx присвоено значение `jScriptQueryString___1v0yhyiyr0raa2w4j4pwf5zl` и часть строки "1v0yhyiyr0raa2w4j4pwf5zl", вероятно, формируется динамически. Удалите из раскрывающегося списка "Найти" эту часть строки поиска. Строка должна выглядеть следующим образом: "CustomQueryString=jScriptQueryString___".

     Значения присваиваются динамическим параметрам в одном из запросов, который предшествует запросу, завершившемуся ошибкой. Установите флажок "Искать назад" и нажимайте кнопку "Найти далее" до тех пор, пока на панели "Запрос" не будет выделен предыдущий запрос страницы Querystring.aspx. Этот запрос должен появиться после троекратного нажатия кнопки "Найти далее".

     ![Использование быстрого поиска для локализации динамического параметра](../test/media/web_test_dynamicparameter_runresultsquckfind4.png)

     Как показано на вкладке ответов и как видно в ранее реализованном коде JavaScript, параметру строки CustomQueryString присвоено значение " jScriptQueryString___", к которому также добавляется значение, возвращаемое переменной sessionId.

    ```
    function jScriptQueryString()          {             var Hidden = document.getElementById("HiddenFieldSessionID");             var sessionId = Hidden.value;             window.location = 'JScriptQuery.aspx?CustomQueryString=jScriptQueryString___' + sessionId;          }

    ```

     Теперь мы знаем, где возникает ошибка, и нам необходимо извлечь значение для sessionId. Однако извлеченное значение является простым текстом, поэтому необходимо продолжить обнаружение ошибки и попытаться найти строку, в которой отображается действительное значение sessionId. Анализируя код, можно увидеть, что значение переменной sessionId равно значению, возвращаемому параметром HiddenFieldSessionID.

5.  Используйте быстрый поиск в HiddenFieldSessionID, сняв флажок "Поиск назад" и выбрав текущий запрос.

     ![Использование быстрого поиска по HiddenFieldSession](../test/media/web_test_dynamicparameter_runresultsquckfindhiddensession.png "Web_Test_DynamicParameter_RunResultsQuckFindHiddenSession")

     Обратите внимание, что возвращаемое значение не совпадает со строкой из исходной записи веб-теста производительности. Для данного тестового запуска возвращенное значение — "5w4v3yrse4wa4axrafykqksq", а в исходной записи значение было "1v0yhyiyr0raa2w4j4pwf5zl". Возвращаемое значение не совпадает с исходной записью, поэтому создается ошибка.

6.  Поскольку нужно исправить динамический параметр в исходной записи, выберите записанный результат на панели инструментов.

     ![Выбор записанного результата](../test/media/web_test_dynamicparameter_recordedresult.png "Web_Test_DynamicParameter_RecordedResult")

7.  В записанных результатах выберите третий запрос, который представляет собой тот же запрос Querystringrequest.aspx, который был изолирован в результатах тестового запуска.

     ![Выбор того же запроса в записанных результатах](../test/media/web_test_dynamicparameter_recordedresultsselectnode.png "Web_Test_DynamicParameter_RecordedResultsSelectNode")

     Откройте вкладку отклика, прокрутите вниз и выберите исходное значение динамического параметра "1v0yhyiyr0raa2w4j4pwf5zl", которое было изолировано ранее, и добавьте правило извлечения.

     ![Добавление правила извлечения для динамического параметра](../test/media/web_test_dynamicparameter_recordedresultaddextractionrule.png "Web_Test_DynamicParameter_RecordedResultAddExtractionRule")

     Новое правило извлечения добавляется к запросу Querystring.aspx и ему присваивается значение "Param0".

     Если диалоговое окно сообщает, что обнаружены совпадения для извлеченного текста, к которым можно привязать параметр, нажмите кнопку "Да".

     ![Правило извлечения создано](../test/media/web_test_dynamicparameter_addextractiondialog.png "Web_Test_DynamicParameter_AddExtractionDialog")

8.  Нажмите кнопку "Найти далее". Первое совпадение — это совпадение, которые необходимо изменить, то есть параметр для CustomQueryString на странице JScriptQuery.

     ![Поиск и замена текста параметром](../test/media/web_test_dynamicparameter_addextractionfindreplace.png "Web_Test_DynamicParameter_AddExtractionFindReplace")

9. Нажмите кнопку "Заменить".

     ![Замена текста параметром](../test/media/web_test_dynamicparameter_addextractionfindreplace2.png "Web_Test_DynamicParameter_AddExtractionFindReplace2")

     Параметр QueryString в запросе JScriptQuery.aspx обновляется новым параметром контекста: CustomQueryString=jScriptQueryString___{{Param0}}.

     ![Параметр, примененный к QueryString](../test/media/web_test_dynamicparameter_addextractionfindreplace3.png "Web_Test_DynamicParameter_AddExtractionFindReplace3")

10. Закройте диалоговое окно "Найти и заменить". Обратите внимание на схожесть структуры дерева запросов для обнаруженного динамического параметра и необнаруженного динамического параметра, корреляция которого только что выполнена.

     ![Обнаруженные и скоррелированные динамические параметры](../test/media/web_test_dynamicparameter_conclusion.png "Web_Test_DynamicParameter_Conclusion")

11. Запустите тест. Теперь он выполняется без ошибок.

## <a name="qa"></a>Вопросы и ответы

### <a name="q-can-i-re-run-dynamic-parameter-detection-if-my-web-app-gets-modified"></a>Вопрос. Можно ли повторно обнаружить динамический параметр, если веб-приложение изменится?

 **Ответ.** Да, используйте следующую процедуру:

1.  На панели инструментов нажмите кнопку "Преобразовать динамические параметры в параметры веб-теста".

     Если были обнаружены динамические параметры, после завершения процесса обнаружения откроется диалоговое окно "Преобразование динамических параметров в параметры веб-теста".

     Динамические параметры перечислены в столбце Динамические параметры. Запросы, из которых будут извлечены динамические параметры, и запросы, к которым они будут привязаны, указаны в столбцах Параметр извлечения из ответа и Привязка к запросу.

     Если выбрать динамический параметр в диалоговом окне "Преобразование динамических параметров в параметры веб-теста", в дереве запросов редактора веб-тестов производительности выделяются два запроса. Первый запрос — это запрос, в который будет добавлено правило извлечения. Второй запрос — это запрос, с которым будет связано извлеченное значение.

2.  Установите или снимите флажок рядом с динамическим параметром, для которого требуется выполнить автоматическую корреляцию. По умолчанию установлены флажки для всех динамических параметров.

### <a name="q-do-i-need-to-configure-visual-studio-to-detect-dynamic-parameters"></a>Вопрос. Необходимо ли настраивать Visual Studio для обнаружения динамических параметров?

 **Ответ.** Конфигурация Visual Studio по умолчанию предполагает обнаружение динамических параметров при записи веб-теста производительности. Однако если в параметрах Visual Studio отключено обнаружение динамических параметров или если тестируемое веб-приложение было изменено с добавлением дополнительных динамических параметров, можно [запустить обнаружение динамических параметров из редактора веб-тестов производительности](#FindingNonDetectableDynamicParamters_QA_ReRunDetection).