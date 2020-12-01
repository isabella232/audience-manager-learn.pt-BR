---
title: Atualização para o DIL da Adobe Audience Manager versão 8.0 (ou superior)
description: Este artigo fornece etapas e recomendações sobre como atualizar o código de Data Integration Library (DIL) do Adobe Audience Manager (AAM) para a versão 8.0 ou posterior. Isso se refere à implementação do DIL "cliente-a-cliente", e não ao encaminhamento de dados Adobe Analytics pelo lado do servidor, e abrangerá o DTM, o Launch by Adobe e as implementações sem a solução do gerenciador de tags Adobe.
feature: dil implementation
topics: null
audience: implementer
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1841
translation-type: tm+mt
source-git-commit: dfd549508cc223714bdb07ac6fd2aa31e6ca5586
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 1%

---


# Atualização para o DIL da Adobe Audience Manager versão 8.0 (ou superior) {#updating-to-adobe-audience-manager-s-dil-version-or-greater}

Este artigo fornecerá etapas e recomendações sobre como atualizar o código Adobe Audience Manager (AAM) [!DNL Data Integration Library] (DIL) para a versão 8.0 ou posterior. Isso se refere à implementação do DIL &quot;cliente-a-cliente&quot;, e não ao encaminhamento de dados Adobe Analytics pelo lado do servidor, e abrangerá o DTM, o Launch by Adobe e as implementações sem a solução do gerenciador de tags Adobe.

## Visão geral {#overview}

