---
title: Uso de modelos semelhantes para estender o inventário vendido para fora dos seus dados primários
description: Neste tutorial, iremos percorrer as etapas que você deve seguir para configurar e usar os Modelos semelhantes, para que você possa criar novas audiências semelhantes e vendê-las como uma extensão para seu segmento de conversão.
feature: algorithmic models
topics: null
audience: all
activity: use
doc-type: feature video
team: Technical Marketing
kt: 1688
translation-type: tm+mt
source-git-commit: dfd549508cc223714bdb07ac6fd2aa31e6ca5586
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---


# Como usar o recurso Aparência [!UICONTROL Models] para estender o inventário vendido para fora dos seus [!UICONTROL First Party] dados {#using-look-alike-models-to-extend-sold-out-inventory-from-your-st-party-data}

Neste tutorial, nós percorreremos as etapas que você deve seguir para configurar e usar a aparência semelhante [!UICONTROL Models], para que você possa criar novas audiências semelhantes e vendê-las como uma extensão para sua conversão [!UICONTROL segment].

## Detalhes do caso de uso {#use-case-details}

Você é um editor de conteúdo. Se você já esgotou o inventário dos conversores do site, talvez ache que sua oportunidade acaba lá. Digite a aparência do AAM [!UICONTROL Models]. Ao usar esse recurso, você pode estender ainda mais o inventário esgotado e também vender audiências de pessoas que talvez ainda não se converteram, mas que parecem/agem como pessoas que se converteram. Normalmente, essa audiência [!UICONTROL segment] venderia por menos do que os conversores reais, mas, mesmo assim, permite que você adicione ao resultado final fornecendo uma opção de audiência adicional para anunciantes que desejam colocar anúncios em seu site. O benefício adicional desse caso de uso é que não custa nada executar esse modelo nos dados primários.

As etapas neste tutorial serão as seguintes:

1. Identifique/crie um usuário ideal (conversão) [!UICONTROL trait] ou [!UICONTROL segment]
1. Criar um [!UICONTROL model] usando esta conversão [!UICONTROL trait]/[!UICONTROL segment] como item base
1. Escolha [!UICONTROL First party] as fontes de dados no [!UICONTROL model] e execute o [!UICONTROL model]
1. Crie um Algoritmo a partir [!UICONTROL Trait] dos [!UICONTROL model] resultados e adicione o [!UICONTROL trait] a um [!UICONTROL segment]
1. Oferta os anunciantes interessados [!UICONTROL segment] para estender as vendas de conversão [!UICONTROL segment]

## Identifique/crie um usuário ideal (conversão) [!UICONTROL trait] ou [!UICONTROL segment] {#identify-create-an-ideal-user-conversion-trait-or-segment}

O que você está tentando fazer com que as pessoas façam em seu site? Qual é o seu evento de conversão? É claro que há muitas respostas diferentes para essa pergunta, dependendo do tipo/vertical do site e das metas organizacionais. Em todo o caso, é comum em AAM criar um sistema [!UICONTROL trait] para visitantes que tenham cumprido esses critérios.

Nesse caso de uso, isso já é considerado, pois você esgotou o inventário para pessoas que são convertidas. Entretanto, para a finalidade deste tutorial, é bom discuti-lo como referência para o restante do caso de uso.

Além disso, ao usar eventos para criar [!UICONTROL traits], há uma grande armadilha que você precisa ter em mente, para que você não colete mais usuários do que deveria no [!UICONTROL trait]. Assista ao vídeo a seguir para ver a grande revelação. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**NOTA:** No vídeo acima, o exemplo que eu mostro presume que você tem Adobe Analytics. Obviamente, pode não ser esse o caso. Se você tiver Google Analytics (GA), nós teremos um módulo que você pode usar para enviar dados para AAM (consulte a [documentação](https://marketing.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html)), e se sua atividade de conversão em seu site for enviada para AAM pelo GA, você poderá criar sua característica de conversão a partir disso. Se você tiver uma solução de análise diferente (ou nenhuma solução de análise), ainda poderá enviar dados para AAM por meio do código de DIL e da `submit` função, etc. (consulte a [documentação](https://marketing.adobe.com/resources/help/en_US/aam/c_dil.html)). Em seguida, crie novamente a característica de conversão com base nos dados enviados quando a atividade de conversão for executada no site.

## Criação de uma aparência semelhante [!UICONTROL Model] a partir de [!UICONTROL First Party] dados {#creating-a-look-alike-model-from-first-party-data}

Neste passo, vamos criar uma [!UICONTROL First Party] Aparência [!UICONTROL Model]. Isso significa que não apenas usaremos uma [!UICONTROL first party] conversão [!UICONTROL trait]/[!UICONTROL segment] para nossa base [!UICONTROL trait]/[!UICONTROL segment] (isso seria normal para a maioria das pessoas de qualquer forma [!UICONTROL models] ), mas também apenas pesquisaremos o pool de [!UICONTROL first party] dados para mais pessoas que se parecem com os conversores. Não vamos olhar para [!UICONTROL second party] os nossos [!UICONTROL third party] dados.

Neste caso de uso, isso é importante, porque estamos tentando criar um grupo [!UICONTROL segment] de usuários em nosso site que se parecem com conversores mas que ainda não foram convertidos, para que possamos vender essa aparência [!UICONTROL segment] para anunciantes interessados.

>[!VIDEO](https://video.tv.adobe.com/v/23504/?quality-12)

## Criação de um algoritmo [!UICONTROL Trait] {#creating-an-algorithmic-trait}

Em seguida, será necessário criar um Algoritmo [!UICONTROL Trait], para que os resultados do [!UICONTROL model] processo possam ser usados. Sem criar um [!UICONTROL trait], o [!UICONTROL model] é inútil. Então depois que o [!UICONTROL model] jogo for executado, certifique-se de entrar no [!UICONTROL trait] diálogo e criar um Algorítmico [!UICONTROL Trait]. O vídeo a seguir mostra algumas dicas.

>[!VIDEO](https://video.tv.adobe.com/v/23523/?quality=12)

## Oferecendo algorítmica [!UICONTROL Segment] aos anunciantes {#offering-the-algorithmic-segment-to-advertisers}

Depois de criar um Algoritmo [!UICONTROL Trait], você pode criar um novo [!UICONTROL segment] para colocá-lo no, para que possa ativar os dados (não é possível ativar um [!UICONTROL trait], mas sim criar um novo[!UICONTROL trait] com o Algoritmo [!UICONTROL segment] nele, para que você possa ativar (usar) o [!UICONTROL Trait] [!UICONTROL segment].

Depois de criar um conjunto [!UICONTROL segment] de [!UICONTROL first party] visitantes com pontuação alta na aparência [!UICONTROL model] (isto é, que parecem conversores mas ainda não foram convertidos), você pode oferta isso [!UICONTROL segment] para anunciantes em seu site, mesmo depois de ter esgotado todo o seu inventário de conversores reais em seu site. Esta é uma ótima maneira de estender essa audiência e continuar a ver mais receita usando o recurso Aparência [!UICONTROL Models] no Audience Manager.
