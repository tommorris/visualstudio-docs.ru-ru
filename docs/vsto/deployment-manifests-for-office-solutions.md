---
title: Манифесты развертывания для решений Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], deployment manifests
- deployment manifests [Office development in Visual Studio]
- manifests [Office development in Visual Studio], deployment
- Office development in Visual Studio, deployment manifests
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 41f0e6b484ae61d53913c51e3d51b123a5d054a2
ms.sourcegitcommit: 209c2c068ff0975994ed892b62aa9b834a7f6077
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34263494"
---
# <a name="deployment-manifests-for-office-solutions"></a>Манифесты развертывания для решений Office
  Манифест развертывания представляет XML-файл, который описывает параметры развертывания решения Office и определяет текущую версию приложения.  
  
 Разработка решений Office в Visual Studio использует [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] схемы манифеста развертывания, определенные в [манифест развертывания ClickOnce](/visualstudio/deployment/clickonce-deployment-manifest) ссылки.  
  
## <a name="remarks"></a>Примечания  
 Файл манифеста развертывания для решений Office определяет текущую версию и другие настройки развертывания. Он ссылается на манифест приложения и описывает текущую версию решения и всех файлах в пределах решения.  
  
## <a name="file-name-syntax"></a>Синтаксис имени файла  
 Имя файла манифеста развертывания должно оканчиваться *.vsto* расширения. Несмотря на то, что это стандартный [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] манифест развертывания, расширение, которое позволяет средства Visual Studio для Office runtime для обработки файла.  
  
## <a name="example"></a>Пример  
 В следующем примере кода показан манифест развертывания для Visual Studio Tools для решения Office.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<asmv1:assembly   
  xsi:schemaLocation=  
    "urn:schemas-microsoft-com:asm.v1 assembly.adaptive.xsd"   
  manifestVersion="1.0"   
  xmlns:asmv3="urn:schemas-microsoft-com:asm.v3"   
  xmlns:dsig="http://www.w3.org/2000/09/xmldsig#"   
  xmlns:co.v1="urn:schemas-microsoft-com:clickonce.v1"   
  xmlns:co.v2="urn:schemas-microsoft-com:clickonce.v2"   
  xmlns="urn:schemas-microsoft-com:asm.v2"   
  xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"   
  xmlns:asmv2="urn:schemas-microsoft-com:asm.v2"   
  xmlns:xrml="urn:mpeg:mpeg21:2003:01-REL-R-NS"   
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <assemblyIdentity   
    name="ContosoOfficeSolutions.vsto"   
    version="1.0.0.0"   
    publicKeyToken="25d0f3ca94156f1f"   
    language="neutral"   
    processorArchitecture="msil"   
    xmlns="urn:schemas-microsoft-com:asm.v1" />  
  <description   
    asmv2:publisher="Microsoft"   
    asmv2:product="ContosoOfficeSolutions"   
    xmlns="urn:schemas-microsoft-com:asm.v1" />  
  <deployment install="false" mapFileExtensions="true" />  
  <dependency>  
    <dependentAssembly   
      dependencyType="install"   
      codebase="ContosoOfficeSolutions.dll.manifest"   
      size="13545">  
      <assemblyIdentity   
        name="ContosoOfficeSolutions.dll"   
        version="1.0.0.0"   
        publicKeyToken="25d0f3ca94156f1f"   
        language="neutral"   
        processorArchitecture="msil"   
        type="win32" />  
      <hash>  
        <dsig:Transforms>  
          <dsig:Transform Algorithm=  
            "urn:schemas-microsoft-com:HashTransforms.Identity" />  
        </dsig:Transforms>  
        <dsig:DigestMethod Algorithm=  
          "http://www.w3.org/2000/09/xmldsig#sha1" />  
        <dsig:DigestValue>PoY</dsig:DigestValue>  
      </hash>  
    </dependentAssembly>  
  </dependency>  
  <publisherIdentity name="name" issuerKeyHash="003" />  
