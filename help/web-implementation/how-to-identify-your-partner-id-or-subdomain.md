---
title: Como identificar sua ID de parceiro ou subdomínio de Audience Manager
description: Ao implementar alguns recursos do Experience Cloud, você precisa saber qual é a sua "ID de parceiro" do Audience Manager (também conhecida como "ID de cliente" ou "Subdomínio"). Neste vídeo, mostraremos dois lugares onde você pode obter essa ID na interface do usuário do Audience Manager.
feature: implementation basics
topics: null
audience: implementer
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2359
translation-type: tm+mt
source-git-commit: a108c51fdad66f4e7974eb96609b6d8f058cb6ff
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---


# Como identificar seu subdomínio de Audience Manager {#how-to-identify-your-audience-manager-partner-id-or-subdomain}

Ao implementar alguns recursos de Experience Cloud, você precisa saber o que é seu Audience Manager `Subdomain` (também conhecido como seu `client ID` ou `Partner ID`). Neste vídeo, mostraremos dois lugares onde você pode obter essas informações na interface do usuário do Audience Manager.

## Dando o final... {#giving-away-the-ending}

Caso você prefira apenas pular para dentro e encontrá-lo sem assistir a este vídeo curto, você pode encontrar seu site `Partner Subdomain` em dois lugares na interface do usuário:

1. Se você já tiver criado um [!UICONTROL rule-based] [!UICONTROL trait], clique em **[!UICONTROL Get Trait URL]**
   [!UICONTROL Get Trait URL] está ao lado do [!UICONTROL trait] na lista de [!UICONTROL traits] na pasta e o URL incluirá seu subdomínio no URL.
1. Se você acessar a interface **[!UICONTROL Tools]** > **[!UICONTROL Tags]** e clicar **[!UICONTROL Get code]** para o seu container, o subdomínio será direcionado para o final da linha Akamai

Se você não conseguir encontrá-lo rapidamente com essas referências rápidas, o vídeo é um compromisso de pouco tempo. :)

>[!VIDEO](https://video.tv.adobe.com/v/25922/?quality=12)

>[!IMPORTANT]
>
>Há uma ID numérica atribuída a cada cliente da Adobe Experience Cloud, que geralmente é chamada de &quot;PID&quot; ou ID de parceiro. Esta não é a ID de que estamos falando neste artigo e vídeo. Em vez disso, o &quot;subdomínio do parceiro&quot;, que às vezes é conhecido como a ID do parceiro, geralmente é uma versão do nome do cliente e é o subdomínio do servidor para o qual os dados são enviados. Por exemplo, se sua empresa for &quot;Bob&#39;s Knobs&quot; (todas as coisas são puxadas pela porta, claro, haha), então é provável que o subdomínio do seu parceiro seja &quot;bobsknobs&quot;, enquanto o &quot;PID&quot; seria algo mais parecido com &quot;12345&quot;. Normalmente, você não precisa saber seu PID, mas seu subdomínio é importante saber, para que você possa configurar sua implementação do Audience Manager.

