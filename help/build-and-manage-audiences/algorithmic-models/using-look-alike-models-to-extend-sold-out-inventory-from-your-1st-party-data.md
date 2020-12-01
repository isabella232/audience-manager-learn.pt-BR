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


# Usando Aparência [!UICONTROL Models] para estender o inventário vendido para fora de seus [!UICONTROL First Party] dados {#using-look-alike-models-to-extend-sold-out-inventory-from-your-st-party-data}

Neste tutorial, nós percorreremos as etapas que você deve seguir para configurar e usar o Look-Alike [!UICONTROL Models], para que você possa criar novas audiências semelhantes e vendê-las como uma extensão para sua conversão [!UICONTROL segment].

## Detalhes do caso de uso {#use-case-details}

Você é um editor de conteúdo. Se você já esgotou o inventário dos conversores do site, talvez ache que sua oportunidade acaba lá. Digite a aparência aproximada do AAM [!UICONTROL Models]. Ao usar esse recurso, você pode estender ainda mais o inventário esgotado e também vender audiências de pessoas que talvez ainda não se converteram, mas que parecem/agem como pessoas que se converteram. Essa audiência [!UICONTROL segment] normalmente venderia por menos do que os conversores reais, mas, mesmo assim, permite que você adicione ao resultado final fornecendo uma opção de audiência adicional para anunciantes que desejam colocar anúncios em seu site. O benefício adicional desse caso de uso é que não custa nada executar esse modelo nos dados primários.

As etapas neste tutorial serão as seguintes:

1. Identifique/Crie um usuário ideal (conversão) [!UICONTROL trait] ou [!UICONTROL segment]
1. Criar um [!UICONTROL model] usando essa conversão [!UICONTROL trait]/[!UICONTROL segment] como item base
1. Escolha [!UICONTROL First party] fonte(s) de dados em [!UICONTROL model] e execute [!UICONTROL model]
1. Crie um algoritmo [!UICONTROL Trait] a partir dos resultados [!UICONTROL model] e adicione o [!UICONTROL trait] a um [!UICONTROL segment]
1. Oferta [!UICONTROL segment] aos anunciantes interessados para estender as vendas de conversão [!UICONTROL segment]

## Identifique/Crie um usuário ideal (conversão) [!UICONTROL trait] ou [!UICONTROL segment] {#identify-create-an-ideal-user-conversion-trait-or-segment}

O que você está tentando fazer com que as pessoas façam em seu site? Qual é o seu evento de conversão? É claro que há muitas respostas diferentes para essa pergunta, dependendo do tipo/vertical do site e das metas organizacionais. Em qualquer caso, é comum em AAM criar um [!UICONTROL trait] para visitantes que atenderam a esses critérios.

Nesse caso de uso, isso já é considerado, pois você esgotou o inventário para pessoas que são convertidas. Entretanto, para a finalidade deste tutorial, é bom discuti-lo como referência para o restante do caso de uso.

Além disso, ao usar eventos para criar [!UICONTROL traits], há um grande ganho que você precisa ter em mente, para que você não colete mais usuários do que deveria no [!UICONTROL trait]. Assista ao vídeo a seguir para ver a grande revelação. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**NOTA:** no vídeo acima, o exemplo que eu mostro presume que você tenha o Adobe Analytics. Obviamente, pode não ser esse o caso. Se você tiver Google Analytics (GA), nós teremos um módulo que você pode usar para enviar dados para AAM (consulte a [documentação](https://marketing.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html)), e se sua atividade de conversão em seu site for enviada para AAM pelo GA, você poderá criar sua característica de conversão a partir daí. Se você tiver uma solução de análise diferente (ou nenhuma solução de análise), ainda poderá enviar dados para AAM por meio de nosso código de DIL e da função `submit`, etc. (consulte a [documentação](https://marketing.adobe.com/resources/help/en_US/aam/c_dil.html)). Em seguida, crie novamente a característica de conversão com base nos dados enviados quando a atividade de conversão for executada no site.

## Criando uma aparência semelhante [!UICONTROL Model] a partir de [!UICONTROL First Party] Dados {#creating-a-look-alike-model-from-first-party-data}

Nesta etapa, criaremos uma [!UICONTROL First Party] aparência semelhante a [!UICONTROL Model]. Isso significa que não apenas usaremos uma [!UICONTROL first party] conversão [!UICONTROL trait]/[!UICONTROL segment] para nossa base [!UICONTROL trait]/[!UICONTROL segment] (isso seria normal para a maioria dos [!UICONTROL models] de qualquer forma), mas também só estaremos pesquisando o pool de dados [!UICONTROL first party] para mais pessoas que se parecem com os conversores. Não vamos analisar os dados [!UICONTROL second party] ou [!UICONTROL third party].

Nesse caso de uso, isso é importante, pois estamos tentando criar um [!UICONTROL segment] de usuários em nosso site que se parecem com conversores mas ainda não foram convertidos, para que possamos vender essa aparência [!UICONTROL segment] para anunciantes interessados.

>[!VIDEO](https://video.tv.adobe.com/v/23504/?quality-12)

## Criando um algoritmo [!UICONTROL Trait] {#creating-an-algorithmic-trait}

Em seguida, será necessário criar um algorítmico [!UICONTROL Trait] para que os resultados do [!UICONTROL model] possam ser usados. Sem criar um [!UICONTROL trait], o [!UICONTROL model] é inútil. Assim, depois que [!UICONTROL model] for executado, certifique-se de acessar a caixa de diálogo [!UICONTROL trait] e criar um algorítmico [!UICONTROL Trait]. O vídeo a seguir mostra algumas dicas.

>[!VIDEO](https://video.tv.adobe.com/v/23523/?quality=12)

## Oferecendo algorítmico [!UICONTROL Segment] aos anunciantes {#offering-the-algorithmic-segment-to-advertisers}

Depois de criar um algorítmico [!UICONTROL Trait], você pode criar um novo [!UICONTROL segment] para colocá-lo em, para que você possa ativar os dados (não é possível ativar um [!UICONTROL trait], mas criar um novo [!UICONTROL trait] [!UICONTROL segment] com o algorítmico [!UICONTROL Trait] nele, para que você possa ativar (usar) o [!UICONTROL segment].

Depois que você criar um [!UICONTROL segment] de [!UICONTROL first party] visitantes com pontuação mais alta na aparência [!UICONTROL model] (isto é, que parecem conversores mas ainda não foram convertidos), poderá oferta esse [!UICONTROL segment] para anunciantes no seu site, mesmo depois de ter esgotado todo o seu inventário de conversores reais no seu site. Essa é uma excelente maneira de estender essa audiência e continuar a ver a receita adicional usando o Look-Alike [!UICONTROL Models] no Audience Manager.
