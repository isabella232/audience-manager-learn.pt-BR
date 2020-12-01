---
title: Suporte a IAB TCF 2.0 no Audience Manager
description: O Adobe oferece a você meios de gerenciar e comunicar as opções de privacidade dos usuários por meio da funcionalidade Aceitação e pelo Plug-in do Audience Manager para suporte à IAB Transparency and Consent Framework 2.0 (TCF 2.0). Este artigo funciona em conjunto com a documentação para ajudar você a entender o Plug-in do Audience Manager para o IAB TCF e como ele funciona junto com o objeto Opt-in do Adobe e seu CMP (Consent Management Provider — Provedor de Gerenciamento de Consentimento).
feature: data governance & privacy
topics: null
audience: implementer, architect
activity: implement
doc-type: technical video
team: Technical Marketing
thumbnail: 26434.jpg
kt: 5027
translation-type: tm+mt
source-git-commit: df8afb50ed3971dc47e6506d31a8222a7f488b25
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 0%

---


# Suporte a IAB TCF 2.0 no Audience Manager {#iab-tcf-support-in-audience-manager}

O Adobe oferece a você meios de gerenciar e comunicar as opções de privacidade dos usuários por meio da funcionalidade Aceitação e pelo Plug-in do Audience Manager para suporte à IAB Transparency and Consent Framework 2.0 (TCF 2.0). Este artigo funciona em conjunto com a documentação para ajudar você a entender o Plug-in do Audience Manager para o IAB TCF e como ele funciona junto com o objeto Opt-in do Adobe e seu CMP (Consent Management Provider — Provedor de Gerenciamento de Consentimento). Para saber mais sobre o IAB, visite seu site em [https://www.iabeurope.eu/](https://www.iabeurope.eu/).

## Primeira etapa: Entenda a aceitação da ECID {#first-step-understand-ecid-s-opt-in}

Para entender como trabalhar com o TCF do IAB, é necessário compreender primeiro a funcionalidade [!DNL Opt-in], que faz parte da biblioteca do Serviço de ID do Experience Cloud (ECID). Se você não estiver familiarizado com o modo de participação, consulte [este artigo útil](https://docs.adobe.com/content/help/en/core-services-learn/tutorials/id-service/use-opt-in-to-control-experience-cloud-activities-based-on-user-consent.html) primeiro. Você também deve revisar a documentação [Opt-in](https://docs.adobe.com/content/help/pt-BR/id-service/using/implementation/opt-in-service/optin-overview.html). Depois de percorrer esses recursos, volte para esta página e continue.

## O plug-in Audience Manager para IAB TCF {#the-audience-manager-plug-in-for-iab-tcf}

Agora que você tem pelo menos uma compreensão básica de como o serviço Opt-in funciona, o Audience Manager pode criar camadas nele [!DNL IAB Transparency and Consent Framework (TCF)] suporte, que é feito por meio de um plug-in no objeto Opt-in.

O plug-in do Audience Manager para IAB TCF amplia a funcionalidade do Opt-in e permite que AAM clientes avaliem, honrem e encaminhem opções de privacidade do usuário para parceiros downstream de acordo com a IAB TCF. Fornece um padrão que os controladores de dados (ou seja, você como cliente Adobe) e os fornecedores (DMPs, DSP, SSPs, servidores de anúncios etc.) pode usar para entender o consentimento no cenário de consentimento.

## Habilitando IAB TCF {#enabling-iab-tcf}

Habilitar o Plug-in Audience Manager para IAB TCF é fácil se você estiver usando o Adobe Experience Platform Launch, pois é uma caixa de seleção simples, como mostrado no vídeo curto abaixo:

>[!VIDEO](https://video.tv.adobe.com/v/26433/?quality=12)

Como alternativa, se você não estiver usando o Launch, poderá usar `isIabContext=true` para ativá-lo ao instanciar o Visitante Experience Cloud. Isso inicia o fluxo TCF do IAB, ou seja, adiciona outra etapa para o consentimento da coleta, usando o TCF do IAB para o query da sequência TC do IAB e o fornece de volta à Opt-in, que por sua vez se comunica com as soluções do Experience Cloud.

## String TC IAB {#iab-tcf-consent-string}

Um dos padrões que a IAB fornece é uma &quot;cadeia de caracteres de consentimento&quot; (também conhecida como &quot;DaisyBit&quot;), que é na verdade duas listas juntas:

1. Finalidades: **O que** está sendo dado consentimento para fazer?
1. Fornecedores: **A quem** está a ser dado consentimento?

### Finalidades {#purposes}

Com o IAB TCF 2.0, há dez &quot;objetivos&quot; para os quais obter consentimento (o que os fornecedores podem fazer com os dados do visitante). A Adobe Audience Manager não requer todos os dez, mas apenas o consentimento para os seguintes fins, além do consentimento do fornecedor:

* **Finalidade 1:** Armazenar e/ou acessar informações em um dispositivo;
* **Finalidade 10:** Desenvolver e melhorar produtos;
* **Finalidade especial 1:** Garanta a segurança, evite fraudes e depure.

Esta é a primeira parte da sequência de caracteres IAB TC e é apenas registrada como 1 e 0, indicando se essa finalidade/atividade foi aprovada.

>[!NOTE]
>
>De acordo com os regulamentos IAB, o Especial Propósito 1 (Garanta a segurança, previne fraudes e depure) é sempre aceito e os usuários não podem se opor a ele.

### Fornecedores {#vendors}

Outra parte da string IAB TC é uma lista longa de várias centenas de fornecedores, de modo que os visitantes podem ser apresentados com uma lista de fornecedores aplicáveis que possuem tags no site e podem escolher quais fornecedores usar. Os fornecedores mantêm seu lugar na lista. Por exemplo, o número do fornecedor da Adobe Audience Manager nesta lista é 565. Se esse número na lista tiver um &quot;1&quot;, então o Audience Manager pode fazer as finalidades aprovadas na parte frontal da lista. Se o local do AAM tiver um &quot;0&quot;, ele não poderá fazer nada com os dados.

**Para que a Audience Manager forneça uma interface do usuário para que os clientes usem o TCF da IAB para escolher essas finalidades e fornecedores, ou para aprovar/desaprovar toda a atividade, você deve usar um parceiro CMP registrado no IAB TCF ou criar um que suporte o TCF da IAB e esteja registrado no TCF da IAB.**

## Inclusão: Traduzir entre IAB e Adobe Solutions {#opt-in-translating-between-iab-and-adobe-solutions}

Um dos benefícios da utilização do TCF da IAB é que os objetivos padrão acima listados provavelmente dão ao usuário final mais uma ideia do que uma lista de soluções de Adobe. Os usuários finais talvez não saibam o que significa &quot;aprovar&quot; o Audience Manager ou [!DNL Target], mas &quot;Armazenar e/ou acessar informações em um dispositivo&quot; ou &quot;Desenvolver e melhorar produtos&quot; provavelmente é mais fácil para eles entenderem e consentirem.

Para que a Audience Manager seja aprovada (isto é, para que a tradução dos objetivos da IAB para a aceitação dê AAM um voto de &quot;sim&quot;), os objetivos 1 e 10, tal como acima enumerados, têm de receber o consentimento do utilizador final. Se qualquer um desses itens não for aprovado, ou se um fornecedor não for aprovado, AAM não executará disparos de pixel nem definirá cookies. Também é bom saber que muitos clientes simplesmente escolhem fornecer ao usuário final uma interface do usuário &quot;tudo ou nada&quot;, o que, é claro, permitiria ou impediria o uso de Audience Manager (e de outras soluções de Experience Cloud).

Há algumas informações excelentes na [documentação](https://marketing.adobe.com/resources/help/en_US/aam/aam-iab-plugin.html) sobre como o fluxo de Plug-in de Audience Manager para TCF IAB se aplica aos casos de uso do Publisher e do Anunciante.

## IAB: Enviando Consentimento para Baixo {#iab-sending-consent-downstream}

Quando o Plug-in de Audience Manager para IAB TCF é usado, as opções de consentimento do usuário também serão enviadas para sincronizações de ID de nível de plataforma (de terceiros) para parceiros que estão presentes na Lista de fornecedores globais, para que o parceiro tenha as informações de consentimento do usuário e possa agir com base nelas. Essas informações são enviadas em duas variáveis:

* gdpr = 1
* gdpr_agreement = [cadeia de caracteres de consentimento codificada]

O problema é que se o usuário estiver no contexto IAB e não fornecer consentimento (ou fornecer consentimento negativo), o Audience Manager não coleta a sequência de caracteres de TC IAB e, como tal, diminui as chamadas. Então, nesse caso... sem transmissão de consentimento.

## Demonstração{#demo}

No vídeo abaixo, veja como os cookies e os beacons da ECID e das soluções são afetados pelas seleções de opções do usuário do IAB.

>[!VIDEO](https://video.tv.adobe.com/v/26434/?quality=12)

Para obter informações mais detalhadas sobre o Plug-in de Audience Manager para IAB TCF 2.0, incluindo como implementar e testar, casos de uso e fluxo de trabalho, consulte a [documentação](https://docs.adobe.com/content/help/en/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).
