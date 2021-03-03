---
title: Migração do servidor de rastreamento para o encaminhamento pelo lado do servidor no nível do conjunto de relatórios
description: Este artigo e vídeo mostram como habilitar o encaminhamento pelo lado do servidor de dados do Analytics para o Audience Manager em um nível de conjunto de relatórios em vez de em um nível de servidor de rastreamento.
product: audience manager, analytics
feature: Integração do Adobe Analytics
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1776
role: '"Desenvolvedor, engenheiro de dados"'
level: Intermediário
translation-type: tm+mt
source-git-commit: a7dc335e75697a7b1720eccdadbb9605fdeda798
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---


# Migração de [!UICONTROL Tracking Server] para [!UICONTROL Report Suite]-Nível [!UICONTROL Server-Side Forwarding] {#migrating-from-tracking-server-to-report-suite-level-server-side-forwarding}

Este artigo e vídeo mostram como habilitar [!UICONTROL server-side forwarding] de [!DNL Analytics] Dados para o Audience Manager em um nível [!UICONTROL report suite] em vez de em um nível [!UICONTROL tracking server].

## Introdução {#introduction}

Se você tiver o Adobe Audience Manager E o Adobe Analytics, poderá implementar &quot;[!UICONTROL Server-side Forwarding]&quot; dos dados [!DNL Analytics] no Audience Manager. Isso significa que, em vez de sua página enviar 2 ocorrências (uma para [!DNL Analytics] e outra para o Audience Manager), ela pode simplesmente enviar uma ocorrência para [!DNL Analytics], e [!DNL Analytics] encaminhará esses dados para o Audience Manager. Se você já tiver ativado ou implementado isso antes de outubro de 2017, seu [!UICONTROL server-side forwarding] pode ser baseado no seu &quot;[!UICONTROL Tracking Server]&quot;, que deve ser habilitado pelo Atendimento ao cliente da Adobe ou pela Adobe Consulting. A partir de outubro de 2017, você poderá configurar [!UICONTROL server-side forwarding] e fazer isso em um nível [!UICONTROL Report Suite] (encaminhando por [!UICONTROL Report Suite]). Há benefícios significativos para isso, que serão discutidos abaixo.

## [!UICONTROL Tracking Server] Encaminhamento  {#tracking-server-forwarding}

Seu [!UICONTROL tracking server] é o local para o qual você está enviando seus dados [!DNL Analytics] e também o domínio em que a solicitação de imagem e o cookie são gravados. Ele deve ser definido no DTM ou [!DNL Experience Platform Launch], ou no arquivo [!DNL AppMeasurement.js], e normalmente será semelhante a isto, com seu site ou nome comercial substituindo &quot;mysite&quot;:

`s.trackingServer = "mysite.sc.omtrdc.net";`

Se [!UICONTROL server-side forwarding] estiver configurado para encaminhar no nível [!UICONTROL tracking server] , qualquer ocorrência que esteja sendo enviada para esse [!UICONTROL tracking server] (SE o Serviço da Experience Cloud ID também estiver habilitado) será encaminhada para o Audience Manager. Isso tinha que ser ativado pelo Atendimento ao cliente da Adobe ou pela Adobe Consulting. Eles também são aqueles que podem desativá-lo, DEPOIS que você mudar para o encaminhamento [!UICONTROL report suite], conforme descrito abaixo.

Se não tiver certeza se [!DNL tracking server forwarding] está ativado para você, entre em contato com o Atendimento ao cliente da Adobe ou com a Adobe Consulting, e eles poderão informar você.

## [!UICONTROL Report Suite]-Nível  [!UICONTROL Server-Side Forwarding] {#report-suite-level-server-side-forwarding}

Um dos maiores benefícios de passar para o [!UICONTROL report suite] encaminhamento a partir do [!UICONTROL tracking server] é que agora você poderá usar o &quot;Audience Analytics&quot;, que é a capacidade de encaminhar o Audience Manager [!UICONTROL segments] de volta para o Adobe Analytics para análise [!UICONTROL segment] detalhada. Esse excelente recurso NÃO é suportado se você ainda estiver encaminhando [!UICONTROL tracking server] e não [!UICONTROL report suite]. Consulte mais informações sobre o Audience Analytics na [documentação](https://marketing.adobe.com/resources/help/en_US/analytics/audiences/).

>[!VIDEO](https://video.tv.adobe.com/v/23701/?quality=12)

## Dica importante {#additional-resources}

Conforme declarado no vídeo acima, depois que todas as [!UICONTROL report suites] forem encaminhadas para o Audience Manager, você deverá entrar em contato com o Atendimento ao cliente da Adobe ou com a Adobe Consulting e desativá-las o encaminhamento [!UICONTROL tracking server]. Não é uma emergência para você fazer isso, pois ter o encaminhamento [!UICONTROL tracking server] e [!UICONTROL report suite] NÃO resultará em ocorrências duplicadas. No entanto, é uma prática recomendada ter apenas o encaminhamento [!UICONTROL report suite] ativado. Se você deixar o [!UICONTROL tracking server] encaminhamento ativado, não somente os dados de [!UICONTROL report suites] que você não deseja encaminhar, como também no futuro, depois que você (e todos na empresa) esquecer que o [!UICONTROL tracking server] encaminhamento está ativado, você pode pensar que os dados não estão sendo encaminhados para um [!UICONTROL report suite] específico (porque não está ativado no nível de conjunto de relatórios), mas os dados ainda estão sendo encaminhados por &lt;a 4/>. [!UICONTROL tracking server] Em seguida, você perderá tempo e dinheiro descobrindo por que está encaminhando e também pagando por chamadas de servidor AAM que você não esperava. Portanto, é apenas uma boa ideia desativar o encaminhamento [!UICONTROL tracking server] assim que tiver todos os [!UICONTROL report suites] definidos para encaminhar que façam sentido às suas necessidades de negócios.
