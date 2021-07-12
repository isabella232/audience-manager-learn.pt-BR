---
title: Atualização para o Adobe Audience Manager DIL versão 8.0 (ou superior)
description: Este artigo fornecerá etapas e recomendações sobre como atualizar o código de Data Integration Library (DIL) do Adobe Audience Manager (AAM) para a versão 8.0 ou posterior. Isso se refere à implementação de DIL "no lado do cliente", não ao encaminhamento de dados do Adobe Analytics pelo lado do servidor, e abordará o DTM, o Launch by Adobe e as implementações sem solução de gerenciador de tags do Adobe.
feature: Implementação de DIL
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1841
role: Developer, Data Engineer
level: Intermediate
exl-id: 8c1e6ed5-0f21-427b-a681-0ecb020a0e60
source-git-commit: 4b91696f840518312ec041abdbe5217178aee405
workflow-type: tm+mt
source-wordcount: '1151'
ht-degree: 1%

---

# Atualização para o DIL do Adobe Audience Manager versão 8.0 (ou superior) {#updating-to-adobe-audience-manager-s-dil-version-or-greater}

Este artigo fornecerá etapas e recomendações sobre como atualizar o código do Adobe Audience Manager (AAM) [!DNL Data Integration Library] (DIL) para a versão 8.0 ou posterior. Isso se refere à implementação de DIL &quot;no lado do cliente&quot;, não ao encaminhamento de dados do Adobe Analytics pelo lado do servidor, e abordará o DTM, o Launch by Adobe e as implementações sem solução de gerenciador de tags do Adobe.

## Visão geral {#overview}

