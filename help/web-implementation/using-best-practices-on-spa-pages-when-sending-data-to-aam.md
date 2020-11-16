---
title: Uso de práticas recomendadas em páginas SPA ao enviar dados para AAM
description: Neste documento, descreveremos várias práticas recomendadas que você deve seguir e estar ciente ao enviar dados de Aplicativos de página única (SPA) para a Adobe Audience Manager (AAM). Este documento se concentrará em usar o Launch by Adobe, que é o método de implementação recomendado.
feature: implementation basics
topics: spa
audience: implementer
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1390
translation-type: tm+mt
source-git-commit: a108c51fdad66f4e7974eb96609b6d8f058cb6ff
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# Uso de práticas recomendadas em páginas SPA ao enviar dados para AAM {#using-best-practices-on-spa-pages-when-sending-data-to-aam}

Neste documento, descreveremos várias práticas recomendadas que você deve seguir e estar ciente ao enviar dados do [!UICONTROL Single Page Applications] (SPA) para a Adobe Audience Manager (AAM). Este doc se concentra em usar [!UICONTROL Experience Platform Launch], que é o método de implementação recomendado.

## Notas iniciais

* Os itens abaixo assumirão que você está usando [!DNL Platform Launch] para implementar em seu site. As considerações ainda existirão se você não estiver usando [!DNL Platform Launch], mas precisaria adaptá-las ao seu método de implementação.
* Todos os SPA são diferentes, portanto, talvez seja necessário ajustar alguns dos itens a seguir para melhor atender às suas necessidades, mas queríamos compartilhar algumas práticas recomendadas com você. itens que você precisa pensar ao enviar dados de páginas SPA para Audience Manager.

## Diagrama simples de como trabalhar com SPA e AAM em Experience Platform Launch {#simple-diagram-of-working-with-spas-and-aam-in-experience-platform-launch}

![spa for aam in [!DNL launch]](assets/spa_for_aam_in_launch.png)

>[!NOTE]
>Como declarado, este é um diagrama simplificado de como as páginas SPA são tratadas em uma implementação do Adobe Audience Manager (sem Adobe Analytics) usando [!DNL Platform Launch]. Como podem ver, é bastante direto, com a grande decisão de como você vai comunicar uma mudança visualização (ou uma ação) para [!DNL Platform Launch].

## Acionamento [!DNL Launch] da página SPA {#triggering-launch-from-the-spa-page}

Dois dos métodos mais comuns para acionar uma regra no [!DNL Platform Launch] (e, portanto, enviar dados para o Audience Manager) são:

* Configuração de eventos personalizados JavaScript (consulte exemplo [AQUI](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html) com Adobe Analytics)
* Usando um [!UICONTROL Direct Call Rule]

Neste exemplo de Audience Manager, vamos usar um [!UICONTROL Direct Call rule] em [!DNL Launch] para disparar a ocorrência para Audience Manager. Como você verá nas próximas seções, isso se torna útil ao configurar o valor [!UICONTROL Data Layer] para um novo valor, para que ele possa ser selecionado pelo [!UICONTROL Data Element] campo em [!DNL Platform Launch].

## Página de demonstração {#demo-page}

Criamos uma pequena página de demonstração que demonstra como alterar um valor no e enviá-lo para AAM, como você pode fazer em uma página SPA. [!DNL data layer] Essa funcionalidade pode ser modelada para alterações mais elaboradas necessárias. Você pode encontrar esta página de demonstração [AQUI](https://aam.enablementadobe.com/SPA-Launch.html).

## A definição da variável [!DNL data layer] {#setting-the-data-layer}

Conforme mencionado, quando um novo conteúdo é carregado na página ou quando alguém executa uma ação no site, o [!DNL data layer] precisa ser definido dinamicamente no cabeçalho da página ANTES [!DNL Launch] é chamado e executa o [!UICONTROL rules], de modo que [!DNL Platform Launch] seja possível coletar os novos valores do [!DNL data layer] e empurrá-los para o Audience Manager.

Se você for ao site de demonstração listado acima e observar a fonte da página, você verá:

* O [!DNL data layer] está no cabeçalho da página, antes da chamada para [!DNL Platform Launch]
* O JavaScript no link de SPA simulado altera as chamadas [!UICONTROL Data Layer]e ENTÃO [!DNL Platform Launch] (a chamada _satellite.track()). Se você estivesse usando eventos personalizados JavaScript em vez disso, a lição seria a mesma [!UICONTROL Direct Call Rule]. Primeiro mude o [!DNL data layer]e depois ligue [!DNL Launch].

>[!VIDEO](https://video.tv.adobe.com/v/23322/?quality=12)

## Recursos adicionais {#additional-resources}

* [SPA discussão nos fóruns do Adobe](https://forums.adobe.com/thread/2451022)
* [Sites de arquitetura de referência para mostrar como implementar SPA no Launch by Adobe](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html)
* [Usar práticas recomendadas ao rastrear SPA no Adobe Analytics](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html)
* [Site de demonstração usado neste artigo](https://aam.enablementadobe.com/SPA-Launch.html)
