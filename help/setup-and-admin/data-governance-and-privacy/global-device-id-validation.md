---
title: Validação da ID de dispositivo global
description: Saiba mais sobre a validação de IDs de dispositivos enviadas às fontes de dados globais para formatação adequada e sobre mensagens de erro quando IDs estão formatadas incorretamente.
feature: Data Governance & Privacy
topics: mobile
activity: implement
doc-type: article
team: Technical Marketing
kt: 2977
role: Developer, Data Engineer, Architect
level: Experienced
exl-id: 0ff3f123-efb3-4124-bdf9-deac523ef8c9
source-git-commit: 2094d3bcf658913171afa848e4228653c71c41de
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 1%

---

# Validação da ID de dispositivo global {#global-device-id-validation}

Os identificadores de anúncios de dispositivos (ou seja, iDFA, GAID, Roku ID) têm padrões de formatação que devem ser atendidos para serem utilizáveis no ecossistema de publicidade digital. Atualmente, os clientes e parceiros podem fazer upload de IDs em nossas fontes de dados globais em qualquer formato sem ser notificados sobre a formatação correta da ID. Esse recurso introduzirá a validação das IDs de dispositivo enviadas às fontes de dados globais para formatação adequada e fornecerá mensagens de erro quando as IDs estiverem formatadas incorretamente. Oferecemos suporte à validação para [!DNL iDFA], [!DNL Google Advertising] e [!DNL Roku IDs] no lançamento.

## Visão geral dos padrões de formato {#overview-of-format-standards}

A seguir estão os pools globais de IDs de publicidade de dispositivo que são reconhecidos e suportados atualmente pela AAM. Eles são implementados como compartilhados [!UICONTROL Data Sources] que podem ser usadas por qualquer cliente ou parceiro de dados que funcione com dados vinculados a usuários dessas plataformas.

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
   <td>32 números hexadecimais, geralmente apresentados como 8-4-4-4-12<em>exemplo, 97987bca-ae59-4c7d-94ba-ee4f19ab8c21<br/> </em> </td>
   <td>1352</td>
   <td>Essa ID deve ser coletada em uma Referência de forma bruta/sem hash/inalterada - <a href="https://play.google.com/about/monetization-ads/ads/ad-id/">https://play.google.com/about/monetization-ads/ads/ad-id/</a></td>
  </tr>
  <tr>
   <td>Apple iOS (IDFA)</td>
   <td>20915</td>
   <td>32 números hexadecimais, geralmente apresentados como 8-4-4-4-12 <em>exemplo, 6D92078A-8246-4BA4-AE5B-76104861E7DC<br /> </em> </td>
   <td>3560</td>
   <td>Essa ID deve ser coletada em uma Referência de forma bruta/sem hash/inalterada - <a href="https://support.apple.com/en-us/HT205223">https://support.apple.com/en-us/HT205223</a></td>
  </tr>
  <tr>
   <td>Roku (RIDA)</td>
   <td>121963</td>
   <td>32 números hexadecimais, geralmente apresentados como 8-4-4-4-12 <em>exemplo,</em> <em>fcb2a29c-315a-5e6b-bcfd-d889ba19aada</em></td>
   <td>11536</td>
   <td>Essa ID deve ser coletada em uma Referência de forma bruta/sem hash/inalterada - <a href="https://sdkdocs.roku.com/display/sdkdoc/Roku+Advertising+Framework">https://sdkdocs.roku.com/display/sdkdoc/Roku+Advertising+Framework</a> </td>
  </tr>
  <tr>
   <td>Microsoft Advertising ID (MAID)</td>
   <td>389146</td>
   <td>Sequência numérica alfa</td>
   <td>14593</td>
   <td>Essa ID deve ser coletada em uma Referência de forma bruta/sem hash/inalterada - <a href="https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid">https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid</a><br/><a href="https://msdn.microsoft.com/en-us/library/windows/apps/windows.system.userprofile.advertisingmanager.advertisingid.aspx">https://msdn.microsoft.com/en-us/library/windows/apps/windows.system.userprofile.advertisingmanager.advertisingid.aspx</a></td>
  </tr>
  <tr>
   <td>Samsung DUID</td>
   <td>404660</td>
   <td>Exemplo de string numérica alfa, 7XCBNROQJPYW</td>
   <td>15950</td>
   <td>Essa ID deve ser coletada em uma Referência de forma bruta/sem hash/inalterada - <a href="https://developer.samsung.com/tv/develop/api-references/samsung-product-api-references/productinfo-api">https://developer.samsung.com/tv/develop/api-references/samsung-product-api-references/productinfo-api</a> </td>
  </tr>
</table>

## Definição de um identificador de publicidade no aplicativo {#setting-an-advertising-identifier-in-the-app}

Definir a ID do anunciante no aplicativo é um processo de duas etapas, primeiro recuperar a ID do anunciante e depois enviá-la para o Experience Cloud. Os links são encontrados abaixo para executar essas etapas.

1. Recuperar a ID
   1. [!DNL Apple] informações sobre [!DNL advertising ID] pode ser encontrado [AQUI](https://developer.apple.com/documentation/adsupport/asidentifiermanager).
   1. Algumas informações sobre como definir a variável [!DNL advertiser ID] para [!DNL Android] desenvolvedores podem ser encontrados [AQUI](http://android.cn-mirrors.com/google/play-services/id.html).
1. Envie-o para o Experience Cloud usando o [!DNL setAdvertisingIdentifier] no SDK
   1. Informações para uso `setAdvertisingIdentifier` está no [documentação](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#set-an-advertising-identifier) para ambos [!DNL iOS] e [!DNL Android].

`// iOS (Swift) example for using setAdvertisingIdentifier:`
`ACPCore.setAdvertisingIdentifier([AdvertisingId]) // ...where [AdvertisingId] is replaced by the actual advertising ID`

## Mensagem de erro DCS para IDs incorretas  {#dcs-error-messaging-for-incorrect-ids}

Quando uma ID de dispositivo global incorreta (IDFA, GAID etc) é enviada em tempo real para o Audience Manager, um código de erro será retornado na ocorrência. A seguir, um exemplo de um erro retornado porque a ID é enviada como um [!DNL Apple IDFA], que deve conter somente letras maiúsculas e, no entanto, há um &quot;x&quot; em letras minúsculas na ID.

![imagem de erro](assets/image_4_.png)

Consulte a [documentação](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-error-codes.html?lang=en#api-and-sdk-code) para obter a lista de códigos de erro.

## Integração de IDs de dispositivos globais {#onboarding-global-device-ids}

Além do envio em tempo real de IDs de dispositivos globais, você também pode &quot;[!DNL onboard]&quot; (upload) dados em relação às IDs também. Esse processo é o mesmo de quando você está incorporando dados às IDs do cliente (normalmente por meio de pares de chave/valor), mas simplesmente usa as IDs de fonte de dados apropriadas, para que os dados sejam atribuídos à ID do dispositivo global. A documentação sobre o processo de integração pode ser encontrada no [documentação](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/sending-audience-data/batch-data-transfer-process/batch-data-transfer-overview.html?lang=en#implementation-integration-guides). Lembre-se de usar a ID da fonte de dados global, dependendo da plataforma que você está usando.

Se as IDs de dispositivo global incorretas forem enviadas por meio do processo de integração, os erros serão exibidos na variável [[!DNL Onboarding Status Report]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reporting/onboarding-status-report.html?lang=en#reporting).

A seguir encontra-se um exemplo de erro que viria por esse relatório:

![imagem de erro](assets/image_5_.png)
