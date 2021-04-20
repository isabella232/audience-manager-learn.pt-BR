---
title: Uso de práticas recomendadas em páginas SPA ao enviar dados para o AAM
description: Neste documento, descreveremos várias práticas recomendadas que você deve seguir e estar ciente ao enviar dados de Aplicativos de página única (SPA) para o Adobe Audience Manager (AAM). Este documento se concentrará em usar o Launch da Adobe, que é o método de implementação recomendado.
feature: Implementation Basics
topics: spa
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1390
topic: SPA
role: "Developer, Data Engineer"
level: Experienced
translation-type: tm+mt
source-git-commit: a7dc335e75697a7b1720eccdadbb9605fdeda798
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---


# Uso de práticas recomendadas em páginas SPA ao enviar dados para o AAM {#using-best-practices-on-spa-pages-when-sending-data-to-aam}

Neste documento, descreveremos várias práticas recomendadas que você deve seguir e estar ciente ao enviar dados de [!UICONTROL Single Page Applications] (SPA) para o Adobe Audience Manager (AAM). Este documento se concentra em usar [!UICONTROL Experience Platform Launch], que é o método de implementação recomendado.

## Observações iniciais

* Os itens abaixo presumirão que você está usando [!DNL Platform Launch] para implementar o em seu site. As considerações ainda existiriam se você não estivesse usando [!DNL Platform Launch], mas precisaria adaptá-las ao seu método de implementação.
* Todos os SPAs são diferentes, portanto, talvez seja necessário ajustar alguns dos itens a seguir para melhor atender às suas necessidades, mas queremos compartilhar algumas práticas recomendadas com você; coisas que você precisa pensar ao enviar dados de páginas do SPA para o Audience Manager.

## Diagrama simples de como trabalhar com SPAs e AAM no Experience Platform Launch {#simple-diagram-of-working-with-spas-and-aam-in-experience-platform-launch}

![spa para aam em  [!DNL launch]](assets/spa_for_aam_in_launch.png)

>[!NOTE]
>Conforme dito, este é um diagrama simplificado de como as páginas de SPA são tratadas em uma implementação do Adobe Audience Manager (sem o Adobe Analytics) usando [!DNL Platform Launch]. Como você pode ver, é bastante direto, com a grande decisão sendo como você vai comunicar uma mudança de exibição (ou uma ação) para [!DNL Platform Launch].

## Acionando [!DNL Launch] da página SPA {#triggering-launch-from-the-spa-page}

Dois dos métodos mais comuns para acionar uma regra em [!DNL Platform Launch] (e, portanto, enviar dados para o Audience Manager) são:

* Definir eventos personalizados do JavaScript (consulte o exemplo [HERE](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html) com o Adobe Analytics)
* Usar um [!UICONTROL Direct Call Rule]

Neste exemplo do Audience Manager, vamos usar um [!UICONTROL Direct Call rule] em [!DNL Launch] para acionar a ocorrência que entra no Audience Manager. Como você verá nas próximas seções, isso se torna útil ao configurar o [!UICONTROL Data Layer] para um novo valor, para que ele possa ser selecionado pelo [!UICONTROL Data Element] em [!DNL Platform Launch].

## Página de demonstração {#demo-page}

Criamos uma pequena página de demonstração que demonstra a alteração de um valor no [!DNL data layer] e o envio para o AAM, como você pode fazer em uma página SPA. Essa funcionalidade pode ser modelada para alterações mais elaboradas necessárias. Você pode encontrar esta página de demonstração [HERE](https://aam.enablementadobe.com/SPA-Launch.html).

## A definição da variável [!DNL data layer] {#setting-the-data-layer}

Conforme mencionado, quando o novo conteúdo é carregado na página ou quando alguém executa uma ação no site, o [!DNL data layer] precisa ser definido dinamicamente no cabeçalho da página ANTES que [!DNL Launch] seja chamado e execute o [!UICONTROL rules], para que [!DNL Platform Launch] possa escolher os novos valores do [!DNL data layer] e enviá-los para o Audience Manager.

Caso vá para o site de demonstração listado acima e veja a fonte da página, você verá:

* O [!DNL data layer] está no cabeçalho da página, antes da chamada para [!DNL Platform Launch]
* O JavaScript no link SPA simulado altera o [!UICONTROL Data Layer] e ENTÃO chama [!DNL Platform Launch] (a chamada _satellite.track() ). Se você estava usando eventos personalizados JavaScript em vez deste [!UICONTROL Direct Call Rule], a lição é a mesma. Primeiro, altere o [!DNL data layer] e depois chame [!DNL Launch].

>[!VIDEO](https://video.tv.adobe.com/v/23322/?quality=12)

## Recursos adicionais {#additional-resources}

* [Discussão sobre o SPA nos fóruns da Adobe](https://forums.adobe.com/thread/2451022)
* [Sites de arquitetura de referência para mostrar como implementar o SPA no Launch da Adobe](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html)
* [Usar as práticas recomendadas ao rastrear o SPA no Adobe Analytics](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html)
* [Site de demonstração usado para este artigo](https://aam.enablementadobe.com/SPA-Launch.html)
