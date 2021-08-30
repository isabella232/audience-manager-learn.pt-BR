---
title: Suporte ao IAB TCF 2.0 no Audience Manager
description: O Adobe fornece o meio de gerenciar e comunicar as opções de privacidade de seus usuários por meio da funcionalidade de aceitação e pelo Plug-in do Audience Manager para o suporte à Estrutura de transparência e consentimento 2.0 (TCF 2.0) do IAB. Este artigo funciona junto com a documentação para ajudá-lo a entender o Plug-in do Audience Manager para a TCF do IAB e como ele funciona junto com o objeto Opt-in do Adobe e o Provedor de gerenciamento de consentimento (CMP).
feature: Data Governance & Privacy
activity: implement
doc-type: technical video
team: Technical Marketing
thumbnail: 26434.jpg
kt: 5027
role: Developer, Data Engineer, Architect
level: Experienced
exl-id: 04b4e786-0457-4dcc-bcf9-a79eda67bb2e
source-git-commit: 4d4c12e9f9a33760a89460258c3802fcf3a4e22b
workflow-type: tm+mt
source-wordcount: '1120'
ht-degree: 0%

---

# Suporte ao IAB TCF 2.0 no Audience Manager {#iab-tcf-support-in-audience-manager}

O Adobe fornece o meio de gerenciar e comunicar as opções de privacidade de seus usuários por meio da funcionalidade de aceitação e pelo Plug-in do Audience Manager para o suporte à Estrutura de transparência e consentimento 2.0 (TCF 2.0) do IAB. Este artigo funciona junto com a documentação para ajudá-lo a entender o Plug-in do Audience Manager para a TCF do IAB e como ele funciona junto com o objeto Opt-in do Adobe e o Provedor de gerenciamento de consentimento (CMP). Para saber mais sobre o IAB, consulte o site em [https://www.iabeurope.eu/](https://www.iabeurope.eu/).

## Primeira etapa: Entenda a aceitação da ECID {#first-step-understand-ecid-s-opt-in}

Para entender como trabalhar com a TCF do IAB, primeiro você deve entender a funcionalidade [!DNL Opt-in], que faz parte da biblioteca do Experience Cloud ID Service (ECID). Se não estiver familiarizado com o funcionamento do Opt-in, consulte [este artigo útil](https://experienceleague.adobe.com/docs/core-services-learn/tutorials/id-service/use-opt-in-to-control-experience-cloud-activities-based-on-user-consent.html) primeiro. Você também deve revisar a [documentação](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) do Opt-in. Depois de passar por esses recursos, volte para esta página e continue.

## O plug-in do Audience Manager para a TCF do IAB {#the-audience-manager-plug-in-for-iab-tcf}

Agora que você tem pelo menos uma compreensão básica de como o serviço de Opt-in funciona, o Audience Manager pode criar camadas nele [!DNL IAB Transparency and Consent Framework (TCF)] suporte, que é feito por meio de um plug-in no objeto Opt-in.

O plug-in do Audience Manager para TCF do IAB amplia a funcionalidade de Opt-in e permite que AAM clientes avaliem, honrem e encaminhem as opções de privacidade do usuário para parceiros downstream de acordo com a TCF do IAB. Ele fornece um padrão que os controladores de dados (ou seja, você como cliente Adobe) e os fornecedores (DMPs, DSP, SSPs, servidores de anúncios etc.) O pode usar o para entender o consentimento no cenário de consentimento.

## Ativação da TCF do IAB {#enabling-iab-tcf}

Habilitar o Plug-in do Audience Manager para a TCF do IAB é fácil se você estiver usando o Adobe Experience Platform Launch, já que é uma caixa de seleção simples, como mostrado no vídeo curto abaixo:

>[!VIDEO](https://video.tv.adobe.com/v/26433/?quality=12)

Como alternativa, se você não estiver usando o Launch, poderá usar `isIabContext=true` para ativá-lo ao instanciar o Visitante do Experience Cloud. Isso inicia o fluxo TCF do IAB, ou seja, adiciona outra etapa para a obtenção de consentimento, usando a TCF do IAB para consultar a cadeia de caracteres TC do IAB e a fornece de volta ao Opt-in, que, por sua vez, se comunica com as soluções do Experience Cloud.

## String TC IAB {#iab-tcf-consent-string}

Um dos padrões que o IAB fornece é uma &quot;cadeia de consentimento&quot; (também conhecida como &quot;DaisyBit&quot;), que é na verdade duas listas juntas:

1. Finalidades: **O que** é o consentimento dado para fazer?
1. Fornecedores: **A quem** é dado consentimento?

### Finalidades {#purposes}

Com a TCF do IAB 2.0, há dez &quot;finalidades&quot; para coletar consentimento (o que os fornecedores podem fazer com os dados do visitante). A Adobe Audience Manager não requer todos os dez, mas apenas o consentimento para os seguintes fins, além do consentimento do fornecedor:

* **Finalidade 1:** Armazenar e/ou acessar informações em um dispositivo;
* **Finalidade 10:** desenvolver e melhorar os produtos;
* **Propósito especial 1:** garanta a segurança, evite fraudes e depure.

Esta é a primeira parte da string IAB TC e é registrada como 1’s e 0’s, ditando se essa finalidade/atividade é aprovada ou não.

>[!NOTE]
>
>De acordo com as regulamentações do IAB, o Especial Objetivo 1 (Garantir a segurança, evitar fraudes e depurar) é sempre consentido e os usuários não podem se opor a ele.

### Fornecedores {#vendors}

Outra parte da cadeia de caracteres IAB TC é uma longa lista de várias centenas de fornecedores, para que os visitantes possam receber uma lista de fornecedores aplicáveis que têm tags no site e possam escolher quais fornecedores usar. Os fornecedores mantêm seu ponto na lista. Por exemplo, o número de fornecedor da Adobe Audience Manager nesta lista é 565. Se esse número na lista tiver um &quot;1&quot;, o Audience Manager poderá fazer os objetivos aprovados na frente da lista. Se o local do AAM tiver um &quot;0&quot;, ele não poderá fazer nada com os dados.

**Para o Audience Manager fornecer uma interface de usuário para que os clientes usem a TCF do IAB para escolher essas finalidades e fornecedores, ou para aprovar/rejeitar todas as atividades, você deve usar um parceiro da CMP registrado na TCF do IAB ou criar um que seja compatível com a TCF do IAB e esteja registrado na TCF do IAB.**

## Opt-in: Tradução entre Soluções IAB e Adobe {#opt-in-translating-between-iab-and-adobe-solutions}

Um dos benefícios do uso da TCF do IAB é que os objetivos padrão listados acima provavelmente dão ao usuário final mais uma ideia do que estão aprovando do que uma lista de soluções de Adobe. Os usuários finais podem não saber o que significa &quot;aprovar&quot; o Audience Manager ou [!DNL Target], mas &quot;Armazenar e/ou acessar informações em um dispositivo&quot; ou &quot;Desenvolver e melhorar produtos&quot; provavelmente será mais fácil para eles entender e consentir.

Para que o Audience Manager seja aprovado (ou seja, para que a tradução dos objetivos do IAB para o Opt-in dê AAM &quot;sim&quot;), os objetivos 1 e 10, conforme listado acima, devem receber o consentimento do usuário final. Se um desses itens não for aprovado ou se um fornecedor não for aprovado, AAM não executará disparos de pixel ou definirá cookies. Também é bom saber que muitos clientes simplesmente optam por fornecer ao usuário final uma interface do usuário &quot;tudo ou nada&quot;, o que, é claro, permitiria ou impediria o uso do Audience Manager (e das outras soluções do Experience Cloud).

Há algumas informações excelentes na [documentação](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=en) sobre como o fluxo do Plug-in do Audience Manager para TCF do IAB se aplica aos casos de uso do Editor e do Anunciante.

## IAB: Enviar Consentimento a Download {#iab-sending-consent-downstream}

Quando o Plug-in do Audience Manager para a TCF do IAB é usado, as opções de consentimento do usuário também são enviadas para as sincronizações de ID no nível da plataforma (de terceiros) para parceiros que estão presentes na Lista de fornecedores globais, para que o parceiro tenha as informações de consentimento do usuário e possa agir de acordo com elas. Essas informações são enviadas em duas variáveis:

* gdpr = 1
* gdpr_consent = [cadeia de consentimento codificada]

O problema é que, se o usuário estiver no contexto IAB e não fornecer consentimento (ou fornecer consentimento negativo), o Audience Manager não coletará a cadeia de caracteres TC IAB e, como tal, ignorará as chamadas. Então, nesse caso.. sem transmissão de consentimento.

## Demonstração {#demo}

No vídeo abaixo, veja como os cookies e os beacons da ECID e das soluções são afetados pelas seleções de opções do usuário do IAB.

>[!VIDEO](https://video.tv.adobe.com/v/26434/?quality=12)

Para obter informações mais detalhadas sobre o Plug-in do Audience Manager para TCF do IAB 2.0, incluindo como implementar e testar, casos de uso e workflow, consulte a [documentação](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).
