---
title: Use modelos semelhantes para estender o inventário esgotado de dados primários
description: Neste tutorial, abordamos as etapas que você deve seguir para configurar e usar modelos semelhantes, para que você possa criar novos públicos-alvo semelhantes e vendê-los como uma extensão para seu segmento de conversão.
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
source-git-commit: 2094d3bcf658913171afa848e4228653c71c41de
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# Use modelos semelhantes para estender o inventário esgotado de dados primários {#using-look-alike-models-to-extend-sold-out-inventory-from-your-st-party-data}

Neste tutorial, vamos seguir as etapas que você deve seguir para configurar e usar a aparência [!UICONTROL Models], para que você possa criar novos públicos-alvo semelhantes e vendê-los como uma extensão do seu segmento de conversão.

## Detalhes do caso de uso {#use-case-details}

Você é um editor de conteúdo. Se você já esgotou o inventário dos conversores do site, talvez ache que sua oportunidade termina lá. Digite a aparência do AAM [!UICONTROL Models]. Ao usar esse recurso, você pode estender ainda mais o inventário esgotado e também vender públicos-alvo de pessoas que talvez ainda não tenham se convertido, mas que parecem/atuam como pessoas que se converteram. Esse segmento de público-alvo normalmente seria vendido por menos do que os conversores reais, mas no entanto permite que você adicione o resultado fornecendo uma opção de público-alvo adicional para anunciantes que desejam colocar anúncios em seu site. O benefício adicional desse caso de uso é que não custa nada executar esse modelo em seus dados primários.

As etapas neste tutorial serão as seguintes:

1. Identificar/criar uma característica ou segmento ideal do usuário (conversão)
1. Criar um modelo usando esta característica/segmento de conversão como o item base
1. Choose [!UICONTROL First party] fonte(s) de dados no modelo e execute o modelo
1. Crie um [!UICONTROL Algorithmic Trait] dos resultados do modelo e adicionar a característica a um segmento
1. Ofereça o segmento aos anunciantes interessados para estender as vendas do segmento de conversão

## Identificar ou criar uma característica ou segmento ideal do usuário (conversão) {#identify-create-an-ideal-user-conversion-trait-or-segment}

O que você está tentando fazer com que as pessoas façam em seu site? Qual é o seu evento de conversão? É claro que há muitas respostas diferentes para essa pergunta, dependendo do tipo/vertical do site e das metas organizacionais. Em qualquer caso, é comum AAM criar uma característica para visitantes que atenderam a esses critérios.

Nesse caso de uso, isso já é considerado, pois você esgotou o inventário para pessoas que são conversores. No entanto, para a finalidade deste tutorial, é bom discuti-lo como referência para o resto do caso de uso.

Além disso, ao usar eventos para criar características, há um grande gotcha que você precisa ter em mente, para que não colete mais usuários do que deveria na característica. Assista ao vídeo a seguir para a grande revelação. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**OBSERVAÇÃO:** No vídeo acima, o exemplo que mostro assume que você tem o Adobe Analytics. Obviamente, pode não ser esse o caso. Se você tiver o Google Analytics (GA), temos um módulo que pode ser usado para enviar dados para o AAM (consulte o [documentação](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html)) e se sua atividade de conversão no seu site for enviada para AAM por GA, você poderá criar sua característica de conversão a partir disso. Se você tiver uma solução de análise diferente (ou nenhuma solução de análise), ainda poderá enviar dados para o AAM por meio do nosso código de DIL e do `submit` , etc. (consulte o [documentação](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-modules.html)). Em seguida, crie novamente a característica de conversão com base nos dados enviados quando a atividade de conversão for executada no site.

## Criar um modelo semelhante a partir de dados primários {#creating-a-look-alike-model-from-first-party-data}

Nesta etapa, vamos criar um [!UICONTROL First Party] Modelo semelhante. Isso significa que não apenas usaremos uma característica/segmento de conversão primário para nossa característica/segmento base (isso seria normal para a maioria dos modelos de qualquer maneira), como também analisaremos apenas o pool de dados primários para mais pessoas que se parecem com os conversores. Não analisaremos dados secundários ou de terceiros.

Nesse caso de uso, isso é importante, pois estamos tentando criar um segmento de usuários em nosso site que parecem conversores, mas ainda não foram convertidos, para que possamos vender esse segmento de semelhança para anunciantes interessados.

>[!VIDEO](https://video.tv.adobe.com/v/23504/?quality-12)

## Criar uma característica algorítmica {#creating-an-algorithmic-trait}

Em seguida, será necessário criar um [!UICONTROL Algorithmic Trait], para que os resultados do modelo possam ser usados. Sem criar uma característica, o modelo é inútil. Assim, depois que o modelo for executado, certifique-se de entrar na caixa de diálogo de características e criar um [!UICONTROL Algorithmic Trait]. O vídeo a seguir mostra algumas dicas.

>[!VIDEO](https://video.tv.adobe.com/v/23523/?quality=12)

## Ofereça o [!UICONTROL Algorithmic Segment] aos anunciantes {#offering-the-algorithmic-segment-to-advertisers}

Depois de criar uma [!UICONTROL Algorithmic Trait], é possível criar um novo segmento para inseri-lo, de modo que você possa ativar os dados (não é possível ativar uma característica, mas criar um novo segmento de uma característica com a variável [!UICONTROL Algorithmic Trait] nela, para que você possa ativar (usar) o segmento.

Depois de criar um segmento de visitantes primários que tiveram pontuação alta no modelo de semelhança (ou seja, que parecem conversores, mas ainda não fizeram a conversão), você pode oferecer esse segmento aos anunciantes em seu site, mesmo depois de ter esgotado todo o inventário de conversores reais em seu site. Essa é uma ótima maneira de estender esse público-alvo e continuar a ver receita adicional usando a aparência [!UICONTROL Models] em Audience Manager.
