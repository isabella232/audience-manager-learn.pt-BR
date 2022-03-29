---
title: Usar as práticas recomendadas em páginas SPA ao enviar dados para o AAM
description: Conheça as práticas recomendadas para enviar dados de aplicativos de página única (SPA) para o Adobe Audience Manager (AAM). Este artigo foca no uso de tags Experience Platform, o método de implementação recomendado.
feature: Implementation Basics
topics: spa
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1390
topic: SPA
role: Developer, Data Engineer
level: Experienced
exl-id: 99ec723a-dd56-4355-a29f-bd6d2356b402
source-git-commit: d4874d9f6d7a36bb81ac183eb8b853d893822ae0
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Usar as práticas recomendadas em páginas SPA ao enviar dados para o AAM {#using-best-practices-on-spa-pages-when-sending-data-to-aam}

Este documento descreve várias práticas recomendadas para enviar dados de aplicativos de página única (SPA) para o Adobe Audience Manager (AAM). Este artigo foca em usar [!UICONTROL Experience Platform tags], o método de implementação recomendado.

## Notas iniciais

* Os itens abaixo presumirão que você está usando tags de plataforma para implementar em seu site. As considerações ainda existem se você não estiver usando tags da plataforma, mas precisará adaptá-las ao seu método de implementação.
* Todos os SPA são diferentes, portanto, talvez seja necessário ajustar alguns dos itens a seguir para atender melhor suas necessidades, mas o Adobe deseja compartilhar algumas práticas recomendadas que você precisa considerar ao enviar dados de páginas SPA para o Audience Manager.

## Diagrama simples de como trabalhar com SPA e AAM em tags Experience Platform (anteriormente, Launch){#simple-diagram-of-working-with-spas-and-aam-in-experience-platform-launch}

![spa para aam nas tags](assets/spa_for_aam_in_launch.png)

>[!NOTE]
>Conforme dito, este é um diagrama simplificado de como as páginas de SPA são tratadas em uma implementação do Adobe Audience Manager (sem Adobe Analytics) usando tags da plataforma. Como você pode ver, é bastante direto, com a grande decisão de como você vai comunicar uma mudança de exibição (ou uma ação) às tags da plataforma.

## Acionamento de tags da página de SPA {#triggering-launch-from-the-spa-page}

Dois dos métodos mais comuns para acionar uma regra nas tags da Platform (e, portanto, enviar dados para o Audience Manager) são:

* Configuração de eventos personalizados JavaScript (consulte o exemplo [AQUI](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html) com Adobe Analytics)
* Uso de uma [!UICONTROL Direct Call Rule]

Neste exemplo de Audience Manager, use um [!UICONTROL Direct Call rule] nas tags da Platform para acionar a ocorrência no Audience Manager. Como você verá nas próximas seções, isso se torna útil ao definir a variável [!UICONTROL Data Layer] para um novo valor, para que possa ser selecionado pela variável [!UICONTROL Data Element] nas tags da Platform.

## Página de demonstração {#demo-page}

Esta é uma pequena página que demonstra como alterar um valor na camada de dados e enviá-lo para o Audience Manager, como você pode fazer em uma página de SPA. Essa funcionalidade pode ser modelada para alterações mais elaboradas necessárias. Você pode encontrar esta página de demonstração [AQUI](https://aam.enablementadobe.com/SPA-Launch.html).

## Configuração da camada de dados {#setting-the-data-layer}

Conforme mencionado, quando o novo conteúdo é carregado na página ou quando alguém executa uma ação no site, a camada de dados precisa ser definida dinamicamente no cabeçalho da página ANTES que as tags da plataforma sejam chamadas e execute o [!UICONTROL rules], para que as tags da Platform possam coletar os novos valores da camada de dados e enviá-los para o Audience Manager.

Caso vá para o site de demonstração listado acima e veja a fonte da página, você verá:

* A camada de dados está no cabeçalho da página, antes da chamada para tags da plataforma
* O JavaScript no link de SPA simulado altera a variável [!UICONTROL Data Layer], em seguida, chama as tags da plataforma (a variável `_satellite.track()` call). Se você estava usando eventos personalizados JavaScript em vez disso [!UICONTROL Direct Call Rule], a lição é a mesma. Primeira alteração [!DNL data layer]e, em seguida, chame as tags da plataforma .

>[!VIDEO](https://video.tv.adobe.com/v/23322/?quality=12)

## Recursos adicionais {#additional-resources}

* [SPA discussão sobre os fóruns do Adobe](https://forums.adobe.com/thread/2451022)
* [Sites de arquitetura de referência para mostrar como implementar SPA nas tags de plataforma](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html)
* [Usar as práticas recomendadas ao rastrear SPA no Adobe Analytics](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html)
* [Site de demonstração usado para este artigo](https://aam.enablementadobe.com/SPA-Launch.html)
