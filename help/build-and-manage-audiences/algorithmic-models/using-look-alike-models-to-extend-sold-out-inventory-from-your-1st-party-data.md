---
title: Uso de modelos semelhantes para estender o inventário vendido dos dados primários
description: Neste tutorial, vamos analisar as etapas que você deve seguir para configurar e usar Modelos semelhantes, para que você possa criar novos públicos semelhantes e vendê-los como uma extensão para seu segmento de conversão.
feature: Algorithmic Models
topics: null
activity: use
doc-type: feature video
team: Technical Marketing
thumbnail: 23523.jpg
kt: 1688
role: User, Developer, Data Engineer, Architect, Data Architect, Admin, Leader
level: Intermediate
exl-id: 6820528e-3211-4a1d-be05-50f1292179d2
source-git-commit: 4d4c12e9f9a33760a89460258c3802fcf3a4e22b
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 0%

---

# Usar a aparência [!UICONTROL Models] para estender o inventário vendido dos dados [!UICONTROL First Party] {#using-look-alike-models-to-extend-sold-out-inventory-from-your-st-party-data}

Neste tutorial, vamos percorrer as etapas que você deve seguir para configurar e usar a Aparência [!UICONTROL Models], para que você possa criar novos públicos-alvo semelhantes e vendê-los como uma extensão para sua conversão [!UICONTROL segment].

## Detalhes do caso de uso {#use-case-details}

Você é um editor de conteúdo. Se você já esgotou o inventário dos conversores do site, talvez ache que sua oportunidade termina lá. Digite a aparência de AAM [!UICONTROL Models]. Ao usar esse recurso, você pode estender ainda mais o inventário esgotado e também vender públicos-alvo de pessoas que talvez ainda não tenham se convertido, mas que parecem/atuam como pessoas que se converteram. Esse público-alvo [!UICONTROL segment] normalmente seria vendido por menos do que os conversores reais, mas no entanto permite que você adicione o resultado fornecendo uma opção de público-alvo adicional para anunciantes que desejam colocar anúncios em seu site. O benefício adicional desse caso de uso é que não custa nada executar esse modelo em seus dados primários.

As etapas neste tutorial serão as seguintes:

1. Identificar/criar um usuário ideal (conversão) [!UICONTROL trait] ou [!UICONTROL segment]
1. Crie um [!UICONTROL model] usando essa conversão [!UICONTROL trait]/[!UICONTROL segment] como o item base
1. Escolha [!UICONTROL First party] fonte(s) de dados no [!UICONTROL model] e execute o [!UICONTROL model]
1. Crie um Algoritmo [!UICONTROL Trait] a partir dos resultados [!UICONTROL model] e adicione [!UICONTROL trait] a [!UICONTROL segment]
1. Ofereça o [!UICONTROL segment] aos anunciantes interessados para estender a conversão [!UICONTROL segment] de vendas

## Identificar/criar um usuário ideal (conversão) [!UICONTROL trait] ou [!UICONTROL segment] {#identify-create-an-ideal-user-conversion-trait-or-segment}

O que você está tentando fazer com que as pessoas façam em seu site? Qual é o seu evento de conversão? É claro que há muitas respostas diferentes para essa pergunta, dependendo do tipo/vertical do site e das metas organizacionais. Em qualquer caso, é comum AAM criar um [!UICONTROL trait] para visitantes que atenderam a esses critérios.

Nesse caso de uso, isso já é considerado, pois você esgotou o inventário para pessoas que são conversores. No entanto, para a finalidade deste tutorial, é bom discuti-lo como referência para o resto do caso de uso.

Além disso, ao usar eventos para criar [!UICONTROL traits], há um gotcha importante que você precisa ter em mente, para que não colete mais usuários do que deveria no [!UICONTROL trait]. Assista ao vídeo a seguir para a grande revelação. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**OBSERVAÇÃO:** no vídeo acima, o exemplo que mostro assume que você tem Adobe Analytics. Obviamente, pode não ser esse o caso. Se você tiver o Google Analytics (GA), temos um módulo que pode ser usado para enviar dados para o AAM (consulte a [documentação](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html)), e se sua atividade de conversão no seu site for enviada para AAM por GA, você poderá criar sua característica de conversão a partir daí. Se você tiver uma solução de análise diferente (ou nenhuma solução de análise), ainda poderá enviar dados para o AAM por meio do nosso código DIL e da função `submit`, etc. (consulte a [documentação](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-modules.html)). Em seguida, crie novamente a característica de conversão com base nos dados enviados quando a atividade de conversão for executada no site.

## Criando uma aparência semelhante [!UICONTROL Model] a partir de [!UICONTROL First Party] dados {#creating-a-look-alike-model-from-first-party-data}

Nesta etapa, vamos criar um [!UICONTROL First Party] Semelhante a [!UICONTROL Model]. Isso significa que não apenas usaremos uma [!UICONTROL first party] conversão [!UICONTROL trait]/[!UICONTROL segment] para nossa base [!UICONTROL trait]/[!UICONTROL segment] (isso seria normal para a maioria dos [!UICONTROL models] de qualquer forma), mas também só estaremos pesquisando o pool de dados [!UICONTROL first party] para mais pessoas que se parecem com os conversores. Não analisaremos os dados [!UICONTROL second party] ou [!UICONTROL third party].

Nesse caso de uso, isso é importante, pois estamos tentando criar um [!UICONTROL segment] de usuários em nosso site que parecem conversores, mas ainda não foram convertidos, para que possamos vender essa semelhança [!UICONTROL segment] para anunciantes interessados.

>[!VIDEO](https://video.tv.adobe.com/v/23504/?quality-12)

## Criação de um algoritmo [!UICONTROL Trait] {#creating-an-algorithmic-trait}

Em seguida, precisaremos criar um algorítmico [!UICONTROL Trait], para que os resultados do [!UICONTROL model] possam ser usados. Sem criar um [!UICONTROL trait], o [!UICONTROL model] é inútil. Assim, depois que o [!UICONTROL model] for executado, acesse a caixa de diálogo [!UICONTROL trait] e crie um Algorítmico [!UICONTROL Trait]. O vídeo a seguir mostra algumas dicas.

>[!VIDEO](https://video.tv.adobe.com/v/23523/?quality=12)

## Oferecer o algoritmo [!UICONTROL Segment] aos anunciantes {#offering-the-algorithmic-segment-to-advertisers}

Depois de criar um Algorítmico [!UICONTROL Trait], você pode criar um novo [!UICONTROL segment] para inseri-lo, para que possa ativar os dados (não é possível ativar um [!UICONTROL trait], mas criar um novo [!UICONTROL trait] [!UICONTROL segment] com o Algorítmico [!UICONTROL Trait] nele, para que você possa ativar (usar) o [!UICONTROL segment].

Depois de criar um [!UICONTROL segment] de [!UICONTROL first party] visitantes com pontuação alta na aparência [!UICONTROL model] (ou seja, que parecem conversores, mas ainda não fizeram a conversão), você pode oferecer esse [!UICONTROL segment] aos anunciantes do site, mesmo após ter esgotado todo o inventário de conversores reais do site. Essa é uma ótima maneira de estender esse público-alvo e continuar a ver receita adicional usando a aparência [!UICONTROL Models] no Audience Manager.
