---
title: Atualização para o Adobe Audience Manager DIL versão 8.0 (ou superior)
description: Este artigo fornecerá etapas e recomendações sobre como atualizar o código da Data Integration Library (DIL) do Adobe Audience Manager (AAM) para a versão 8.0 ou posterior. Isso se refere à implementação de DIL do "lado do cliente", não ao encaminhamento do lado do servidor de dados da Adobe Analytics, e cobrirá o DTM, o Launch by Adobe e as implementações sem a solução de gerenciador de tags Adobe.
feature: DIL Implementation
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1841
role: Developer, Data Engineer
level: Intermediate
exl-id: 8c1e6ed5-0f21-427b-a681-0ecb020a0e60
source-git-commit: 62b43b5627dabf754cf821f974a56c60989ef7ef
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 1%

---

# Atualização para o DIL do Adobe Audience Manager versão 8.0 (ou superior) {#updating-to-adobe-audience-manager-s-dil-version-or-greater}

Este artigo fornecerá etapas e recomendações sobre a atualização do Adobe Audience Manager (AAM) [!DNL Data Integration Library] (DIL) para a versão 8.0 ou posterior. Isso se refere à implementação de DIL do &quot;lado do cliente&quot;, não ao encaminhamento do lado do servidor de dados da Adobe Analytics, e cobrirá o DTM, o Launch by Adobe e as implementações sem a solução de gerenciador de tags Adobe.

## Visão geral {#overview}

do Audience Manager [!DNL Data Integration Library] O código (DIL) permite implementar o AAM no seu site*. Ao implementar as versões anteriores do DIL, não era necessário ter o Experience Cloud ID Service (ECID) do Adobe implementado também (embora fosse uma ótima ideia). A partir do DIL versão 8.0, há uma dependência forte na ECID versão 3.3 ou posterior. Se você implementar o DIL 8.0 ou posterior sem a ECID 3.3 ou com uma versão anterior, ocorrerá um erro e ela não funcionará. Como há várias maneiras de implementar o AAM, criamos esta página para fornecer algumas etapas a serem seguidas, bem como algumas recomendações. Abaixo, você encontrará essas etapas e recomendações divididas por plataforma/método de implementação. Mais informações sobre o DIL estão disponíveis em [documentação](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=en).

* Conforme dito na descrição desta página, serão abordadas apenas implementações de DIL do &quot;lado do cliente&quot;, usadas por clientes AAM que não têm Adobe Analytics. Se tiver o Adobe Analytics, você deve usar o método de encaminhamento pelo lado do servidor para implementar o AAM. Este método é descrito na seção [documentação](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/server-side-forwarding/ssf.html).

## Métodos e elementos duplicados e obsoletos {#duplicate-and-deprecated-elements-and-methods}

Em versões anteriores do DIL e da ECID, havia métodos duplicados (métodos que fazem a mesma função no DIL e na ECID), o que causou confusão em relação a qual usar. Normalmente, você precisava usar os dois e combiná-los, e essa mensagem não era bem comunicada aos nossos clientes. A partir do DIL 8.0, esses métodos e elementos duplicados foram descontinuados no DIL e é recomendável usar a versão ECID.

Por exemplo:

* Ao usar [!DNL DIL.create], alguns elementos foram descontinuados e você deve usar os elementos ECID. Esses elementos são apresentados na [[!DNL DIL.create] documentação](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/class-level-dil-methods/dil-create.html).
* A variável [!DNL idSync] método em nível de instância também foi descontinuado, como chamado na seção [documentação](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-instance-methods.html).

## Sincronização de ID com uma ID do cliente {#id-syncing-with-a-customer-id}

No AAM, você pode sincronizar a UUID (ID de usuário exclusiva anônima) no computador com uma ID do cliente, para poder carregar dados offline sobre esse cliente e vinculá-los ao comportamento online dele, para obter uma melhor compreensão dos clientes. No passado, isso foi feito de uma das duas seguintes maneiras:

* A variável [!DNL idSync] método de nível de instância
* A variável [!DNL declaredId] elemento em [!DNL DIL.create]

Se você tem usado um desses métodos mais antigos para sincronizar com uma ID do cliente, é altamente recomendável atualizar para usando o [!DNL setCustomerIDs] que faz parte do serviço ECID. Mais informações sobre [!DNL setCustomerIDs] está disponível no do método [documentação](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html).

**Dica Rápida:** Ao usar um dos métodos acima, você fez referência ao AAM [!UICONTROL Data Source] com o [!UICONTROL Data Source] ID (também conhecido como &quot;DPID&quot;). Ao atualizar para [!DNL setCustomerIDs], será necessário usar o AAM [!UICONTROL Data Source]do &quot;[!UICONTROL Integration Code]&quot; em vez disso. Ele ainda aponta para o mesmo [!UICONTROL Data Source] mas é apenas um identificador diferente. Isso é mostrado no vídeo abaixo.

