---
title: Aumente o ROAS usando modelos algorítmicos (semelhantes) no Audience Manager
description: O poder real da modelagem semelhante à Audience Manager é que você busca expandir sua audiência de referência em relação a um conjunto novo de usuários de qualidade de fontes de dados de terceiros e fontes de dados de terceiros. Neste tutorial, aprenda as etapas para criar um modelo a partir desses dados.
feature: modelos algorítmicos
topics: null
audience: all
activity: use
doc-type: feature video
team: Technical Marketing
thumbnail: 25188.jpg
kt: 1849
translation-type: tm+mt
source-git-commit: 6c81fd73d2c5abd646b0d38b6f4eebde837b09f2
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 0%

---


# Aumente o ROAS usando algorítmico (semelhante) [!UICONTROL Models] em Audience Manager {#increase-roas-by-using-algorithmic-look-alike-models-in-audience-manager}

O poder real da aparência semelhante ao Audience Manager [!UICONTROL Modeling] vem quando você procura expandir sua audiência de linha de base em relação a um conjunto de usuários novo e de qualidade de [!UICONTROL second party] e [!UICONTROL third party] [!UICONTROL data sources]. Neste tutorial, aprenda as etapas necessárias para criar um [!UICONTROL model] a partir desses dados.

## Habilitar [!UICONTROL Second Party] ou [!UICONTROL Third Party] Fluxos de dados do Audience Marketplace {#enable-2nd-or-3rd-party-data-streams-from-the-audience-marketplace}

Para usar os dados [!UICONTROL second party] e [!UICONTROL third party] em uma aparência semelhante [!UICONTROL model], primeiro temos que ativar esses dados na interface do Audience Manager. Adobe tem um grande número de provedores de dados [!UICONTROL second party] e [!UICONTROL third party] dos quais você pode escolher. Eles estão disponíveis para você em uma interface de autoatendimento em AAM, via Audience Marketplace. Navegue até o Audience Marketplace e navegue pelas possibilidades. O vídeo a seguir mostrará como fazer isso, incluindo como ativar fluxos gratuitos de &quot;tentar antes de comprar&quot;, para que você possa se bloquear nos dados que serão mais úteis para a sua organização antes de confirmar o preço do provedor de dados.

