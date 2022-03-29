---
title: Migrar do servidor de rastreamento para o encaminhamento pelo lado do servidor no nível do conjunto de relatórios
description: Saiba como habilitar o encaminhamento pelo lado do servidor dos dados do Adobe Analytics para o Audience Manager em um nível de conjunto de relatórios em vez de em um nível de servidor de rastreamento.
product: audience manager
feature: Adobe Analytics Integration
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1776
role: Developer, Data Engineer
level: Intermediate
exl-id: 08b81e52-a28a-43e4-a284-df2460a43016
source-git-commit: 4adaade180545bcf5f911b7453a7e9939e2ed178
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 0%

---

# Migrar do servidor de rastreamento para o encaminhamento pelo lado do servidor no nível do conjunto de relatórios {#migrating-from-tracking-server-to-report-suite-level-server-side-forwarding}

Este artigo e vídeo mostrarão como habilitar o encaminhamento pelo lado do servidor de [!DNL Analytics] Dados para o Audience Manager a [!UICONTROL report suite] em vez de em uma [!UICONTROL tracking server] nível.

## Introdução {#introduction}

Se você tiver o Adobe Audience Manager E o Adobe Analytics, poderá implementar o encaminhamento pelo lado do servidor do [!DNL Analytics] dados para o Audience Manager. Isso significa que, em vez de sua página enviar duas ocorrências (uma para [!DNL Analytics] e um para o Audience Manager), ele pode enviar uma ocorrência para [!DNL Analytics]e [!DNL Analytics] O encaminhará esses dados para o Audience Manager.

Se você já estiver executando e se estiver habilitado/implementado antes de outubro de 2017, o encaminhamento pelo lado do servidor pode ser baseado no [!UICONTROL Tracking Server], que precisavam ser ativadas pelo Atendimento ao cliente do Adobe ou pela Adobe Consulting. A partir de outubro de 2017, você poderá configurar o encaminhamento pelo lado do servidor e fazer isso em um nível de conjunto de relatórios (encaminhamento por conjunto de relatórios). Há benefícios significativos para isso, que é discutido abaixo.

## [!UICONTROL Tracking server] encaminhamento {#tracking-server-forwarding}

Seu [!UICONTROL tracking server] é o local para o qual você está enviando seu [!DNL Analytics] e também o domínio em que a solicitação de imagem e o cookie são gravados. Ela deve ser definida no DTM ou [!DNL Experience Platform Launch]ou no [!DNL AppMeasurement.js] e normalmente terá esta aparência, com seu site ou nome comercial substituindo &quot;mysite&quot;:

`s.trackingServer = "mysite.sc.omtrdc.net";`

Se o encaminhamento pelo lado do servidor estiver configurado para ser encaminhado no [!UICONTROL tracking server] , qualquer ocorrência que esteja sendo enviada para esse [!UICONTROL tracking server] (SE o Serviço de ID de Experience Cloud também estiver ativado) será encaminhado para o Audience Manager. Isso tinha que ser ativado pelo Adobe Customer Care ou Adobe Consulting. Eles também são aqueles que podem desativá-lo, depois que você mudar para [!UICONTROL report suite] como descrito abaixo.

Se não tiver certeza se [!DNL tracking server forwarding] O está habilitado para você, entre em contato com o Atendimento ao cliente do Adobe ou com a Adobe Consulting e eles devem poder informar você.

## [!UICONTROL Report-suite]Encaminhamento no nível do servidor {#report-suite-level-server-side-forwarding}

Um dos maiores benefícios para mudar para [!UICONTROL report suite] encaminhar de [!UICONTROL tracking server] o encaminhamento do é que você agora poderá usar o &quot;Audience Analytics&quot;, que é a capacidade de encaminhar o Audience Manager [!UICONTROL segments] volte ao Adobe Analytics para obter a análise detalhada do segmento. Este recurso excelente NÃO é suportado se você ainda estiver em [!UICONTROL tracking server] encaminhamento e não [!UICONTROL report suite] encaminhamento. Veja mais informações sobre o Audience Analytics na seção [documentação](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html).

>[!VIDEO](https://video.tv.adobe.com/v/23701/?quality=12)

## Dica importante {#additional-resources}

Conforme declarado no vídeo acima, uma vez que você tenha todos os [!UICONTROL report suites] configurado para encaminhar para o Audience Manager, você deve entrar em contato com o Atendimento ao cliente do Adobe ou com a Consultoria do Adobe e fazer com que desative o [!UICONTROL tracking server] encaminhamento. Não é uma emergência para você fazer isso, porque ter ambos [!UICONTROL tracking server] encaminhamento e [!UICONTROL report suite] o encaminhamento não resulta em ocorrências duplicadas. No entanto, a prática recomendada é ter apenas [!UICONTROL report suite] encaminhamento em.

Se você sair [!UICONTROL tracking server] encaminhar em, e não somente poderá encaminhar dados de [!UICONTROL report suites] que você não deseja encaminhar, mas no futuro, depois que você (e todos na sua empresa) esquecer que [!UICONTROL tracking server] o encaminhamento está ativado, você pode achar que os dados não estão sendo encaminhados para um [!UICONTROL report suite]. Isso ocorre porque ele não está ativado no nível do conjunto de relatórios, mas os dados ainda estão sendo encaminhados por causa do [!UICONTROL tracking server]. Em seguida, você perderá tempo e dinheiro descobrindo por que está encaminhando e também pagando por chamadas de servidor AAM que você não esperava. Portanto, é uma boa ideia desativar [!UICONTROL tracking server] encaminhar assim que tiver todas as [!UICONTROL report suites] configurada para encaminhar o que faz sentido para as necessidades de sua empresa.
