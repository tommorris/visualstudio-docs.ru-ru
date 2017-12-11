---
title: "Установка средств сборки в контейнер | Документы Майкрософт"
ms.custom: 
ms.date: 10/18/2017
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d5c038e2-e70d-411e-950c-8a54917b578a
author: heaths
ms.author: heaths
manager: ghogen
ms.openlocfilehash: 3a48ba73e51af789e4017a104d7ea2f70338f3e9
ms.sourcegitcommit: 26419ab0cccdc30d279c32d6a841758cfa903806
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/11/2017
---
# <a name="install-build-tools-into-a-container"></a>Установка средств сборки в контейнер

Средства Visual Studio Build Tools можно установить в контейнере Windows для поддержки процессов непрерывной интеграции и поставки. В этой статье описываются необходимые изменения конфигурации Docker, а также [рабочие нагрузки и компоненты](workload-component-id-vs-build-tools.md), которые можно установить в контейнере.

[Контейнеры](https://www.docker.com/what-container) — это отличное средство для упаковки согласованной системы сборки, которую можно использовать не только в серверной среде непрерывной интеграции и поставки, но и в средах разработки. Например, вы можете поместить исходный код в контейнер, сборка которого будет выполняться в настраиваемой среде, и в то же время продолжать использовать Visual Studio или другие средства для написания кода. Если в рамках рабочего процесса непрерывной интеграции и поставки используется тот же образ контейнера, можно быть уверенным в том, что сборка кода будет производиться согласованно. Контейнеры можно также применять для обеспечения согласованности среды выполнения. Это обычный сценарий для микрослужб, использующих несколько контейнеров с системой оркестрации, но он выходит за рамки этой статьи.

Если возможностей средств Visual Studio Build Tools недостаточно для сборки исходного кода, эти же инструкции можно использовать для других продуктов Visual Studio. Однако имейте в виду, что контейнеры Windows не поддерживают интерактивный пользовательский интерфейс, поэтому все команды должны быть автоматизированы.

## <a name="overview"></a>Обзор

С помощью [Docker](https://www.docker.com/what-docker) вы создаете образ, на основе которого можно создавать контейнеры для сборки исходного кода. Пример файла Dockerfile устанавливает последнюю версию средств Visual Studio Build Tools 2017 и ряд других полезных программ, часто применяемых для сборки исходного кода. Собственный файл Dockerfile можно изменить, включив в него другие средства и скрипты для проведения тестов, публикации выходных данных сборки и других задач.

Если вы уже установили Docker для Windows, вы можете перейти к шагу 3.

## <a name="step-1-enable-hyper-v"></a>Шаг 1. Включение Hyper-V

По умолчанию технология Hyper-V отключена. Ее необходимо включить для запуска Docker для Windows, так как в настоящее время в Windows 10 поддерживается только изоляция Hyper-V.

* [Включение Hyper-V в Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)
* [Включение Hyper-V в Windows Server 2016](https://docs.microsoft.com/windows-server/virtualization/hyper-v/get-started/install-the-hyper-v-role-on-windows-server)

> [!NOTE]
> На компьютере должна быть включена виртуализация. Как правило, она включена по умолчанию, однако если установить Hyper-V не удалось, обратитесь к документации по вашей системе за инструкциями по включению виртуализации.

## <a name="step-2-install-docker-for-windows"></a>Шаг 2. Установка Docker для Windows

Если вы используете Windows 10, то можете скачать и установить [Docker Community Edition для Windows](https://www.docker.com/docker-windows). Вы можете [установить Docker Enterprise Edition для Windows Server 2016](https://docs.docker.com/engine/installation/windows/docker-ee) с помощью PowerShell, используя Desired State Configuration (DSC), или выполнить простую одиночную установку с помощью [поставщика пакетов](https://docs.microsoft.com/virtualization/windowscontainers/deploy-containers/deploy-containers-on-server).

## <a name="step-3-switch-to-windows-containers"></a>Шаг 3. Переключение на контейнеры Windows

Средства Build Tools 2017 можно установить только в Windows, для чего нужно [переключиться на контейнеры Windows](https://docs.docker.com/docker-for-windows/#getting-started-with-windows-containers). Контейнеры Windows в Windows 10 поддерживают только [изоляцию Hyper-V](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/hyperv-container), в то время как в Windows Server 2016 они поддерживают как изоляцию Hyper-V, так и изоляцию процессов.

## <a name="step-4-expand-maximum-container-disk-size"></a>Шаг 4. Увеличение максимального размера диска для контейнеров

Средства Visual Studio Build Tools, и тем более среда Visual Studio, требуют много места на диске для установки всех компонентов. Хотя используемый в качестве примера файл Dockerfile отключает кэш пакетов, размер диска для образов контейнеров следует увеличить до необходимого. В настоящее время увеличить размер диска в Windows можно только путем изменения конфигурации Docker.

**Windows 10**

1. В области уведомлений [щелкните значок Docker для Windows правой кнопкой мыши](https://docs.docker.com/docker-for-windows/#docker-settings) и выберите пункт **Параметры...**.
2. [Выберите раздел "Управляющая программа"](https://docs.docker.com/docker-for-windows/#docker-daemon).
3. [Нажмите кнопку **Основные**](https://docs.docker.com/docker-for-windows/#edit-the-daemon-configuration-file), чтобы переключиться в режим **Дополнительно**.
4. Добавьте приведенное ниже свойство массива JSON, чтобы увеличить дисковое пространство до 120 ГБ (этого более чем достаточно для средств Build Tools с учетом накопления данных в будущем).

   ```json
   {
     "storage-opts": [
       "size=120GB"
     ]
   }
   ```

   Это свойство добавляется к уже имеющимся. Например, после внесения этих изменений файл конфигурации управляющей программы по умолчанию должен выглядеть так:

   ```json
   {
     "registry-mirrors": [],
     "insecure-registries": [],
     "debug": true,
     "experimental": true,
     "storage-opts": [
       "size=120GB"
     ]
   }
   ```

5. Нажмите кнопку **Применить**.

**Windows Server 2016**

1. Остановите службу docker.

   ```shell
   sc.exe stop docker
   ```

2. В командной строке с повышенными привилегиями отредактируйте файл "%ProgramData%\Docker\config\daemon.json" (или иной файл, указанный в `dockerd --config-file`).
3. Добавьте приведенное ниже свойство массива JSON, чтобы увеличить дисковое пространство до 120 ГБ (этого более чем достаточно для средств Build Tools с учетом накопления данных в будущем).

   ```json
   {
     "storage-opts": [
       "size=120GB"
     ]
   }
   ```

   Это свойство добавляется к уже имеющимся.
4. Сохраните и закройте файл.
5. Запустите службу docker.

   ```shell
   sc.exe start docker
   ```

## <a name="step-5-create-and-build-the-dockerfile"></a>Шаг 5. Создание и сборка Dockerfile

Приведенный ниже пример Dockerfile необходимо сохранить в новый файл на диске. Если файл имеет имя Dockerfile, он распознается по умолчанию.

> [!NOTE]
> В этом образце файла Dockerfile исключены только старые пакеты Windows SDK, которые нельзя устанавливать в контейнерах. Старые выпуски приводят к сбою команды сборки.

1. Откройте окно командной строки.
2. Создайте каталог (рекомендуется):

   ```shell
   mkdir C:\BuildTools
   ```

3. Перейдите в этот каталог:

   ```shell
   cd C:\BuildTools
   ```

3. Сохраните в каталоге C:\BuildTools\Dockerfile представленное ниже содержимое.

   ```dockerfile
   # Use the latest Windows Server Core image.
   FROM microsoft/windowsservercore

   # Download useful tools to C:\Bin.
   ADD https://dist.nuget.org/win-x86-commandline/v4.1.0/nuget.exe C:\\Bin\\nuget.exe

   # Download the Build Tools bootstrapper outside of the PATH.
   ADD https://aka.ms/vs/15/release/vs_buildtools.exe C:\\TEMP\\vs_buildtools.exe

   # Add C:\Bin to PATH and install Build Tools excluding workloads and components with known issues.
   RUN setx /m PATH "%PATH%;C:\Bin" \
    && C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --installPath C:\BuildTools --all \
       --remove Microsoft.VisualStudio.Component.Windows10SDK.10240 \
       --remove Microsoft.VisualStudio.Component.Windows10SDK.10586 \
       --remove Microsoft.VisualStudio.Component.Windows10SDK.14393 \
       --remove Microsoft.VisualStudio.Component.Windows81SDK \
    || IF "%ERRORLEVEL%"=="3010" EXIT 0

   # Start developer command prompt with any other commands specified.
   ENTRYPOINT C:\BuildTools\Common7\Tools\VsDevCmd.bat &&

   # Default to PowerShell if no other command specified.
   CMD ["powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]
   ```

4. Выполните в этом каталоге приведенную ниже команду.

   ```shell
   docker build -t buildtools2017:latest -m 2GB .
   ```

   Эта команда выполняет сборку файла Dockerfile в текущем каталоге, используя 2 ГБ памяти. Размер памяти по умолчанию, равный 1 ГБ, недостаточен, если установлены некоторые рабочие нагрузки. Однако в зависимости от требований вам, возможно, удастся выполнить сборку, используя всего 1 ГБ памяти.

   Итоговый образ помечается как "buildtools2017:latest", так что вы можете легко запустить его в контейнере как "buildtools2017", так как "latest" — это тег по умолчанию, используемый, если тег не указан. Если вы хотите использовать определенную версию средств Visual Studio Build Tools 2017 в более [сложном сценарии](advanced-build-tools-container.md), вы можете пометить контейнер конкретным номером сборки Visual Studio, а также тегом "latest", чтобы контейнеры применяли одну и ту же версию.

## <a name="step-6-using-the-built-image"></a>Шаг 6. Использование собранного образа

После создания образа его можно запустить в контейнере для выполнения как интерактивной, так и автоматической сборки. В этом примере используется Командная строка разработчика, поэтому PATH и другие переменные среды уже настроены.

1. Откройте окно командной строки.
2. Запустите контейнер, чтобы запустить среду PowerShell, в которой заданы все переменные среды разработчика:

   ```shell
   docker run -it buildtools2017
   ```

Чтобы использовать этот образ для процесса непрерывной интеграции и поставки, его можно опубликовать в собственном [реестре контейнеров Azure](https://azure.microsoft.com/services/container-registry) или другом внутреннем [реестре Docker](https://docs.docker.com/registry/deploying), откуда его могут извлекать серверы.

## <a name="get-support"></a>Техническая поддержка
Иногда возникают проблемы. При сбое установки Visual Studio ознакомьтесь с советами, приведенными на странице [Устранение неполадок и исправление ошибок установки и обновления Visual Studio 2017](troubleshooting-installation-issues.md). Кроме того, вы можете сообщить о проблемах при использовании продукта в корпорацию Майкрософт, используя средство [Сообщить о проблеме](../ide/how-to-report-a-problem-with-visual-studio-2017.md) в Visual Studio IDE или платформу [UserVoice](https://visualstudio.uservoice.com/forums/121579). Вы можете просматривать описания проблем в [сообществе разработчиков Visual Studio](https://developercommunity.visualstudio.com/). Там же можно получать ответы на интересующие вас вопросы. Вы также можете связаться с нами и другими разработчиками Visual Studio, используя [средство для обсуждения Visual Studio в сообществе Gitter](https://gitter.im/Microsoft/VisualStudio) (требуется учетная запись [GitHub](https://github.com/)).

## <a name="see-also"></a>См. также

* [Расширенный пример для контейнеров](advanced-build-tools-container.md)
* [Известные проблемы для контейнеров](build-tools-container-issues.md)