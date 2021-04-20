---
title: Validação da ID do dispositivo global
description: Os identificadores de anúncios de dispositivos (ou seja, iDFA, GAID, Roku ID) têm padrões de formatação que devem ser atendidos para serem utilizáveis no ecossistema de publicidade digital. Atualmente, os clientes e parceiros podem fazer upload de IDs em nossas fontes de dados globais em qualquer formato sem ser notificados sobre a formatação correta da ID. Esse recurso introduzirá a validação das IDs de dispositivo enviadas às fontes de dados globais para formatação adequada e fornecerá mensagens de erro quando as IDs estiverem formatadas incorretamente. Ofereceremos suporte à validação para iDFA, Google Advertising e Roku IDs na inicialização.
feature: Data Governance & Privacy
topics: mobile
activity: implement
doc-type: article
team: Technical Marketing
kt: 2977
role: Developer, Data Engineer, Architect
level: Experienced
exl-id: 0ff3f123-efb3-4124-bdf9-deac523ef8c9
translation-type: tm+mt
source-git-commit: 256edb05f68221550cae2ef7edaa70953513e1d4
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---

# Validação de ID de dispositivo global {#global-device-id-validation}

Os identificadores de anúncios de dispositivos (ou seja, iDFA, GAID, Roku ID) têm padrões de formatação que devem ser atendidos para serem utilizáveis no ecossistema de publicidade digital. Atualmente, os clientes e parceiros podem fazer upload de IDs para nosso [!UICONTROL data sources] global em qualquer formato sem serem notificados sobre a formatação correta da ID. Esse recurso introduzirá a validação das IDs de dispositivo enviadas para o [!UICONTROL data sources] Global para formatação adequada e fornecerá mensagens de erro quando as IDs estiverem formatadas incorretamente. Ofereceremos suporte à validação para [!DNL iDFA], [!DNL Google Advertising] e [!DNL Roku IDs] na inicialização.

## Visão geral dos padrões de formato {#overview-of-format-standards}

A seguir estão os pools globais de IDs de publicidade de dispositivo que são reconhecidos e suportados atualmente pela AAM. Eles são implementados como [!UICONTROL Data Sources] compartilhado que pode ser usado por qualquer cliente ou parceiro de dados que funcione com dados vinculados aos usuários dessas plataformas.

<table>
  <tr>
   <td>Plataforma </td>
   <td>ID da Fonte de Dados AAM </td>
   <td>Formato de ID </td>
   <td>PID AAM </td>
   <td>Notas </td>
  </tr>
  <tr>
   <td>Google Android (GAID)</td>
   <td>20914</td>
   <td>32 números hexadecimais, geralmente apresentados como 8-4-4-12<em>example, 97987bca-ae59-4c7d-94ba-ee4f19ab8c21<br/> </em> </td>
   <td>1352</td>
   <td>Essa ID deve ser coletada em uma Referência de formulário bruta/sem hash/inalterada - <a href="https://play.google.com/about/monetization-ads/ads/ad-id/">https://play.google.com/about/monetization-ads/ads/ad-id/</a></td>
  </tr>
  <tr>
   <td>Apple iOS (IDFA)</td>
   <td>20915</td>
   <td>32 números hexadecimais, geralmente apresentados como 8-4-4-12 <em>example, 6D92078A-8246-4BA4-AE5B-76104861E7DC<br /> </em> </td>
   <td>3560</td>
   <td>Essa ID deve ser coletada em uma Referência de formulário bruta/sem hash/inalterada - <a href="https://support.apple.com/en-us/HT205223">https://support.apple.com/en-us/HT205223</a></td>
  </tr>
  <tr>
   <td>Roku (RIDA)</td>
   <td>121963</td>
   <td>32 números hexadecimais, geralmente apresentados como 8-4-4-12 <em>example,</em> <em>fcb2a29c-315a-5e6b-bcfd-d889ba19aada</em></td>
   <td>11536</td>
   <td>Essa ID deve ser coletada em uma Referência de formulário bruta/sem hash/inalterada - <a href="https://sdkdocs.roku.com/display/sdkdoc/Roku+Advertising+Framework">https://sdkdocs.roku.com/display/sdkdoc/Roku+Advertising+Framework</a> </td>
  </tr>
  <tr>
   <td>ID de publicidade da Microsoft (MAID)</td>
   <td>389146</td>
   <td>Sequência numérica alfa</td>
   <td>14593</td>
   <td>Essa ID deve ser coletada em uma Referência de formulário bruta/sem hash/inalterada - <a href="https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid">https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid</a><br/><a href="https://msdn.microsoft.com/en-us/library/windows/apps/windows.system.userprofile.advertisingmanager.advertisingid.aspx">https://msdn.microsoft.com/en-us/library/windows/apps/windows.system.userprofile.advertisingmanager.advertisingid.aspx</a></td>
  </tr>
  <tr>
   <td>Samsung DUID</td>
   <td>404660</td>
   <td>Exemplo de string numérica alfa, 7XCBNROQJPYW</td>
   <td>15950</td>
   <td>Essa ID deve ser coletada em uma Referência de formulário bruta/sem hash/inalterada - <a href="https://developer.samsung.com/tv/develop/api-references/samsung-product-api-references/productinfo-api">https://developer.samsung.com/tv/develop/api-references/samsung-product-api-references/productinfo-api</a> </td>
  </tr>