Além disso, para ajudá-lo a pesquisar e decidir em qual provedor de dados usar, um grande recurso é [[!DNL Adobe Audience Finder]](https://www.adobe-audience-finder.com/).

>[!VIDEO](https://video.tv.adobe.com/v/25188/?quality=12)

## Identifique/Crie um usuário ideal (conversão) [!UICONTROL trait] ou [!UICONTROL segment] {#identify-create-an-ideal-user-conversion-trait-or-segment}

O que você está tentando fazer com que as pessoas façam em seu site? Qual é o seu evento de conversão? É claro que há muitas respostas diferentes para essa pergunta, dependendo do tipo/vertical do site e das metas organizacionais. Em qualquer caso, é comum em AAM criar um [!UICONTROL trait] para visitantes que atenderam a esses critérios.

No vídeo abaixo, mostrarei como criar uma conversão [!UICONTROL trait], que você desejará ter em vigor à medida que você continuar neste tutorial e criar uma aparência semelhante [!UICONTROL model].

Além disso, ao usar eventos Adobe Analytics para criar [!UICONTROL traits], há uma grande armadilha que você precisa ter em mente, para que você não colete mais usuários do que deveria no [!UICONTROL trait]. Assista ao vídeo a seguir para ver a grande revelação. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**NOTA:** no vídeo acima, o exemplo que eu mostro presume que você tenha o Adobe Analytics. Obviamente, pode não ser esse o caso. Se você tiver Google Analytics (GA), temos um módulo que pode ser usado para enviar dados para AAM (consulte a [documentação](https://marketing.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html)), e se sua atividade de conversão no seu site for enviada para AAM pelo GA, você poderá criar sua conversão [!UICONTROL trait] a partir disso. Se você tiver uma solução de análise diferente (ou nenhuma solução de análise), ainda poderá enviar dados para AAM por meio de nosso código de DIL e da função `submit`, etc. (consulte a [documentação](https://marketing.adobe.com/resources/help/en_US/aam/c_dil.html)). Em seguida, crie a conversão [!UICONTROL trait] com base nos dados enviados quando a atividade de conversão for executada no site.

## Crie uma aparência semelhante [!UICONTROL Model] a partir de [!UICONTROL Second Party] ou [!UICONTROL Third Party] Dados {#create-a-look-alike-model-from-2nd-or-3rd-party-data}

Depois de concluir as etapas acima, estamos prontos para criar um algoritmo (sósia) [!UICONTROL Model]. À medida que configuramos o [!UICONTROL model], usaremos a conversão [!UICONTROL trait] como nossa base [!UICONTROL trait] (visitantes-chave que queremos duplicado), e usaremos o fluxo de dados [!UICONTROL third party] habilitado como nosso pool de pessoas para extrair.

>[!VIDEO](https://video.tv.adobe.com/v/25190/?quality-12)

## Uma Prática Recomendada Importante {#an-important-best-practice}

Ao criar o algoritmo [!UICONTROL model] no Audience Manager, obviamente queremos que [!UICONTROL model] seja o mais eficaz possível. Como o [!UICONTROL model] está considerando todos os [!UICONTROL traits] membros da sua base [!UICONTROL trait]/[!UICONTROL segment] fazem parte do, isso não ajuda o [!UICONTROL model] se TODAS as pessoas estiverem em um [!UICONTROL trait]/[!UICONTROL segment]. Portanto, se você tiver um [!UICONTROL traits] super genérico (como todos os que foram ao seu site, ou todos os que receberam qualquer anúncio seu, etc.), certifique-se de que o [!UICONTROL data source] ao qual eles pertencem NÃO esteja incluído no [!UICONTROL data sources] em seu [!UICONTROL model]. No caso de uso deste artigo, não é provável que você o faça, pois estamos focados nos dados [!UICONTROL third party] para nossos novos sósias, mas vale a pena mencionar de qualquer forma, e se aplica a TODOS os algoritmos [!UICONTROL models].

## Criando um algoritmo [!UICONTROL Trait] {#creating-an-algorithmic-trait}

Em seguida, será necessário criar um algorítmico [!UICONTROL Trait] para que os resultados de [!UICONTROL model] possam ser usados. Sem criar um [!UICONTROL trait], o modelo é inútil. Assim, depois que [!UICONTROL model] for executado, certifique-se de acessar a caixa de diálogo [!UICONTROL trait] e criar um algorítmico [!UICONTROL Trait]. O vídeo a seguir mostra algumas dicas.

>[!VIDEO](https://video.tv.adobe.com/v/25191/?quality=12)

## Criar um [!UICONTROL Segment] a partir dos [!UICONTROL Model] Dados e enviá-los para DSP {#creating-a-segment-from-the-model-data-and-sending-it-to-dsps}

Depois de criar um algorítmico [!UICONTROL Trait], você pode criar um novo [!UICONTROL segment] para colocá-lo em, para que você possa ativar os dados (não é possível ativar um [!UICONTROL trait], mas criar um novo [!UICONTROL trait] [!UICONTROL segment] com o algorítmico [!UICONTROL Trait] nele, para que você possa ativar (usar) o [!UICONTROL segment]).

Depois de criar um [!UICONTROL segment] a partir deste algorítmico [!UICONTROL trait], você terá uma audiência de clientes potenciais que se parecem com pessoas que já converteram em seu site. Agora você pode mapear [!UICONTROL segment] para qualquer DSP [!UICONTROL destinations] no Audience Manager. Você poderá público alvo seu marketing para esses sósias, que têm maior probabilidade de serem convertidos em seu site do que apenas o público normal, aumentando seu Retorno da despesa de publicidade. Boa sorte!
