---
title: Развертывание ASP.NET в IIS с помощью веб-развертывания
ms.custom: ''
ms.date: 06/04/2018
ms.technology: vs-ide-deployment
ms.topic: tutorial
ms.assetid: 9cb339b5-3caf-4755-aad1-4a5da54b2a23
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- aspnet
ms.openlocfilehash: 4705ca6e72001f8930e2fa4270515df53e1213a8
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39080854"
---
# <a name="deploy-aspnet-to-a-remote-iis-computer-using-web-deploy-in-visual-studio"></a>Развертывание ASP.NET в удаленном компьютере IIS, с помощью веб-развертывания в Visual Studio

В этой статье объясняется, как установить и настроить приложение Visual Studio 2017 ASP.NET MVC 4.5.2 и развертывания в IIS. В этой статье представлены инструкции по настройке базовую конфигурацию IIS на сервере Windows и развертывание приложения из Visual Studio. Чтобы убедиться в том, что сервер необходимые компоненты, которые установлены и готовы к развертыванию включены следующие действия. Если вы развертываете приложение ASP.NET Core, некоторые шаги будут отличаться. Чтобы развернуть приложение ASP.NET Core, см. в разделе [публикации приложения в службах IIS путем импорта параметров публикации](../deployment/tutorial-import-publish-settings-iis.md) инструкции. В некоторых сценариях ASP.NET и ASP.NET Core, легче и быстрее для развертывания в IIS путем импорта параметров публикации.

Эти процедуры протестированы на эти конфигурации сервера:
* Windows Server 2012 R2 и служб IIS 8 (для Windows Server 2008 R2, server, шаги будут отличаться)

## <a name="create-the-aspnet-452-application-on-the-visual-studio-computer"></a>Создавать приложения ASP.NET 4.5.2 приложения на компьютере с Visual Studio
  
1. На компьютере с Visual Studio, выберите **файл** > **новый проект**.

1. В разделе **Visual C#** или **Visual Basic**, выберите **Web**, а затем в средней области выберите либо **веб-приложение ASP.NET (.NET Framework)** и нажмите кнопку **ОК**.

    Если вы не видите шаблоны указанный проект, нажмите кнопку **открыть установщик Visual Studio** ссылку в левой части **новый проект** диалоговое окно. Запускается Visual Studio Installer. Предварительные требования в этой статье, чтобы определить необходимые рабочие нагрузки Visual Studio, которые необходимо установить.

1. Выберите **MVC** (.NET Framework) и убедитесь, что **без проверки подлинности** выбран, а затем нажмите кнопку **ОК**.

1. Введите имя, например **MyWebApp** и нажмите кнопку **ОК**.

    Visual Studio создаст проект.

1. Выберите **построения** > **построить решение** для сборки проекта.

## <a name="install-and-configure-iis-on-windows-server"></a>Установка и настройка служб IIS на Windows Server

[!INCLUDE [remote-debugger-install-iis-role](../debugger/includes/remote-debugger-install-iis-role.md)]

## <a name="update-browser-security-settings-on-windows-server"></a>Обновить параметры безопасности браузера на сервере Windows

Если конфигурация усиленной безопасности включен в Internet Explorer (он включен по умолчанию), может потребоваться добавить некоторые домены в список надежных сайтов, чтобы можно было загрузить некоторые компоненты веб-сервера. Добавить надежных сайтов, выбрав **обозревателя** > **безопасности** > **надежных сайтов** > **сайтов** . Добавьте следующие домены.

- Microsoft.com
- go.microsoft.com
- download.microsoft.com
- IIS.NET

При загрузке программного обеспечения, можно получить запросы, чтобы предоставить разрешение для загрузки различные сценарии веб-сайт и ресурсы. Некоторые из этих ресурсов не являются обязательными, но чтобы упростить процесс, нажмите кнопку **добавить** при появлении запроса.

## <a name="install-aspnet-45-on-windows-server"></a>Установка ASP.NET 4.5 на Windows Server

Если нужны более подробные сведения для установки ASP.NET на IIS, см. в разделе [IIS 8.0, с помощью ASP.NET 3.5 и ASP.NET 4.5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45).

1. В левой области диспетчера серверов выберите **IIS**. Щелкните правой кнопкой мыши сервер и выберите **Internet Information Services (IIS) Manager**.

