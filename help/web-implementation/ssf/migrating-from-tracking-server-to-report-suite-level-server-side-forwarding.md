---
title: Migração do servidor de rastreamento para o encaminhamento do lado do servidor no nível do conjunto de relatórios
description: Saiba como ativar o encaminhamento pelo lado do servidor de dados do Adobe Analytics para o Audience Manager em um nível de conjunto de relatórios, em vez de em um nível de servidor de rastreamento.
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

# Migração do servidor de rastreamento para o encaminhamento do lado do servidor no nível do conjunto de relatórios {#migrating-from-tracking-server-to-report-suite-level-server-side-forwarding}

Este artigo e vídeo mostrarão como habilitar o encaminhamento pelo lado do servidor do [!DNL Analytics] Dados para Audience Manager em um [!UICONTROL report suite] em vez de em um [!UICONTROL tracking server] nível.

## Introdução {#introduction}

Se você tiver o Adobe Audience Manager E o Adobe Analytics, poderá implementar o encaminhamento pelo lado do servidor do [!DNL Analytics] dados para Audience Manager. Isso significa que, em vez de sua página enviar duas ocorrências (uma para [!DNL Analytics] e um para o Audience Manager), pode enviar uma ocorrência para [!DNL Analytics], e [!DNL Analytics] encaminhará esses dados para o Audience Manager.

Se você já tiver esse recurso ativo e em execução, e se ele tiver sido habilitado/implementado antes de outubro de 2017, o encaminhamento pelo lado do servidor poderá se basear no [!UICONTROL Tracking Server], que deveria ser ativado pelo Atendimento ao cliente do Adobe ou pela Adobe Consulting. A partir de outubro de 2017, agora você pode configurar o encaminhamento pelo lado do servidor sozinho e fazer isso em nível de conjunto de relatórios (encaminhamento por conjunto de relatórios). Há benefícios significativos para isso, que são discutidos abaixo.

## [!UICONTROL Tracking server] encaminhamento {#tracking-server-forwarding}

Seu [!UICONTROL tracking server] é o local para o qual você está enviando seu [!DNL Analytics] e também o domínio no qual a solicitação de imagem e o cookie são gravados. Ele deve ser definido no DTM ou [!DNL Experience Platform Launch], ou no [!DNL AppMeasurement.js] arquivo, e normalmente terá esta aparência, com seu nome de site ou comercial substituindo &quot;mysite&quot;:

`s.trackingServer = "mysite.sc.omtrdc.net";`

Se o encaminhamento pelo lado do servidor estiver configurado para ser encaminhado no [!UICONTROL tracking server] nível, qualquer ocorrência que estiver sendo enviada para este [!UICONTROL tracking server] (SE o Serviço de ID de Experience Cloud também estiver ativado) será encaminhado para o Audience Manager. Isso tinha que ser ativado pelo Atendimento ao cliente do Adobe ou pela Adobe Consulting. Também são eles que podem desativá-lo, DEPOIS que você mudar para [!UICONTROL report suite] conforme descrito abaixo.

Se não tiver certeza se [!DNL tracking server forwarding] estiver ativado para você, entre em contato com o Atendimento ao cliente da Adobe ou com a Consultoria da Adobe e você deverá ser informado por eles.

## [!UICONTROL Report-suite]Encaminhamento pelo lado do servidor no nível da {#report-suite-level-server-side-forwarding}

Um dos maiores benefícios de mudar para [!UICONTROL report suite] encaminhamento de [!UICONTROL tracking server] o encaminhamento é que agora você poderá usar &quot;Audience Analytics&quot;, que é a capacidade de encaminhar Audience Manager [!UICONTROL segments] no Adobe Analytics para análise detalhada de segmentos. Este excelente recurso NÃO é suportado se você ainda estiver em [!UICONTROL tracking server] encaminhamento e não [!UICONTROL report suite] encaminhamento. Consulte mais informações sobre o Audience Analytics na [documentação](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html).

>[!VIDEO](https://video.tv.adobe.com/v/23701/?quality=12)

## Dica importante {#additional-resources}

Conforme dito no vídeo acima, uma vez que você tenha todos os [!UICONTROL report suites] definido para encaminhar que deseja encaminhar para Audience Manager, entre em contato com o Atendimento ao cliente da Adobe ou com a Adobe Consulting e solicite a desativação de [!UICONTROL tracking server] encaminhamento. Não é uma emergência para você fazer isso, porque ter ambos [!UICONTROL tracking server] encaminhamento e [!UICONTROL report suite] o encaminhamento não resulta em ocorrências duplicadas. No entanto, é prática recomendada ter apenas [!UICONTROL report suite] encaminhando em.

Se você sair [!UICONTROL tracking server] encaminhando o, ele não apenas encaminhará os dados do [!UICONTROL report suites] que você não deseja encaminhar, mas no futuro, depois que você (e todos na sua empresa) esqueceram isso [!UICONTROL tracking server] encaminhamento estiver ativado, você pode achar que os dados não estão sendo encaminhados para uma [!UICONTROL report suite]. Isso ocorre porque ele não está ativado no nível do conjunto de relatórios, mas os dados ainda estão sendo encaminhados devido à [!UICONTROL tracking server]. Em seguida, você perderá tempo e dinheiro descobrindo por que ele está encaminhando e também pagando por chamadas de servidor AAM que você não esperava. Portanto, é uma boa ideia desativar o [!UICONTROL tracking server] encaminhando assim que tiver todos os [!UICONTROL report suites] defina como encaminhar para atender às suas necessidades comerciais.
