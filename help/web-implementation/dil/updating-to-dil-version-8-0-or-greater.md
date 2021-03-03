---
title: Atualização para o Adobe Audience Manager DIL versão 8.0 (ou superior)
description: Este artigo fornecerá etapas e recomendações sobre como atualizar o código da Biblioteca de integração de dados (DIL) do Adobe Audience Manager (AAM) para a versão 8.0 ou posterior. Isso se refere à implementação da DIL do "lado do cliente", não ao encaminhamento pelo lado do servidor dos dados do Adobe Analytics, e abordará o DTM, o Launch da Adobe e as implementações sem a solução do gerenciador de tags da Adobe.
feature: Implementação de DIL
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1841
role: '"Desenvolvedor, engenheiro de dados"'
level: Intermediário
translation-type: tm+mt
source-git-commit: a7dc335e75697a7b1720eccdadbb9605fdeda798
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 1%

---


# Atualização para o DIL do Adobe Audience Manager versão 8.0 (ou superior) {#updating-to-adobe-audience-manager-s-dil-version-or-greater}

Este artigo fornecerá etapas e recomendações sobre como atualizar o código do Adobe Audience Manager (AAM) [!DNL Data Integration Library] (DIL) para a versão 8.0 ou posterior. Isso se refere à implementação da DIL do &quot;lado do cliente&quot;, não ao encaminhamento pelo lado do servidor dos dados do Adobe Analytics, e abordará o DTM, o Launch da Adobe e as implementações sem a solução do gerenciador de tags da Adobe.

## Visão geral {#overview}

