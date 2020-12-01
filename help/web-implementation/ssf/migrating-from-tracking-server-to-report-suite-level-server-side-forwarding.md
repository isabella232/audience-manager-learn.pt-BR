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


# Migração de [!UICONTROL Tracking Server] para [!UICONTROL Report Suite]-Nível [!UICONTROL Server-Side Forwarding] {#migrating-from-tracking-server-to-report-suite-level-server-side-forwarding}

Este artigo e vídeo mostram como ativar [!UICONTROL server-side forwarding] dos [!DNL Analytics] Dados para Audience Manager em um nível [!UICONTROL report suite] em vez de em um nível [!UICONTROL tracking server].

## Introdução {#introduction}

Se você tiver Adobe Audience Manager E Adobe Analytics, poderá implementar &quot;[!UICONTROL Server-side Forwarding]&quot; dos dados [!DNL Analytics] no Audience Manager. Isso significa que, em vez de sua página enviar 2 ocorrências (uma para [!DNL Analytics] e uma para Audience Manager), ela pode simplesmente enviar uma ocorrência para [!DNL Analytics], e [!DNL Analytics] encaminhará esses dados para o Audience Manager. Se você já tiver isso ativado/implementado antes de outubro de 2017, seu [!UICONTROL server-side forwarding] poderá se basear em seu &quot;[!UICONTROL Tracking Server]&quot;, que precisaria ser habilitado pelo Atendimento ao cliente da Adobe ou pela consultoria de Adobe. A partir de outubro de 2017, você pode configurar [!UICONTROL server-side forwarding] por conta própria e fazer isso em um nível [!UICONTROL Report Suite] (encaminhamento PER [!UICONTROL Report Suite]). Há benefícios significativos para isso, que serão discutidos abaixo.

## [!UICONTROL Tracking Server] Encaminhamento  {#tracking-server-forwarding}

Seu [!UICONTROL tracking server] é o local para o qual você está enviando seus dados [!DNL Analytics] e também o domínio no qual a solicitação de imagem e o cookie são gravados. Ele deve ser definido no DTM ou [!DNL Experience Platform Launch], ou no arquivo [!DNL AppMeasurement.js], e normalmente terá a seguinte aparência, com seu site ou nome de empresa substituindo &quot;mysite&quot;:

`s.trackingServer = "mysite.sc.omtrdc.net";`

Se [!UICONTROL server-side forwarding] estiver configurado para encaminhar no nível [!UICONTROL tracking server], qualquer ocorrência que esteja sendo enviada para esse [!UICONTROL tracking server] (SE o Serviço de ID de Experience Cloud também estiver ativado) será encaminhada para o Audience Manager. Isso precisava ser habilitado pelo Atendimento ao cliente da Adobe ou pela consultoria de Adobe. Eles também são os que podem desativá-lo, DEPOIS que você alternar para o encaminhamento [!UICONTROL report suite], conforme descrito abaixo.

Se você não tiver certeza se [!DNL tracking server forwarding] está habilitado para você, entre em contato com o Atendimento ao cliente da Adobe ou com a Adobe Consultoria e eles poderão informá-lo.

## [!UICONTROL Report Suite]-Nível  [!UICONTROL Server-Side Forwarding] {#report-suite-level-server-side-forwarding}

Um dos maiores benefícios para o encaminhamento [!UICONTROL report suite] do encaminhamento [!UICONTROL tracking server] é que agora você poderá usar o &quot;Audience Analytics&quot;, que é a capacidade de redirecionar o Audience Manager [!UICONTROL segments] de volta para o Adobe Analytics para análise detalhada [!UICONTROL segment]. Este excelente recurso NÃO é suportado se você ainda estiver encaminhando [!UICONTROL tracking server] e não [!UICONTROL report suite]. Consulte mais informações sobre o Audience Analytics na [documentação](https://marketing.adobe.com/resources/help/en_US/analytics/audiences/).

>[!VIDEO](https://video.tv.adobe.com/v/23701/?quality=12)

## Dica importante {#additional-resources}

Conforme declarado no vídeo acima, uma vez que todos os [!UICONTROL report suites] estejam configurados para encaminhar para o Audience Manager, entre em contato com o Atendimento ao cliente da Adobe ou com a Consultoria de Adobe e desative o encaminhamento [!UICONTROL tracking server]. Não é uma emergência para você fazer isso, pois ter [!UICONTROL tracking server] encaminhamento e [!UICONTROL report suite] encaminhamento NÃO resultará em ocorrências de duplicado. No entanto, a prática recomendada é ter apenas o encaminhamento [!UICONTROL report suite] ativado. Se você deixar o encaminhamento [!UICONTROL tracking server] ativado, não somente os dados de [!UICONTROL report suites] que você não deseja encaminhar, mas no futuro, depois que você (e todos na sua empresa) tiver esquecido que o encaminhamento [!UICONTROL tracking server] está ativado, você pode achar que os dados não estão sendo encaminhados para um [!UICONTROL report suite] específico (porque ele não está ativado no nível do conjunto de relatórios), mas os dados ainda estão sendo encaminhados por causa do a4/>. [!UICONTROL tracking server] Em seguida, você perderá tempo e dinheiro descobrindo por que está encaminhando e também pagando por chamadas de servidor AAM que você não esperava. Portanto, é uma boa ideia desativar o encaminhamento [!UICONTROL tracking server] assim que você tiver todos os [!UICONTROL report suites] definidos para encaminhar que façam sentido para suas necessidades de negócios.
