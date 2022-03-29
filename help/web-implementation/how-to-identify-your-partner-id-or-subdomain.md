---
title: Como identificar a ID do parceiro ou o subdomínio
description: Saiba como identificar a ID do parceiro ou o subdomínio ao implementar alguns recursos do Experience Cloud e sobre dois lugares onde você pode obter essa ID na interface do usuário do Audience Manager.
feature: Implementation Basics
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2359
role: Developer, Data Engineer
level: Intermediate
exl-id: d3f4a12d-acc5-47b7-a38a-a6a14152bf3a
source-git-commit: 62b43b5627dabf754cf821f974a56c60989ef7ef
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Como identificar o subdomínio do Audience Manager {#how-to-identify-your-audience-manager-partner-id-or-subdomain}

Ao implementar alguns recursos do Experience Cloud, você precisa saber qual é o seu Audience Manager `Subdomain` é (também conhecido como seu `client ID` ou `Partner ID`). Neste vídeo, mostraremos dois locais onde você pode obter essas informações na interface do usuário do Audience Manager.

## Dando o final... {#giving-away-the-ending}

Caso prefira simplesmente entrar e encontrá-lo sem assistir a este pequeno vídeo, você pode encontrar sua `Partner Subdomain` em dois locais na interface do usuário do :

1. Se você já criou uma [!UICONTROL rule-based] característica, clique **[!UICONTROL Get Trait URL]**
   [!UICONTROL Get Trait URL] está ao lado da característica na lista de características dessa pasta e o URL incluirá seu subdomínio no URL.
1. Se você entrar no **[!UICONTROL Tools]** > **[!UICONTROL Tags]** e clique em **[!UICONTROL Get code]** para seu contêiner, o subdomínio fica em direção ao final da linha Akamai

Se você não conseguir encontrá-lo rapidamente com essas referências rápidas, o vídeo é um compromisso de pouco tempo. :)

>[!VIDEO](https://video.tv.adobe.com/v/25922/?quality=12)

>[!IMPORTANT]
>
>Há uma ID numérica atribuída a cada cliente da Adobe Experience Cloud, geralmente chamada de &quot;PID&quot; ou ID do parceiro. Esta não é a ID sobre a qual estamos falando neste artigo e vídeo. Em vez disso, o &quot;subdomínio do parceiro&quot;, que às vezes é chamado de ID do parceiro, geralmente é uma versão do nome do cliente e é o subdomínio do servidor para o qual os dados são enviados. Por exemplo, se sua empresa é &quot;Bob&#39;s Knobs&quot; (todas as coisas dão nozes, é claro, haha), é provável que o subdomínio de seu parceiro seja &quot;bobsknobs&quot;, enquanto o &quot;PID&quot; seria algo mais parecido com &quot;12345&quot;. Normalmente, você não precisa saber seu PID, mas seu subdomínio é importante saber, para que você possa configurar a implementação do Audience Manager.