<Signature   
  Id="StrongNameSignature"   
  xmlns="http://www.w3.org/2000/09/xmldsig#">    
  <SignedInfo>  
    <CanonicalizationMethod Algorithm=  
      "http://www.w3.org/2001/10/xml-exc-c14n#" />  
  <SignatureMethod Algorithm=  
    "http://www.w3.org/2000/09/xmldsig#rsa-sha1" />  
    <Reference URI="">  
      <Transforms>  
        <Transform Algorithm=  
          "http://www.w3.org/2000/09/xmldsig#enveloped-signature" />  
        <Transform Algorithm=  
          "http://www.w3.org/2001/10/xml-exc-c14n#" />  
      </Transforms>  
      <DigestMethod Algorithm=  
        "http://www.w3.org/2000/09/xmldsig#sha1" />  
      <DigestValue>5oz</DigestValue>  
    </Reference>  
  </SignedInfo>  
  <SignatureValue>nNG</SignatureValue>  
  <KeyInfo Id="StrongNameKeyInfo">  
    <KeyValue>  
      <RSAKeyValue>  
        <Modulus>ufI</Modulus>  
        <Exponent>AQAB</Exponent>  
      </RSAKeyValue>  
    </KeyValue>  
    <msrel:RelData   
      xmlns:msrel=  
        "http://schemas.microsoft.com/windows/rel/2005/reldata">  
      <r:license   
        xmlns:r="urn:mpeg:mpeg21:2003:01-REL-R-NS"   
        xmlns:as=  
          "http://schemas.microsoft.com/windows/pki/2005/Authenticode">  
        <r:grant>  
          <as:ManifestInformation   
            Hash="099"   
            Description=""   
            Url="">  
            <as:assemblyIdentity   
              name="ContosoOfficeSolutions.vsto"   
              version="1.0.0.0"   
              publicKeyToken="25d0f3ca94156f1f"   
              language="neutral"   
              processorArchitecture="msil"   
              xmlns="urn:schemas-microsoft-com:asm.v1" />  
          </as:ManifestInformation>  
          <as:SignedBy />  
          <as:AuthenticodePublisher>  
            <as:X509SubjectName>CN=DDNET\BAAdmin</as:X509SubjectName>  
          </as:AuthenticodePublisher>  
        </r:grant>  
        <r:issuer>  
          <Signature   
            Id="AuthenticodeSignature"   
            xmlns="http://www.w3.org/2000/09/xmldsig#">  
            <SignedInfo>  
              <CanonicalizationMethod   
                Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />  
              <SignatureMethod   
                Algorithm=  
                  "http://www.w3.org/2000/09/xmldsig#rsa-sha1" />  
              <Reference URI="">  
                <Transforms>  
                  <Transform Algorithm=  
                    "http://www.w3.org/2000/09/xmldsig#enveloped-signature" />  
                  <Transform Algorithm=  
                    "http://www.w3.org/2001/10/xml-exc-c14n#" />  
                </Transforms>  
                <DigestMethod   
                  Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />  
                <DigestValue>iAd</DigestValue>  
              </Reference>  
            </SignedInfo>  
            <SignatureValue>HL9</SignatureValue>  
            <KeyInfo>  
              <KeyValue>  
                <RSAKeyValue>  
                  <Modulus>ufI</Modulus>  
                  <Exponent>AQAB</Exponent>  
                </RSAKeyValue>  
              </KeyValue>  
              <X509Data>  
                <X509Certificate>MII</X509Certificate>  
              </X509Data>  
            </KeyInfo>  
          </Signature>  
        </r:issuer>  
      </r:license>  
    </msrel:RelData>  
  </KeyInfo>  
</Signature>  
</asmv1:assembly>  
```  
  
## <a name="see-also"></a>См. также  
 [Манифесты приложений для решений Office](../vsto/application-manifests-for-office-solutions.md)  
  
  