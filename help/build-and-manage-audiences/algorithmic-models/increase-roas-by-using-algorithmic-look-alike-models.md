---
title: Aumente o ROAS usando modelos algorítmicos (semelhantes) no Audience Manager
description: O poder real da Modelagem de semelhança do Audience Manager vem quando você procura expandir seu público-alvo básico em relação a uma qualidade, um novo conjunto de usuários de fontes de dados de terceiros e de segunda geração. Neste tutorial, aprenda as etapas para criar um modelo a partir desses dados.
feature: Algorithmic Models
topics: null
activity: use
doc-type: feature video
team: Technical Marketing
thumbnail: 25188.jpg
kt: 1849
role: "Business Practitioner, Developer, Data Engineer, Architect, Data Architect, Administrator, Leader"
level: Intermediate
translation-type: tm+mt
source-git-commit: a7dc335e75697a7b1720eccdadbb9605fdeda798
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---


# Aumente o ROAS usando algorítmico (semelhante) [!UICONTROL Models] no Audience Manager {#increase-roas-by-using-algorithmic-look-alike-models-in-audience-manager}

O poder real da semelhança do Audience Manager [!UICONTROL Modeling] vem quando você procura expandir seu público-alvo básico contra uma qualidade, um novo conjunto de usuários de [!UICONTROL second party] e [!UICONTROL third party] [!UICONTROL data sources]. Neste tutorial, aprenda as etapas necessárias para criar um [!UICONTROL model] a partir desses dados.

## Habilite [!UICONTROL Second Party] ou [!UICONTROL Third Party] Fluxos de dados do Audience Marketplace {#enable-2nd-or-3rd-party-data-streams-from-the-audience-marketplace}

Para usar os dados [!UICONTROL second party] e [!UICONTROL third party] em uma aparência [!UICONTROL model], primeiro precisamos habilitar esses dados na interface do Audience Manager. A Adobe tem um grande número de provedores de dados [!UICONTROL second party] e [!UICONTROL third party] a partir dos quais você pode escolher. Eles estão disponíveis para você em uma interface de autoatendimento no AAM, por meio do Audience Marketplace. Navegue até o Audience Marketplace e navegue pelas possibilidades. O vídeo a seguir mostrará como fazer isso, incluindo como ativar fluxos gratuitos de &quot;tente antes de comprar&quot;, para que você possa se bloquear nos dados que serão mais úteis para sua organização antes de se comprometer com o preço do provedor de dados.