>[!VIDEO](https://video.tv.adobe.com/v/23873/?quality=12)

As seções a seguir listam as etapas e recomendações para atualização para o DIL 8.0 de acordo com seu método de implementação:

## Atualização para o DIL 8.0 nas tags Adobe Experience Platform {#updating-to-dil-in-experience-platform-launch}

Etapas básicas para atualização para o DIL 8.0

1. Se você estiver usando DIL anterior a 8.0, antes de atualizar, entre na configuração de DIL na extensão AAM e anote todas as opções avançadas que estiver usando (para ser usada em uma etapa subsequente).
1. Atualize sua extensão do AAM para a versão 8.0 ou superior.
1. Verifique se a sua extensão do Experience Cloud ID Service é versão 3.3.0 ou superior.
1. Para quaisquer métodos/elementos obsoletos (como `disableIDSyncs`) que estavam na extensão AAM pré-8.0 ou no código personalizado para DIL, ative os métodos ECID na extensão ECID.

   1. (DIL) `disableDestinationPublishingIframe` -> (ECID) `disableIdSyncs`
   1. (DIL) `disableIDSyncs` -> (ECID) `disableIdSyncs`
   1. (DIL) `iframeAkamaiHTTPS` -> (ECID) `dSyncSSLUseAkamai`
   1. (DIL) `declaredId` -> (ECID) `setCustomerIDs`

1. Publique as alterações.

>[!VIDEO](https://video.tv.adobe.com/v/23874/?quality=12)

## Atualização para o DIL 8.0 no Adobe DTM {#updating-to-dil-in-adobe-dtm}

1. Atualize sua ferramenta AAM para a versão 8.0 ou superior. Essa configuração de versão está na seção &quot;Geral&quot; da ferramenta AAM.
1. Para quaisquer métodos/elementos obsoletos (como `disableIDSyncs`) que estavam em seu código personalizado da Ferramenta AAM pré-8.0 para DIL, anote-os (para que você possa adicioná-los à ferramenta ECID) e remova-os da ferramenta personalizada [!DNL DIL code] na ferramenta AAM.
1. Atualize sua extensão do Experience Cloud ID Service para a versão 3.3.0 ou superior
1. Adicione as opções avançadas à ferramenta ECID que você removeu do código personalizado da ferramenta AAM.
1. Publicar as alterações

## Atualização para o DIL 8.0 sem solução Adobe Tag Management {#additional-resources}

Se você estiver atualizando seu código diretamente na página, poderá apenas substituir itens mais antigos por itens mais novos, exceto quando for necessário mover métodos/elementos de DIL para ECID, conforme discutido acima. Nesse caso, basta substituir o método/elemento antigo no local do DIL pelo método/elemento da ECID no local da ECID.

O mesmo vale para os gerenciadores de tags não-Adobe. Sempre que você tiver as versões antigas nessa solução de gerenciamento de tags, substitua-a pelo novo código, conforme descrito nas etapas a seguir.

1. Atualize sua biblioteca de DIL para a versão mais recente (8.0 ou superior). Você precisará obter o código de DIL mais recente da Adobe Consulting ou do Adobe Customer Care, pois ele não está disponível atualmente em um local público. Em seguida, basta substituir o código antigo da biblioteca de DIL pelo novo código da biblioteca de DIL e seguir para a próxima etapa (não pare agora ou você terá problemas, ha).
1. Instalar [!DNL ECID Service] ou atualize sua versão existente para 3.3.0 ou posterior. Você pode baixar a versão mais recente do serviço de ID de Experience Cloud [na nossa página do GitHub](https://github.com/Adobe-Marketing-Cloud/id-service/releases). Se precisar de ajuda, consulte [documentação](https://experienceleague.adobe.com/docs/id-service/using/home.html) ou fale com um consultor da Adobe.

1. Verifique se todos os métodos ou elementos obsoletos que estão no código personalizado para DIL foram movidos para os métodos ECID:

   1. (DIL) `disableDestinationPublishingIframe` -> (ECID) `disableIdSyncs`

      [Documentação](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/disableidsync.html)

   1. (DIL) `disableIDSyncs` -> (ECID) `disableIdSyncs`

      [Documentação](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/disableidsync.html)

   1. (DIL) `iframeAkamaiHTTPS` -> (ECID) `idSyncSSLUseAkamai`

      [Documentação](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/class-level-dil-methods/dil-create.html)

   1. (DIL) `declaredId` -> (ECID) `setCustomerIDs`

      [Documentação](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html)