O código [!DNL Data Integration Library] (DIL) do Audience Manager permite implementar AAM em seu site*. Ao implementar versões anteriores do DIL, não era necessário ter o serviço de ID do Experience Cloud (ECID) do Adobe (embora fosse uma boa ideia) também implementado. A partir do DIL versão 8.0, há uma dependência forte no ECID versão 3.3 ou posterior. Se você implementar o DIL 8.0 ou posterior sem ECID 3.3 ou com uma versão anterior, aparecerá um erro e ele não funcionará. Como há várias maneiras de implementar AAM, criamos esta página para fornecer algumas etapas a serem seguidas, bem como algumas recomendações. Abaixo, você encontrará essas etapas e recomendações detalhadas pelo método de plataforma/implementação. Mais informações sobre o DIL estão disponíveis na [documentação](https://marketing.adobe.com/resources/help/en_US/aam/c_dil.html).

* Conforme declarado na descrição desta página, isso abrangerá apenas implementações de DIL &quot;do lado do cliente&quot;, usadas por clientes AAM que não têm Adobe Analytics. Se você tiver a Adobe Analytics, deverá usar o método de encaminhamento pelo lado do servidor para implementar AAM. Este método está descrito na [documentação](https://marketing.adobe.com/resources/help/en_US/reference/ssf.html).

## Duplicado e elementos e métodos obsoletos {#duplicate-and-deprecated-elements-and-methods}

Em versões anteriores do DIL e do ECID, existiam métodos duplicados (métodos que executam a mesma função tanto no DIL e no ECID), o que causava confusão em relação a qual usar. Geralmente, você precisava usar ambos e compará-los, e essa mensagem não foi bem comunicada aos nossos clientes. A partir do DIL 8.0, esses métodos e elementos de duplicado foram descontinuados no DIL e recomenda-se o uso da versão ECID.

Por exemplo:

* Ao usar [!DNL DIL.create], alguns elementos foram descontinuados e você deve usar os elementos ECID. Esses elementos são chamados na [[!DNL DIL.create] documentação](https://marketing.adobe.com/resources/help/en_US/aam/r_dil_create.html).
* O método de nível de instância [!DNL idSync] também foi descontinuado, como é chamado em [documentation](https://marketing.adobe.com/resources/help/en_US/aam/r_dil_idsync.html) do método.

## Sincronização de ID com uma ID do cliente {#id-syncing-with-a-customer-id}

No AAM, você pode sincronizar seu UUID (ID de usuário único anônimo) no computador com uma ID do cliente, para que possa carregar dados offline sobre o cliente e conectá-lo ao comportamento online, a fim de obter uma melhor compreensão dos clientes. No passado, isto foi feito de duas formas:

* O método de nível de instância [!DNL idSync]
* O elemento [!DNL declaredId] em [!DNL DIL.create]

Se você tiver usado um desses métodos mais antigos para sincronizar com uma ID do cliente, é altamente recomendável atualizar para usar o método [!DNL setCustomerIDs], que faz parte do Serviço ECID. Mais informações sobre [!DNL setCustomerIDs] estão disponíveis na [documentação](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid_setcustomerids.html) do método.

**Dica rápida:** ao usar um dos métodos acima, você fez referência ao AAM  [!UICONTROL Data Source] com a  [!UICONTROL Data Source] ID (AKA, o &quot;DPID&quot;). Ao atualizar para [!DNL setCustomerIDs], será necessário usar o &quot;[!UICONTROL Integration Code]&quot; do AAM [!UICONTROL Data Source]&quot;. Ele ainda aponta para o mesmo [!UICONTROL Data Source], mas é apenas um identificador diferente. Isso é mostrado no vídeo abaixo.

>[!VIDEO](https://video.tv.adobe.com/v/23873/?quality=12)

As seguintes seções listas etapas e recomendações para atualização para o DIL 8.0 com base no método de implementação:

## Atualização para o DIL 8.0 no Adobe Experience Platform Launch {#updating-to-dil-in-experience-platform-launch}

Etapas básicas para a atualização para o DIL 8.0

1. Se você estiver usando o DIL anterior ao 8.0, antes de atualizar, vá para a configuração do DIL na extensão AAM e anote quaisquer opções avançadas que estiver usando (para serem usadas em uma etapa subsequente)
1. Atualize sua extensão do AAM para a versão 8.0 ou superior
1. Verifique se a sua extensão do serviço de ID de Experience Cloud é a versão 3.3.0 ou superior
1. Para quaisquer métodos/elementos obsoletos (como &quot;[!DNL disableIDSyncs]&quot;) que estejam na extensão de AAM anterior a 8.0 ou no código personalizado para DIL, ative os métodos ECID na extensão ECID.

   1. (DIL) disableDestinationPublishingIframe -> (ECID) disableIdSyncs
   1. (DIL) disableIDSyncs -> (ECID) disableIdSyncs
   1. (DIL) iframeAkamaiHTTPS -> (ECID) dSyncSSLUseAkamai
   1. (DIL) declaradaId -> (ECID) setCustomerIDs

1. Publicar as alterações

>[!VIDEO](https://video.tv.adobe.com/v/23874/?quality=12)

## Atualização para o DIL 8.0 no Adobe DTM {#updating-to-dil-in-adobe-dtm}

1. Atualize sua ferramenta AAM para a versão 8.0 ou superior. Esta configuração de versão está na seção &quot;Geral&quot; da ferramenta AAM.
1. Para quaisquer métodos/elementos obsoletos (como &quot;disableIDSyncs&quot;) que estavam no código personalizado da ferramenta de AAM anterior a 8.0 para o DIL, anote-os (para que você possa adicioná-los à ferramenta ECID) e remova-os do [!DNL DIL code] personalizado na ferramenta de AAM.
1. Atualize sua extensão do serviço de ID de Experience Cloud para a versão 3.3.0 ou superior
1. Adicione as opções avançadas à ferramenta ECID que você removeu do código personalizado da ferramenta AAM.
1. Publicar as alterações

## Atualização para o DIL 8.0 sem solução de gerenciamento de tags do Adobe {#additional-resources}

Se você estiver atualizando seu código diretamente na página, é possível substituir itens mais antigos por itens mais recentes, exceto quando for necessário mover métodos/elementos de DIL para ECID, como discutido acima. Nesse caso, você simplesmente substituirá o método/elemento antigo na localização de DIL pelo método/elemento ECID na localização ECID.

O mesmo vale para os gestores de tags não-Adobe. Sempre que tiver as versões antigas na solução de gerenciamento de tags, substitua-a pelo novo código, conforme descrito nas etapas a seguir.

1. Atualize sua biblioteca de DIL para a versão mais recente (8.0 ou superior) - Você precisará obter o código de DIL do Adobe Consulting ou do Adobe Customer Care, pois ele não está disponível em um local público. Em seguida, basta substituir o código da biblioteca do DIL antigo pelo novo código da biblioteca do DIL e seguir para a próxima etapa (não pare agora ou você terá problemas, ha).
1. Instale [!DNL ECID Service] ou atualize sua versão existente para 3.3.0 ou superior. Você pode baixar a versão mais recente do serviço de ID da Experience Cloud [de nossa página do GitHub](https://github.com/Adobe-Marketing-Cloud/id-service/releases). Se precisar de ajuda com isso, consulte a [documentação](https://marketing.adobe.com/resources/help/pt_BR/mcvid/) ou entre em contato com um consultor Adobe.

1. Verifique se todos os métodos ou elementos obsoletos que estão em seu código personalizado para DIL são movidos para os métodos ECID:

   1. (DIL) disableDestinationPublishingIframe -> (ECID) disableIdSyncs

      [Documentação](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-disableidsync.html)

   1. (DIL) disableIDSyncs -> (ECID) disableIdSyncs

      [Documentação](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-disableidsync.html)

   1. (DIL) iframeAkamaiHTTPS -> (ECID) idSyncSSLUseAkamai

      [Documentação](https://marketing.adobe.com/resources/help/en_US/aam/r_dil_create.html)

   1. (DIL) declaradaId -> (ECID) setCustomerIDs

      [Documentação](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid_setcustomerids.html)