Além disso, para ajudá-lo a pesquisar e decidir qual provedor de dados usar, um grande recurso é o [[!DNL Adobe Audience Finder]](https://www.adobe-audience-finder.com/).

>[!VIDEO](https://video.tv.adobe.com/v/25188/?quality=12)

## Identifique/crie um usuário ideal (conversão) [!UICONTROL trait] ou [!UICONTROL segment] {#identify-create-an-ideal-user-conversion-trait-or-segment}

O que você está tentando fazer com que as pessoas façam em seu site? Qual é o seu evento de conversão? É claro que há muitas respostas diferentes para essa pergunta, dependendo do tipo/vertical do site e das metas organizacionais. Em qualquer caso, é comum no AAM criar um [!UICONTROL trait] para visitantes que atenderam a esses critérios.

No vídeo abaixo, mostrarei como criar uma conversão [!UICONTROL trait], que você desejará ter em vigor à medida que continuar neste tutorial e criar um [!UICONTROL model] semelhante.

Além disso, ao usar eventos do Adobe Analytics para criar [!UICONTROL traits], há um grande gotcha que você precisa ter em mente, para que não colete mais usuários do que deveria no [!UICONTROL trait]. Assista ao vídeo a seguir para a grande revelação. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**OBSERVAÇÃO:** no vídeo acima, o exemplo que mostro assume que você tem o Adobe Analytics. Obviamente, pode não ser esse o caso. Se você tiver o Google Analytics (GA), temos um módulo que pode ser usado para enviar dados para o AAM (consulte a [documentação](https://marketing.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html)), e se a atividade de conversão em seu site for enviada para o AAM pela GA, você poderá criar sua conversão [!UICONTROL trait] a partir daí. Se você tiver uma solução de análise diferente (ou nenhuma solução de análise), ainda poderá enviar dados para o AAM por meio de nosso código DIL e da função `submit`, etc. (consulte a [documentação](https://marketing.adobe.com/resources/help/en_US/aam/c_dil.html)). Em seguida, crie a conversão [!UICONTROL trait] com base nos dados enviados quando a atividade de conversão é executada no site.

## Crie uma semelhança [!UICONTROL Model] a partir de [!UICONTROL Second Party] ou [!UICONTROL Third Party] Dados {#create-a-look-alike-model-from-2nd-or-3rd-party-data}

Depois de concluir as etapas acima, agora estamos prontos para criar um Algorítmico (semelhança) [!UICONTROL Model]. À medida que configuramos o [!UICONTROL model], usaremos a conversão [!UICONTROL trait] como nossa base [!UICONTROL trait] (visitantes-chave que queremos duplicar) e usaremos o fluxo de dados [!UICONTROL third party] habilitado como nosso pool de pessoas para extrair.

>[!VIDEO](https://video.tv.adobe.com/v/25190/?quality-12)

## Uma Prática Recomendada Importante {#an-important-best-practice}

Ao criar o algoritmo [!UICONTROL model] no Audience Manager, obviamente queremos que [!UICONTROL model] seja o mais eficaz possível. Como o [!UICONTROL model] está considerando todos os [!UICONTROL traits] dos membros de sua base [!UICONTROL trait]/[!UICONTROL segment] fazem parte, isso não ajuda o [!UICONTROL model] se TODAS as pessoas estiverem em um [!UICONTROL trait]/[!UICONTROL segment]. Portanto, se você tiver um [!UICONTROL traits] super genérico (como todos que foram ao seu site, ou todos que receberam qualquer anúncio de você, etc.), verifique se o [!UICONTROL data source] ao qual ele pertence NÃO está incluído no [!UICONTROL data sources] em seu [!UICONTROL model]. No caso de uso deste artigo, é improvável que você faça isso, pois estamos nos concentrando em examinar os dados [!UICONTROL third party] para nossos novos aliques, mas vale a pena mencionar de qualquer forma, e nos aplica a TODOS os seus algoritmos [!UICONTROL models].

## Criação de um algoritmo [!UICONTROL Trait] {#creating-an-algorithmic-trait}

Em seguida, precisaremos criar um algorítmico [!UICONTROL Trait] para que os resultados do [!UICONTROL model] possam ser usados. Sem criar um [!UICONTROL trait], o modelo é inútil. Portanto, depois que o [!UICONTROL model] for executado, verifique se vai para a caixa de diálogo [!UICONTROL trait] e crie um Algorítmico [!UICONTROL Trait]. O vídeo a seguir apresenta o vídeo e mostra algumas dicas.

>[!VIDEO](https://video.tv.adobe.com/v/25191/?quality=12)

## Criação de um [!UICONTROL Segment] a partir dos dados [!UICONTROL Model] e seu envio para DSPs {#creating-a-segment-from-the-model-data-and-sending-it-to-dsps}

Depois de criar um Algorítmico [!UICONTROL Trait], você pode criar um novo [!UICONTROL segment] para inseri-lo, para que possa ativar os dados (não é possível ativar um [!UICONTROL trait], mas criar um novo [!UICONTROL trait] [!UICONTROL segment] com o Algorítmico [!UICONTROL Trait] nele, para que você possa ativar (usar) o [!UICONTROL segment]).

Depois de criar um [!UICONTROL segment] a partir deste [!UICONTROL trait] algorítmico, você terá um público-alvo de clientes potenciais que se pareçam com pessoas que já se converteram no seu site. Agora você pode mapear isso [!UICONTROL segment] para qualquer um de seus DSP [!UICONTROL destinations] no Audience Manager. Você poderá direcionar seu marketing para os sósias, que têm mais probabilidade de conversão em seu site do que apenas o público normal, aumentando seu retorno sobre o gasto com anúncio. Boa sorte!