O código [!DNL Data Integration Library] (DIL) do Audience Manager permite implementar AAM em seu site*. Ao implementar versões anteriores do DIL, não era necessário ter o Serviço de ID de Experience Cloud (ECID) do Adobe também implementado (embora fosse uma ótima ideia). A partir do DIL versão 8.0, há uma grande dependência no ECID versão 3.3 ou posterior. Se implementar o DIL 8.0 ou posterior sem a ECID 3.3 ou com uma versão anterior, você receberá um erro e ele não funcionará. Como há várias maneiras de implementar o AAM, criamos esta página para fornecer algumas etapas a serem seguidas, bem como algumas recomendações. Abaixo você encontrará essas etapas e recomendações detalhadas por plataforma/método de implementação. Mais informações sobre o DIL estão disponíveis na [documentação](https://marketing.adobe.com/resources/help/en_US/aam/c_dil.html).

* Conforme declarado na descrição desta página, isso só abordará implementações de DIL &quot;do lado do cliente&quot;, usadas por clientes do AAM que não têm o Adobe Analytics. Se tiver o Adobe Analytics, você deve usar o método de encaminhamento do lado do servidor para implementar o AAM. Esse método é descrito na [documentação](https://marketing.adobe.com/resources/help/en_US/reference/ssf.html).

## Elementos e métodos duplicados e obsoletos {#duplicate-and-deprecated-elements-and-methods}

Em versões anteriores do DIL e da ECID, havia métodos duplicativos (métodos que fazem a mesma função no DIL e na ECID), o que causou confusão em relação ao que usar. Normalmente, você precisa usar ambos e combiná-los, e essa mensagem não foi bem comunicada para nossos clientes. A partir do DIL 8.0, esses métodos e elementos duplicados foram descontinuados no DIL e é recomendável usar a versão ECID.

Por exemplo:

* Ao usar [!DNL DIL.create], alguns elementos foram descontinuados e você deve usar os elementos ECID em vez disso. Esses elementos são chamados na [[!DNL DIL.create] documentação](https://marketing.adobe.com/resources/help/en_US/aam/r_dil_create.html).
* O método de nível de instância [!DNL idSync] também foi preterido, como chamado em [documentation](https://marketing.adobe.com/resources/help/en_US/aam/r_dil_idsync.html) do método.

## Sincronização de ID com uma ID do cliente {#id-syncing-with-a-customer-id}

No AAM, você pode sincronizar o UUID (ID de usuário exclusiva anônima) no computador com uma ID do cliente, para fazer upload de dados offline sobre esse cliente e vinculá-los ao comportamento online, a fim de obter uma melhor compreensão dos clientes. No passado, isso foi feito de duas formas:

* O método de nível de instância [!DNL idSync]
* O elemento [!DNL declaredId] em [!DNL DIL.create]

Se você tem usado um desses métodos mais antigos para sincronizar com uma ID do cliente, é altamente recomendável atualizar para o uso do método [!DNL setCustomerIDs], que faz parte do Serviço ECID. Mais informações sobre [!DNL setCustomerIDs] estão disponíveis na [documentação](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid_setcustomerids.html) do método.

**Dica rápida:** ao usar anteriormente um dos métodos acima, você fez referência ao AAM  [!UICONTROL Data Source] com a  [!UICONTROL Data Source] ID (conhecida como &quot;DPID&quot;). Ao atualizar para [!DNL setCustomerIDs], será necessário usar o &quot;[!UICONTROL Integration Code]&quot; do AAM [!UICONTROL Data Source]&quot;. Ele ainda aponta para o mesmo [!UICONTROL Data Source], mas é apenas um identificador diferente. Isso é mostrado no vídeo abaixo.

>[!VIDEO](https://video.tv.adobe.com/v/23873/?quality=12)

As seções a seguir listam as etapas e recomendações para atualização para o DIL 8.0 com base no método de implementação:

## Atualização para o DIL 8.0 no Adobe Experience Platform Launch {#updating-to-dil-in-experience-platform-launch}

Etapas básicas para a atualização para o DIL 8.0

1. Se você estiver usando o DIL pré-8.0, antes de atualizar, acesse a configuração do DIL na extensão AAM e anote todas as opções avançadas que estiver usando (para ser usadas em uma etapa subsequente)
1. Atualize sua extensão do AAM para a versão 8.0 ou superior
1. Verifique se a sua extensão do Experience Cloud ID Service é versão 3.3.0 ou superior
1. Para quaisquer métodos/elementos obsoletos (como &quot;[!DNL disableIDSyncs]&quot;) que estavam na Extensão de AAM anterior a 8.0 ou no código personalizado para o DIL, ative os métodos ECID na extensão ECID.

   1. (DIL) disableDestinationPublishingIframe -> (ECID) disableIdSyncs
   1. (DIL) disableIDSyncs -> (ECID) disableIdSyncs
   1. (DIL) iframeAkamaiHTTPS -> (ECID) dSyncSSLUseAkamai
   1. (DIL) declaradaId -> (ECID) setCustomerIDs

1. Publicar as alterações

>[!VIDEO](https://video.tv.adobe.com/v/23874/?quality=12)

## Atualização para o DIL 8.0 no Adobe DTM {#updating-to-dil-in-adobe-dtm}

1. Atualize sua ferramenta de AAM para a versão 8.0 ou superior. Essa configuração de versão está na seção &quot;Geral&quot; da ferramenta AAM.
1. Para quaisquer métodos/elementos obsoletos (como &quot;disableIDSyncs&quot;) que estavam no código personalizado da ferramenta de AAM anterior a 8.0 para o DIL, anote-os (para que você possa adicioná-los à ferramenta ECID) e removê-los do [!DNL DIL code] personalizado na ferramenta de AAM.
1. Atualize sua extensão do Experience Cloud ID Service para a versão 3.3.0 ou superior
1. Adicione as opções avançadas à ferramenta ECID que você removeu do código personalizado da ferramenta de AAM.
1. Publicar as alterações

## Atualização para o DIL 8.0 sem solução de gerenciamento de tags do Adobe {#additional-resources}

Se você estiver atualizando seu código diretamente na página, poderá apenas substituir itens mais antigos por itens mais novos, exceto quando precisar mover métodos/elementos do DIL para a ECID, conforme discutido acima. Nesse caso, basta substituir o método/elemento antigo no local do DIL pelo método/elemento ECID no local da ECID.

O mesmo vale para os gerentes de tags que não são Adobe. Sempre que você tiver as versões antigas nessa solução de gerenciamento de tags, substitua-a pelo novo código, conforme descrito nas etapas a seguir.

1. Atualize sua biblioteca do DIL para a versão mais recente (8.0 ou superior) - Você precisará obter o código do DIL da Adobe Consulting ou do Adobe Customer Care, pois ele não está disponível em um local público. Em seguida, basta substituir o antigo código da biblioteca de DIL pelo novo código da biblioteca de DIL e seguir para a próxima etapa (não pare agora ou você terá problemas, ha).
1. Instale [!DNL ECID Service] ou atualize sua versão existente para 3.3.0 ou superior. Você pode baixar a versão mais recente do Serviço de ID do Experience Cloud [em nossa página do GitHub](https://github.com/Adobe-Marketing-Cloud/id-service/releases). Se precisar de ajuda com isso, consulte a [documentação](https://marketing.adobe.com/resources/help/pt_BR/mcvid/) ou entre em contato com um consultor de Adobe.

1. Verifique se os métodos ou elementos obsoletos que estão em seu código personalizado para o DIL são movidos para os métodos ECID:

   1. (DIL) disableDestinationPublishingIframe -> (ECID) disableIdSyncs

      [Documentação](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-disableidsync.html)

   1. (DIL) disableIDSyncs -> (ECID) disableIdSyncs

      [Documentação](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-disableidsync.html)

   1. (DIL) iframeAkamaiHTTPS -> (ECID) idSyncSSLUseAkamai

      [Documentação](https://marketing.adobe.com/resources/help/en_US/aam/r_dil_create.html)

   1. (DIL) declaradaId -> (ECID) setCustomerIDs

      [Documentação](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid_setcustomerids.html)