O código [!DNL Data Integration Library] (DIL) do Audience Manager permite implementar o AAM em seu site*. Ao implementar versões anteriores do DIL, não era necessário ter o Serviço da Experience Cloud ID (ECID) da Adobe implementado também (embora fosse uma ótima ideia). A partir do DIL versão 8.0, há uma grande dependência no ECID versão 3.3 ou posterior. Se você implementar o DIL 8.0 ou posterior sem a ECID 3.3 ou com uma versão anterior, você receberá um erro e ele não funcionará. Como há várias maneiras de implementar o AAM, criamos esta página para fornecer algumas etapas a serem seguidas, bem como algumas recomendações. Abaixo você encontrará essas etapas e recomendações detalhadas por plataforma/método de implementação. Mais informações sobre a DIL estão disponíveis na [documentação](https://marketing.adobe.com/resources/help/en_US/aam/c_dil.html).

* Conforme declarado na descrição desta página, isso só abordará implementações DIL &quot;do lado do cliente&quot;, usadas por clientes do AAM que não têm o Adobe Analytics. Se tiver o Adobe Analytics, você deve usar o método de encaminhamento do lado do servidor para implementar o AAM. Esse método é descrito na [documentação](https://marketing.adobe.com/resources/help/en_US/reference/ssf.html).

## Elementos e métodos duplicados e obsoletos {#duplicate-and-deprecated-elements-and-methods}

Em versões anteriores do DIL e da ECID, havia métodos duplicados (métodos que fazem a mesma função no DIL e na ECID), o que causou confusão em relação a qual usar. Normalmente, você precisa usar ambos e combiná-los, e essa mensagem não foi bem comunicada para nossos clientes. A partir do DIL 8.0, esses métodos e elementos duplicados foram descontinuados no DIL e é recomendável usar a versão do ECID.

Por exemplo:

* Ao usar [!DNL DIL.create], alguns elementos foram descontinuados e você deve usar os elementos ECID em vez disso. Esses elementos são chamados na [[!DNL DIL.create] documentação](https://marketing.adobe.com/resources/help/en_US/aam/r_dil_create.html).
* O método de nível de instância [!DNL idSync] também foi preterido, como chamado em [documentation](https://marketing.adobe.com/resources/help/en_US/aam/r_dil_idsync.html) do método.

## Sincronização de ID com uma ID do cliente {#id-syncing-with-a-customer-id}

No AAM, você pode sincronizar sua UUID (ID de usuário exclusiva anônima) na máquina com uma ID do cliente, para fazer upload de dados offline sobre esse cliente e vinculá-los ao comportamento online, a fim de obter uma melhor compreensão dos clientes. No passado, isso foi feito de duas formas:

* O método de nível de instância [!DNL idSync]
* O elemento [!DNL declaredId] em [!DNL DIL.create]

Se você tem usado um desses métodos mais antigos para sincronizar com uma ID do cliente, é altamente recomendável atualizar para o uso do método [!DNL setCustomerIDs], que faz parte do Serviço ECID. Mais informações sobre [!DNL setCustomerIDs] estão disponíveis na [documentação](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid_setcustomerids.html) do método.

**Dica rápida:** ao usar anteriormente um dos métodos acima, você fez referência ao AAM  [!UICONTROL Data Source] com a  [!UICONTROL Data Source] ID (ou seja, o &quot;DPID&quot;). Ao atualizar para [!DNL setCustomerIDs], você precisará usar o &quot;[!UICONTROL Data Source]&quot; do AAM em vez disso. [!UICONTROL Integration Code] Ele ainda aponta para o mesmo [!UICONTROL Data Source], mas é apenas um identificador diferente. Isso é mostrado no vídeo abaixo.

>[!VIDEO](https://video.tv.adobe.com/v/23873/?quality=12)

As seções a seguir listam as etapas e recomendações para atualização para o DIL 8.0 com base no método de implementação:

## Atualização para DIL 8.0 no Adobe Experience Platform Launch {#updating-to-dil-in-experience-platform-launch}

Etapas básicas para a atualização para o DIL 8.0

1. Se você estiver usando o DIL pré-8.0, antes de atualizar, acesse a configuração do DIL na extensão AAM e anote todas as opções avançadas que estiver usando (para ser usadas em uma etapa subsequente)
1. Atualize sua extensão do AAM para a versão 8.0 ou superior
1. Verifique se a sua extensão do Experience Cloud ID Service é versão 3.3.0 ou superior
1. Para quaisquer métodos/elementos obsoletos (como &quot;[!DNL disableIDSyncs]&quot;) que estivessem em sua extensão AAM anterior a 8.0 ou no código personalizado para DIL, ative os métodos ECID na extensão ECID.

   1. (DIL) disableDestinationPublishingIframe -> (ECID) disableIdSyncs
   1. (DIL) disableIDSyncs -> (ECID) disableIdSyncs
   1. (DIL) iframeAkamaiHTTPS -> (ECID) dSyncSSLUseAkamai
   1. (DIL) declaradaId -> (ECID) setCustomerIDs

1. Publicar as alterações

>[!VIDEO](https://video.tv.adobe.com/v/23874/?quality=12)

## Atualização para DIL 8.0 no Adobe DTM {#updating-to-dil-in-adobe-dtm}

1. Atualize sua ferramenta AAM para a versão 8.0 ou superior. Essa configuração de versão está na seção &quot;Geral&quot; da ferramenta AAM.
1. Para quaisquer métodos/elementos obsoletos (como &quot;disableIDSyncs&quot;) que estavam no código personalizado da ferramenta AAM anterior a 8.0 para DIL, anote-os (para que você possa adicioná-los à ferramenta ECID) e removê-los do [!DNL DIL code] personalizado na ferramenta AAM.
1. Atualizar a extensão do Experience Cloud ID Service para a versão 3.3.0 ou superior
1. Adicione as opções avançadas à ferramenta ECID que você removeu do código personalizado da ferramenta AAM.
1. Publicar as alterações

## Atualização para DIL 8.0 sem solução de gerenciamento de tags da Adobe {#additional-resources}

Se você estiver atualizando seu código diretamente na página, poderá apenas substituir itens mais antigos por itens mais novos, exceto quando precisar mover métodos/elementos de DIL para ECID, conforme discutido acima. Nesse caso, basta substituir o método/elemento antigo no local do DIL pelo método/elemento ECID no local da ECID.

O mesmo se aplica aos gerenciadores de tags que não são da Adobe. Sempre que você tiver as versões antigas nessa solução de gerenciamento de tags, substitua-a pelo novo código, conforme descrito nas etapas a seguir.

1. Atualize sua biblioteca DIL para a versão mais recente (8.0 ou superior) - Você precisará obter o código DIL mais recente da Adobe Consulting ou do Atendimento ao cliente da Adobe, pois ela não está disponível em um local público no momento. Em seguida, basta substituir o antigo código da biblioteca DIL pelo novo código da biblioteca DIL e seguir para a próxima etapa (não pare agora ou você terá problemas, ha).
1. Instale [!DNL ECID Service] ou atualize sua versão existente para 3.3.0 ou superior. Você pode baixar a versão mais recente do Serviço da Experience Cloud ID [em nossa página do GitHub](https://github.com/Adobe-Marketing-Cloud/id-service/releases). Se precisar de ajuda com isso, consulte a [documentação](https://marketing.adobe.com/resources/help/pt_BR/mcvid/) ou fale com um consultor da Adobe.

1. Verifique se todos os métodos ou elementos obsoletos do código personalizado para DIL foram movidos para os métodos ECID:

   1. (DIL) disableDestinationPublishingIframe -> (ECID) disableIdSyncs

      [Documentação](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-disableidsync.html)

   1. (DIL) disableIDSyncs -> (ECID) disableIdSyncs

      [Documentação](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-disableidsync.html)

   1. (DIL) iframeAkamaiHTTPS -> (ECID) idSyncSSLUseAkamai

      [Documentação](https://marketing.adobe.com/resources/help/en_US/aam/r_dil_create.html)

   1. (DIL) declaradaId -> (ECID) setCustomerIDs

      [Documentação](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid_setcustomerids.html)