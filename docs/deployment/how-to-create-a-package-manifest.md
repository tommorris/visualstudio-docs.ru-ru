---
title: 'Практическое: создание манифеста пакета | Документация Майкрософт'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- package files [Windows Installer]
- package files [ClickOnce]
- prerequisites, custom bootstrapper package
- dependencies, custom bootstrapper packages
ms.assetid: 5aecc507-2764-42f2-ae6f-c227971cf0af
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 38a0c448bcf629c4e914393cb8eabad93ced574c
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/19/2018
ms.locfileid: "39154633"
---
# <a name="how-to-create-a-package-manifest"></a>Практическое: создание манифеста пакета
Чтобы развернуть необходимые условия для приложения, можно использовать пакет начального загрузчика. Пакет начального загрузчика содержит один файл манифеста продукта манифест пакета для каждого языкового стандарта. Общие функции для различных локализованных версий следует перейти в манифест продукта.  
  
 Дополнительные сведения о манифестах пакетов см. в разделе [как: создание манифеста продукта](../deployment/how-to-create-a-product-manifest.md).  
  
## <a name="create-the-package-manifest"></a>Создание манифеста пакета  
  
#### <a name="to-create-the-package-manifest"></a>Создание манифеста пакета  
  
1.  Создайте каталог для пакета начального загрузчика. В этом примере используется *C:\package*.  
  
2.  Создайте подкаталог с именем языкового стандарта, такие как *en* для английского языка.  
  
3.  В Visual Studio создайте XML-файл с именем *package.xml*и сохраните его для *C:\package\en* папки.  
  
4.  Добавьте XML-код, чтобы получить список имя пакета начального загрузчика, язык и региональные параметры для этого локализованного манифеста пакета и необязательный лицензионного соглашения. Следующий код XML использует переменные `DisplayName` и `Culture`, которые определены в элементе более поздней версии.  
  
    ```xml  
    <Package  
        xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"  
        Name="DisplayName"  
        Culture="Culture"  
        LicenseAgreement="eula.txt">  
    ```  
  
5.  Добавьте XML-код, чтобы получить список всех файлов, которые находятся в каталоге, зависящих от языкового стандарта. Следующий код XML использует файл с именем *eula.txt* которая подходит для **en** языкового стандарта.  
  
    ```xml  
    <PackageFiles>  
      <PackageFile Name="eula.txt"/>  
    </PackageFiles>  
    ```  
  
6.  Добавьте XML-код, чтобы определить локализуемые строки для пакета начального загрузчика. Следующий XML-код добавляет строки сообщений об ошибках для **en** языкового стандарта.  
  
    ```xml  
      <Strings>  
        <String Name="DisplayName">Custom Bootstrapper Package</String>  
        <String Name="CultureName">en</String>  
        <String Name="NotAnAdmin">You must be an administrator to install   
    this package.</String>  
        <String Name="GeneralFailure">A general error has occurred while   
    installing this package.</String>  
    </Strings>  
    ```  
  
7.  Копировать *C:\package* папки в каталог начального загрузчика Visual Studio. Для Visual Studio 2010, это *\Program Files\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages* каталога.  
  
## <a name="example"></a>Пример  
 Манифест пакета содержит зависящие от языкового стандарта, например сообщения об ошибках, условия лицензии и языковые пакеты.  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<Package  
  xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"  
  Name="DisplayName"  
  Culture="Culture"  
  LicenseAgreement="eula.txt">  
  
  <PackageFiles>  
    <PackageFile Name="eula.txt"/>  
  </PackageFiles>  
  
  <Strings>  
    <String Name="DisplayName">Custom Bootstrapper Package</String>  
    <String Name="Culture">en</String>  
    <String Name="NotAnAdmin">You must be an administrator to install this package.</String>  
    <String Name="GeneralFailure">A general error has occurred while   
installing this package.</String>  
  </Strings>  
</Package>  
```  
  
## <a name="see-also"></a>См. также  
 [Справочник по схеме продукта и пакета](../deployment/product-and-package-schema-reference.md)