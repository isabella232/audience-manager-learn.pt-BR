---
title: Validação da ID do dispositivo global
description: Os identificadores de publicidade de dispositivo (iDFA, GAID, Roku ID) têm padrões de formatação que devem ser cumpridos para que possam ser usados no ecossistema de publicidade digital. Atualmente, os clientes e parceiros podem fazer upload de IDs para nossas fontes de dados globais em qualquer formato sem serem notificados sobre se a ID está formatada corretamente. Este recurso introduzirá a validação das IDs de dispositivo enviadas para as fontes de dados globais para formatação correta e fornecerá mensagens de erro quando as IDs estiverem formatadas incorretamente. No lançamento, ofereceremos suporte à validação para iDFA, Google Advertising e Roku ID.
feature: data governance & privacy
topics: mobile
audience: implementer, developer, architect
activity: implement
doc-type: article
team: Technical Marketing
kt: 2977
translation-type: tm+mt
source-git-commit: a108c51fdad66f4e7974eb96609b6d8f058cb6ff
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 1%

---


# Validação da ID do dispositivo global {#global-device-id-validation}

Os identificadores de publicidade de dispositivo (iDFA, GAID, Roku ID) têm padrões de formatação que devem ser cumpridos para que possam ser usados no ecossistema de publicidade digital. Atualmente, os clientes e parceiros podem fazer upload de IDs para o Global [!UICONTROL data sources] em qualquer formato sem serem notificados se a ID está formatada corretamente. Esse recurso introduzirá a validação das IDs de dispositivo enviadas ao Global [!UICONTROL data sources] para formatação correta e fornecerá mensagens de erro quando as IDs estiverem formatadas incorretamente. Apoiaremos a validação para [!DNL iDFA], [!DNL Google Advertising] e no [!DNL Roku IDs] lançamento.

## Visão geral dos padrões de formato {#overview-of-format-standards}

A seguir estão os pools globais de IDs de publicidade de dispositivos que são reconhecidos e suportados pela AAM. Eles são implementados como compartilhados [!UICONTROL Data Sources] que podem ser usados por qualquer cliente ou parceiro de dados que funcione com dados vinculados aos usuários dessas plataformas.

<table>
  <tr>
   <td>Plataforma </td>
   <td>ID da fonte de dados AAM </td>
   <td>Formato de ID </td>
   <td>PID AAM </td>
   <td>Notas </td>
  </tr>
  <tr>
   <td>Google Android (GAID)</td>
   <td>20914</td>
   <td>32 números hexadecimais, geralmente apresentados como 8-4-4-12<em>exemplo, 97987bca-ae59-4c7d-94ba-ee4f19ab8c21<br/> </em> </td>
   <td>1352</td>
   <td>Essa ID deve ser coletada em uma Referência de formulário bruto/sem hash/inalterada - <a href="https://play.google.com/about/monetization-ads/ads/ad-id/">https://play.google.com/about/monetization-ads/ads/ad-id/</a></td>
  </tr>
  <tr>
   <td>Apple iOS (IDFA)</td>
   <td>20915</td>
   <td>32 números hexadecimais, geralmente apresentados como <em>exemplo 8-4-4-4-12, 6D92078A-8246-4BA4-AE5B-76104861E7DC<br /> </em> </td>
   <td>3560</td>
   <td>Essa ID deve ser coletada em uma Referência de formulário bruto/sem hash/inalterada - <a href="https://support.apple.com/en-us/HT205223">https://support.apple.com/en-us/HT205223</a></td>
  </tr>
  <tr>
   <td>Roku (RIDA)</td>
   <td>121963</td>
   <td>32 números hexadecimais, geralmente apresentados como <em>exemplo 8-4-4-4-12,</em> <em>fcb2a29c-315a-5e6b-bcfd-d889ba19aada</em></td>
   <td>11536</td>
   <td>Essa ID deve ser coletada em uma Referência de formulário bruto/sem hash/inalterada - <a href="https://sdkdocs.roku.com/display/sdkdoc/Roku+Advertising+Framework">https://sdkdocs.roku.com/display/sdkdoc/Roku+Advertising+Framework</a> </td>
  </tr>
  <tr>
   <td>ID de anúncio da Microsoft (MAID)</td>
   <td>389146</td>
   <td>Sequência numérica alfa</td>
   <td>14593</td>
   <td>Essa ID deve ser coletada em uma Referência de formulário bruto/sem hash/inalterada - <a href="https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid">https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.</a><br/><a href="https://msdn.microsoft.com/en-us/library/windows/apps/windows.system.userprofile.advertisingmanager.advertisingid.aspx">advertisingidhttps://msdn.microsoft.com/en-us/library/windows/apps/windows.system.userprofile.advertisingmanager.advertisingid.aspx</a></td>
  </tr>
  <tr>
   <td>DUID da Samsung</td>
   <td>404660</td>
   <td>Exemplo de string numérica alfa, 7XCBNROQJQPYW</td>
   <td>15950</td>
   <td>Essa ID deve ser coletada em uma Referência de formulário bruto/sem hash/inalterada - <a href="https://developer.samsung.com/tv/develop/api-references/samsung-product-api-references/productinfo-api">https://developer.samsung.com/tv/develop/api-references/samsung-product-api-references/productinfo-api</a> </td>
  </tr>