1. Используйте установщик веб-платформы (WebPI) для установки ASP.NET 4.5 (узел сервера в Windows Server 2012 R2, выберите **получить новый веб-платформы компоненты** и выполните поиск по ASP.NET)

    ![RemoteDBG_IIS_AspNet_45](../debugger/media/remotedbg_iis_aspnet_45.png "RemoteDBG_IIS_AspNet_45")

    > [!NOTE]
    > Если вы используете Windows Server 2008 R2, установите ASP.NET 4, вместо этого с помощью следующей команды:

     **C:\Windows\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -ir**

2. Перезагрузите систему (или выполните **net stop was /y** следуют **net start w3svc** из командной строки, чтобы получить изменения в системную переменную PATH).

## <a name="install-web-deploy-36-on-windows-server"></a>Установка веб-развертывания 3.6 на Windows Server

[!INCLUDE [remote-debugger-install-web-deploy](../debugger/includes/remote-debugger-install-web-deploy.md)]

## <a name="configure-aspnet-web-site-on-the-windows-server-computer"></a>Настройка веб-сайта ASP.NET на компьютере с Windows Server

1. Откройте проводник Windows и создайте новую папку, **C:\Publish**, где позже будет развернут проект ASP.NET.

2. Если он не открыт, откройте **Internet Information Services (IIS) Manager**. (В левой области диспетчера серверов выберите **IIS**. Щелкните правой кнопкой мыши сервер и выберите **Internet Information Services (IIS) Manager**.)

3. В разделе **подключений** в левой области перейдите в раздел **сайты**.

4. Выберите **Default Web Site**, выберите **основные параметры**и задайте **физический путь** для **C:\Publish**.

5. Щелкните правой кнопкой мыши узел **Веб-сайт по умолчанию** и выберите команду **Добавить приложение**.

6. Задайте **псевдоним** поле **MyASPApp**, примите имя по умолчанию пула приложений (**DefaultAppPool**) и задайте **физический путь** для  **C:\Publish**.

7. В разделе **подключений**выберите **пулы приложений**. Откройте **DefaultAppPool** и присвоено поле пул приложения **ASP.NET v4.0** (ASP.NET 4.5 не допускаются для пула приложений).

8. Выбрав сайт в диспетчере служб IIS, выберите **изменение разрешений**и убедитесь, что IUSR IIS_IUSRS и пользователь настроен для пула приложений — авторизованного пользователя с правами на чтение и выполнение. Если ни один из этих пользователей, добавьте IUSR в качестве пользователя с правами на чтение и выполнение.

## <a name="publish-and-deploy-the-app-using-web-deploy-from-visual-studio"></a>Публикация и развертывание приложения с помощью веб-развертывания из Visual Studio

[!INCLUDE [deploy-app-web-deploy](../deployment/includes/deploy-app-web-deploy.md)]

Кроме того необходимо прочитать следующий раздел об устранении порты.

## <a name="troubleshoot-open-required-ports-on-windows-server"></a>Устранение неполадок: Откройте необходимые порты на Windows Server

В большинстве установок необходимые порты открыты путем установки ASP.NET и веб-развертывания. Тем не менее может потребоваться проверить, что порты открыты.

> [!NOTE]
> На виртуальной Машине Azure, необходимо открыть порты, через [группы безопасности сети](/azure/virtual-machines/virtual-machines-windows-hero-role#open-port-80). 

Требуемые порты:

* 80 - необходимые для службы IIS
* 8172 - required для веб-развертывания для развертывания приложения из Visual Studio

1. Чтобы открыть порт на сервере Windows, откройте **запустить** меню, и выполните поиск **брандмауэр Windows в режиме повышенной безопасности**.

2. Затем выберите **правила для входящих подключений** > **новое правило** > **порт**. Выберите **Далее** и в разделе **определенные локальные порты**, введите номер порта, нажмите кнопку **Далее**, затем **разрешить подключение**, «далее», и Добавьте имя (**IIS**, **веб-развертывания**, или **msvsmon**) для правила входящего подключения.

    Дополнительные сведения о настройке брандмауэра Windows, см. в разделе [Настройка брандмауэра Windows для удаленной отладки](../debugger/configure-the-windows-firewall-for-remote-debugging.md).

3. Создайте дополнительные правила для требуемых портов.

## <a name="next-steps"></a>Следующие шаги

В этом руководстве создан файл параметров публикации, импортировать его в Visual Studio и развертывания приложения ASP.NET в IIS. Вы также можете развернуть путем импорта параметров публикации.

> [!div class="nextstepaction"]
> [Развертывание в IIS путем импорта параметров публикации](../deployment/tutorial-import-publish-settings-iis.md)
