---
title: Aumente o ROAS usando modelos algorítmicos (semelhantes)
description: O poder real da modelagem semelhante do Audience Manager é quando você busca expandir seu público-alvo de linha de base em relação a uma qualidade, um novo conjunto de usuários de fontes de dados secundárias e de terceiros. Neste tutorial, aprenda as etapas para criar um modelo a partir desses dados.
feature: Algorithmic Models
topics: null
activity: use
doc-type: feature video
team: Technical Marketing
thumbnail: 25188.jpg
kt: 1849
role: User, Developer, Data Engineer, Architect, Data Architect, Admin, Leader
level: Intermediate
exl-id: 6626ae11-8709-4302-9e03-0d55878d2409
source-git-commit: 2094d3bcf658913171afa848e4228653c71c41de
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 0%

---

# Aumente o ROAS usando modelos algorítmicos (semelhantes) no Audience Manager {#increase-roas-by-using-algorithmic-look-alike-models-in-audience-manager}

O verdadeiro poder do Audience Manager [!UICONTROL Modeling] vem quando você busca expandir seu público-alvo de linha de base em relação a um novo conjunto de usuários de qualidade e novidade de fontes de dados secundárias e de terceiros. Neste tutorial, aprenda as etapas necessárias para criar um modelo a partir desses dados.

## Habilitar fluxos de dados de terceiros ou secundários do Audience Marketplace {#enable-2nd-or-3rd-party-data-streams-from-the-audience-marketplace}

Para usar dados secundários e de terceiros em um modelo semelhante, primeiro precisamos habilitar esses dados na interface do Audience Manager. O Adobe tem um grande número de provedores de dados secundários e de terceiros dos quais você pode escolher. Eles estão disponíveis para você em uma interface de autoatendimento no AAM, por meio do Audience Marketplace. Navegue até o Audience Marketplace e navegue pelas possibilidades. O vídeo a seguir mostrará como fazer isso, incluindo como ativar fluxos gratuitos de &quot;tente antes de comprar&quot;, para que você possa se bloquear nos dados que serão mais úteis para sua organização antes de se comprometer com o preço do provedor de dados.

Além disso, para ajudá-lo a pesquisar e decidir qual provedor de dados usar, um grande recurso é o [[!DNL Adobe Audience Finder]](https://www.adobe-audience-finder.com/).

>[!VIDEO](https://video.tv.adobe.com/v/25188/?quality=12)

## Identificar ou criar uma característica ou segmento ideal do usuário (conversão) {#identify-create-an-ideal-user-conversion-trait-or-segment}

O que você está tentando fazer com que as pessoas façam em seu site? Qual é o seu evento de conversão? É claro que há muitas respostas diferentes para essa pergunta, dependendo do tipo/vertical do site e das metas organizacionais. Em qualquer caso, é comum AAM criar uma característica para visitantes que atenderam a esses critérios.

No vídeo abaixo, mostrarei como criar uma característica de conversão, que você desejará ter em vigor à medida que continuar neste tutorial e criar um modelo semelhante.

Além disso, ao usar eventos do Adobe Analytics para criar características, há um grande ganho que você precisa ter em mente, para que não colete mais usuários do que deveria na característica. Assista ao vídeo a seguir para a grande revelação. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**OBSERVAÇÃO:** No vídeo acima, o exemplo que mostro assume que você tem o Adobe Analytics. Obviamente, pode não ser esse o caso. Se você tiver o Google Analytics (GA), temos um módulo que pode ser usado para enviar dados para o AAM (consulte o [documentação](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-modules.html)) e se sua atividade de conversão no seu site for enviada para AAM por GA, você poderá criar sua característica de conversão a partir disso. Se você tiver uma solução de análise diferente (ou nenhuma solução de análise), ainda poderá enviar dados para o AAM por meio do nosso código de DIL e do `submit` , etc. (consulte o [documentação](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html)). Em seguida, crie a característica de conversão com base nos dados enviados quando a atividade de conversão for executada no site.

## Criar um modelo semelhante a partir de dados secundários ou de terceiros {#create-a-look-alike-model-from-2nd-or-3rd-party-data}

Depois de concluir as etapas acima, estamos prontos para criar um Modelo algorítmico (semelhança). À medida que configuramos o modelo, usaremos a característica de conversão como nossa característica base (visitantes principais que queremos duplicar) e usaremos o fluxo de dados de terceiros habilitado como nosso pool de pessoas para extrair.

>[!VIDEO](https://video.tv.adobe.com/v/25190/?quality-12)

## Prática recomendada importante {#an-important-best-practice}

Ao criar o modelo algorítmico no Audience Manager, obviamente queremos que o modelo seja o mais eficaz possível. Como o modelo está considerando todas as características das quais os membros de sua característica/segmento base fazem parte, ele não ajuda o modelo se TODAS as pessoas estiverem em uma característica/segmento. Portanto, se você tiver características supergenéricas (como todos que foram ao seu site, ou todos os que receberam qualquer anúncio de você, etc.), verifique se a fonte de dados à qual elas pertencem NÃO está incluída nas fontes de dados do seu modelo. No caso de uso deste artigo, é improvável que você faça isso, pois estamos focando em dados de terceiros para nossos novos aliques, mas vale a pena mencionar de qualquer forma, e nos aplica a TODOS os seus modelos algorítmicos.

## Criar um [!UICONTROL Algorithmic Trait] {#creating-an-algorithmic-trait}

Em seguida, será necessário criar um  [!UICONTROL Algorithmic Trait], para que os resultados do modelo possam ser usados. Sem criar uma característica, o modelo é inútil. Assim, depois que o modelo for executado, certifique-se de entrar na caixa de diálogo de características e criar um [!UICONTROL Algorithmic Trait]. O vídeo a seguir apresenta o vídeo e mostra algumas dicas.

>[!VIDEO](https://video.tv.adobe.com/v/25191/?quality=12)

## Criar um segmento a partir dos dados do modelo e enviá-lo para o DSP {#creating-a-segment-from-the-model-data-and-sending-it-to-dsps}

Depois de criar uma [!UICONTROL Algorithmic Trait], é possível criar um novo segmento para inseri-lo, de modo que você possa ativar os dados (não é possível ativar uma característica, mas criar um novo segmento de uma característica com a variável [!UICONTROL Algorithmic Trait] nela, para que você possa ativar (usar) o segmento).

Depois de criar um segmento com base nessa característica algorítmica, você terá um público-alvo de clientes potenciais que se parecerão com pessoas que já se converteram em seu site. Agora você pode mapear esse segmento para qualquer destino de DSP no Audience Manager. Você poderá direcionar seu marketing para os sósias, que têm mais probabilidade de conversão em seu site do que apenas o público normal, aumentando seu retorno sobre o gasto com anúncio.