</table>

## Configuração de um identificador de anúncio no aplicativo {#setting-an-advertising-identifier-in-the-app}

Definir a ID do anunciante no aplicativo é realmente um processo de duas etapas, primeiro recuperar a ID do anunciante e depois enviá-la para o Experience Cloud. Os links são encontrados abaixo para executar essas etapas.

1. Recuperar a ID
   1. [!DNL Apple] informações sobre o [!DNL advertising ID] podem ser encontradas [AQUI](https://developer.apple.com/documentation/adsupport/asidentifiermanager).
   1. Algumas informações sobre como configurar o [!DNL advertiser ID] para [!DNL Android] desenvolvedores podem ser encontradas [AQUI](http://www.androiddocs.com/google/play-services/id.html).
1. Envie-o para o Experience Cloud usando o [!DNL setAdvertisingIdentifier] método no SDK
   1. As informações para uso `setAdvertisingIdentifier` estão na [documentação](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#set-an-advertising-identifier) tanto [!DNL iOS] quanto [!DNL Android].

`// iOS (Swift) example for using setAdvertisingIdentifier:`
`ACPCore.setAdvertisingIdentifier([AdvertisingId]) // ...where [AdvertisingId] is replaced by the actual advertising ID`

## Mensagens de erro DCS para IDs incorretas  {#dcs-error-messaging-for-incorrect-ids}

Quando uma ID de dispositivo global incorreta (IDFA, GAID etc) for enviada em tempo real para o Audience Manager, um código de erro será retornado na ocorrência. Veja a seguir um exemplo de erro retornado porque a ID é enviada como um [!DNL Apple IDFA], que deve conter somente letras maiúsculas e minúsculas e, no entanto, há um &quot;x&quot; minúsculo na ID.

![imagem de erro](assets/image_4_.png)

Consulte a [documentação](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-error-codes.html?lang=en#api-and-sdk-code) para obter informações sobre a lista de códigos de erro.

## IDs de dispositivo global onboard {#onboarding-global-device-ids}

Além do envio em tempo real das IDs de dispositivos globais, você também pode &quot;[!DNL onboard]&quot; (carregar) dados em relação às IDs. Esse processo é o mesmo que quando você está integrando dados em relação às IDs do cliente (normalmente por pares de chaves/valores), mas você simplesmente usaria as IDs de fonte de dados apropriadas, para que os dados fossem atribuídos à ID do dispositivo global. A documentação sobre o processo de integração pode ser encontrada na [documentação](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/sending-audience-data/batch-data-transfer-process/batch-data-transfer-overview.html?lang=en#implementation-integration-guides). Basta lembrar de usar a [!UICONTROL data source] ID global, dependendo da plataforma que você está usando.

Se IDs de dispositivo global incorretas forem enviadas por meio do processo de integração, os erros serão exibidos no [[!DNL Onboarding Status Report]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reporting/onboarding-status-report.html?lang=en#reporting).

Veja a seguir um exemplo de um erro que apareceria no relatório:

![imagem de erro](assets/image_5_.png)