</table>

## Definir um identificador de publicidade no aplicativo {#setting-an-advertising-identifier-in-the-app}

Definir a ID do anunciante no aplicativo é um processo de duas etapas, primeiro recuperar a ID do anunciante e depois enviá-la para o Experience Cloud. Os links são encontrados abaixo para executar essas etapas.

1. Recuperar a ID
   1. [!DNL Apple] informações sobre o  [!DNL advertising ID] podem ser encontradas  [AQUI](https://developer.apple.com/documentation/adsupport/asidentifiermanager).
   1. Algumas informações sobre como configurar o [!DNL advertiser ID] para [!DNL Android] desenvolvedores podem ser encontradas [HERE](http://www.androiddocs.com/google/play-services/id.html).
1. Envie-o para o Experience Cloud usando o método [!DNL setAdvertisingIdentifier] no SDK
   1. As informações para usar `setAdvertisingIdentifier` estão na [documentação](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#set-an-advertising-identifier) para [!DNL iOS] e [!DNL Android].

`// iOS (Swift) example for using setAdvertisingIdentifier:`
`ACPCore.setAdvertisingIdentifier([AdvertisingId]) // ...where [AdvertisingId] is replaced by the actual advertising ID`

## Mensagem de erro DCS para IDs incorretas {#dcs-error-messaging-for-incorrect-ids}

Quando uma ID de dispositivo global incorreta (IDFA, GAID etc) é enviada em tempo real para o Audience Manager, um código de erro será retornado na ocorrência. A seguir, um exemplo de um erro retornado porque a ID é enviada como um [!DNL Apple IDFA], que deve conter somente letras maiúsculas e, no entanto, há um &#39;x&#39; em letras minúsculas na ID.

![imagem de erro](assets/image_4_.png)

Consulte a [documentação](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-error-codes.html?lang=en#api-and-sdk-code) para obter a lista de códigos de erro.

## Integração das IDs de dispositivo global {#onboarding-global-device-ids}

Além do envio em tempo real de IDs de dispositivos globais, você também pode fazer o upload de dados &quot;[!DNL onboard]&quot; em relação às IDs. Esse processo é o mesmo de quando você está incorporando dados às IDs do cliente (normalmente por meio de pares de chave/valor), mas simplesmente usa as IDs de fonte de dados apropriadas, para que os dados sejam atribuídos à ID do dispositivo global. A documentação sobre o processo de integração pode ser encontrada na [documentação](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/sending-audience-data/batch-data-transfer-process/batch-data-transfer-overview.html?lang=en#implementation-integration-guides). Basta lembrar de usar a ID global [!UICONTROL data source] , dependendo da plataforma que você está usando.

Se as IDs de dispositivo global incorretas forem enviadas por meio do processo de integração, os erros serão exibidos no [[!DNL Onboarding Status Report]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reporting/onboarding-status-report.html?lang=en#reporting).

A seguir encontra-se um exemplo de erro que viria por esse relatório:

![imagem de erro](assets/image_5_.png)
