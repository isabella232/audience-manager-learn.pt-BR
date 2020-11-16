---
title: Migração do servidor de rastreamento para o encaminhamento pelo lado do servidor no nível do conjunto de relatórios
description: Este artigo e vídeo mostrarão como ativar o encaminhamento dos dados do Analytics pelo lado do servidor para Audience Manager no nível de conjunto de relatórios em vez de no nível do servidor de rastreamento.
product: audience manager, analytics
feature: integration with analytics
topics: null
audience: implementer
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1776
translation-type: tm+mt
source-git-commit: dfd549508cc223714bdb07ac6fd2aa31e6ca5586
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# Migração de [!UICONTROL Tracking Server] para [!UICONTROL Report Suite]nível [!UICONTROL Server-Side Forwarding] {#migrating-from-tracking-server-to-report-suite-level-server-side-forwarding}

Este artigo e vídeo mostrarão como ativar a opção [!UICONTROL server-side forwarding] de [!DNL Analytics] Dados para Audience Manager em um [!UICONTROL report suite] nível em vez de em um [!UICONTROL tracking server] nível.

## Introdução {#introduction}

Se você tiver Adobe Audience Manager E Adobe Analytics, poderá implementar &quot;[!UICONTROL Server-side Forwarding]&quot; dos [!DNL Analytics] dados no Audience Manager. Isso significa que, em vez de sua página enviar 2 ocorrências (uma para [!DNL Analytics] e uma para o Audience Manager), ela pode simplesmente enviar uma ocorrência para [!DNL Analytics]e [!DNL Analytics] encaminhar esses dados para o Audience Manager. Se você já tiver isso ativado/implementado antes de outubro de 2017, [!UICONTROL server-side forwarding] poderá ser baseado em seu &quot;[!UICONTROL Tracking Server]&quot;, que precisaria ser habilitado pelo Atendimento ao cliente da Adobe ou pela Adobe Consulting. A partir de outubro de 2017, você pode configurar- [!UICONTROL server-side forwarding] se e fazer isso em um [!UICONTROL Report Suite] nível (encaminhamento PER [!UICONTROL Report Suite]). Há benefícios significativos para isso, que serão discutidos abaixo.

## [!UICONTROL Tracking Server] Encaminhamento {#tracking-server-forwarding}

Seu local [!UICONTROL tracking server] é o local para o qual você está enviando seus [!DNL Analytics] dados e também o domínio no qual a solicitação de imagem e o cookie são gravados. Ele deve ser definido no DTM ou [!DNL Experience Platform Launch], ou no [!DNL AppMeasurement.js] arquivo, e normalmente será parecido com isso, com seu site ou nome comercial substituindo &quot;mysite&quot;:

`s.trackingServer = "mysite.sc.omtrdc.net";`

Se [!UICONTROL server-side forwarding] estiver configurado para encaminhar no [!UICONTROL tracking server] nível, qualquer ocorrência que estiver sendo enviada para esse [!UICONTROL tracking server] (SE o serviço de ID de Experience Cloud também estiver ativado) será encaminhada para o Audience Manager. Isso precisava ser habilitado pelo Atendimento ao cliente da Adobe ou pela consultoria de Adobe. Eles também são os que podem desativá-la, DEPOIS que você mudar para o [!UICONTROL report suite] encaminhamento, como descrito abaixo.

Se você não tiver certeza se [!DNL tracking server forwarding] está habilitado para você, entre em contato com o Atendimento ao cliente da Adobe ou com a consultoria de Adobe e eles poderão informá-lo.

## [!UICONTROL Report Suite]-Nível [!UICONTROL Server-Side Forwarding] {#report-suite-level-server-side-forwarding}

Um dos maiores benefícios para o [!UICONTROL report suite] encaminhamento a partir do [!UICONTROL tracking server] encaminhamento é que agora você poderá usar o &quot;Audience Analytics&quot;, que é a capacidade de encaminhar o Audience Manager [!UICONTROL segments] de volta para a Adobe Analytics para [!UICONTROL segment] obter análise detalhada. Este excelente recurso NÃO é suportado se você ainda estiver [!UICONTROL tracking server] encaminhando e não [!UICONTROL report suite] encaminhando. Consulte mais informações sobre o Audience Analytics na [documentação](https://marketing.adobe.com/resources/help/en_US/analytics/audiences/).

>[!VIDEO](https://video.tv.adobe.com/v/23701/?quality=12)

## Dica importante {#additional-resources}

Conforme declarado no vídeo acima, uma vez que tudo esteja [!UICONTROL report suites] definido para encaminhar para o Audience Manager, entre em contato com o Atendimento ao cliente da Adobe ou com a Consultoria de Adobe e desative o [!UICONTROL tracking server] encaminhamento. Não é uma emergência para você fazer isso, pois ter tanto o [!UICONTROL tracking server] encaminhamento quanto o [!UICONTROL report suite] encaminhamento NÃO resultará em ocorrências de duplicado. No entanto, a prática recomendada é apenas [!UICONTROL report suite] reencaminhar. Se você deixar o [!UICONTROL tracking server] encaminhamento ligado, não somente os dados dos quais você não deseja encaminhar, mas no futuro, depois que você (e todos na sua empresa) tiver esquecido que o [!UICONTROL report suites] encaminhamento está ativado, você pode achar que os dados não estão sendo encaminhados para um determinado [!UICONTROL tracking server] (porque não estão ativados no nível do conjunto de relatórios), mas os dados ainda estão sendo encaminhados por causa do [!UICONTROL report suite] [!UICONTROL tracking server]. Em seguida, você perderá tempo e dinheiro descobrindo por que está encaminhando e também pagando por chamadas de servidor AAM que você não esperava. Portanto, é uma boa ideia desativar o [!UICONTROL tracking server] encaminhamento assim que você tiver todos os [!UICONTROL report suites] recursos para encaminhar que façam sentido para suas necessidades comerciais.
