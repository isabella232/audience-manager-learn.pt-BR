---
title: Migração da implementação de AAM do seu site do DIL do lado do cliente para o encaminhamento pelo lado do servidor
description: Este tutorial se aplica a você se você tiver Adobe Audience Manager (AAM) e Adobe Analytics, e estiver enviando uma ocorrência da página para AAM usando o código "DIL" (Data Integration Library) e também enviando uma ocorrência da página para a Adobe Analytics. Como você tem ambas as soluções, e como elas fazem parte da Adobe Experience Cloud, você tem a oportunidade de seguir a melhor prática de ativar o "encaminhamento pelo lado do servidor (SSF)", que permite que os servidores de coleta de dados do Analytics encaminhem os dados de análise do site em tempo real para o Audience Manager, em vez de fazer com que o código do cliente envie uma ocorrência adicional da página para o AAM. Este tutorial o guiará pelas etapas de tornar o switch da implementação mais antiga do "DIL do lado do cliente" para o método mais recente de "encaminhamento pelo lado do servidor".
product: audience manager, analytics
feature: integration with analytics
topics: null
audience: implementer
activity: implement
doc-type: tutorial
team: Technical Marketing
kt: 1778
translation-type: tm+mt
source-git-commit: 133279f589bd58aef36a980c2b7248ae00fd9496
workflow-type: tm+mt
source-wordcount: '2319'
ht-degree: 0%

---


# Migração da implementação de AAM do seu site de [!DNL Client-Side] DIL para [!DNL Server-Side Forwarding] {#migrating-your-site-s-aam-implementation-from-client-side-dil-to-server-side-forwarding}

Este tutorial se aplica a você se você tiver o Adobe Audience Manager (AAM) e o Adobe Analytics, e estiver enviando uma ocorrência da página para AAM usando o código &quot;DIL ([!DNL Data Integration Library])&quot; e também enviando uma ocorrência da página para o Adobe Analytics. Como você tem ambas as soluções, e já que ambas fazem parte da Adobe Experience Cloud, você tem a oportunidade de seguir a melhor prática de ativar o &quot;[!DNL Server-Side Forwarding] (SSF)&quot;, que permite que os servidores de coleta de [!DNL Analytics] dados encaminhem os dados analíticos do site em tempo real para o Audience Manager, em vez de ter o [!DNL client-side] código enviando uma ocorrência adicional da página para o AAM. Este tutorial o guiará pelas etapas de tornar o switch da implementação &quot;[!DNL Client-Side DIL]&quot; mais antiga para o método &quot;[!DNL Server-Side forwarding]&quot; mais recente.

## [!DNL Client-Side] (DIL) vs. [!DNL Server-Side] {#client-side-dil-vs-server-side}

Ao comparar e contrastar esses dois métodos de obter dados do Adobe Analytics em AAM, pode ser útil visualizar as diferenças na imagem a seguir:

![do lado do cliente para o lado do servidor](assets/client-side_vs_server-side_aam_implementation.png)

### [!DNL Client-side] Implementação de DIL {#client-side-dil-implementation}

Se você estiver usando este método para obter dados do Adobe Analytics para AAM, isso significa que você tem duas ocorrências que vêm de suas páginas da Web: Um indo para [!DNL Analytics], e outro indo para AAM (depois de ter copiado os [!DNL Analytics] dados na página da Web. [!UICONTROL Segments] são retornados do AAM para a página, onde podem ser usados para personalização etc. Essa é considerada uma implementação &quot;legada&quot; e não é mais recomendada.

Além de não seguir as práticas recomendadas, as desvantagens de usar esse método incluem:

* Duas ocorrências vindas da página em vez de apenas uma
* [!UICONTROL Server-Side Forwarding] é necessário para o compartilhamento em tempo real de AAM audiências para [!DNL Analytics], portanto, [!DNL Client-side] as implementações não permitem esse recurso (e possivelmente outros recursos no futuro)

É recomendável que você passe para um [!UICONTROL Server-Side Forwarding] método de implementação AAM.

### [!UICONTROL Server-Side Forwarding] Implementação {#server-side-forwarding-implementation}

Conforme mostrado na imagem acima, uma ocorrência vem da página da Web para o Adobe Analytics. [!DNL Analytics] em seguida, encaminha esses dados para AAM em tempo real, e os visitantes são avaliados em AAM [!UICONTROL traits] e [!UICONTROL segments], como se a ocorrência tivesse vindo diretamente da página.

[!UICONTROL Segments] são retornados na mesma ocorrência em tempo real para [!DNL Analytics], que encaminha a resposta para a página da Web para personalização, etc.

Não há nenhum tempo para mudar para o encaminhamento pelo lado do servidor. Recomendamos que qualquer pessoa que tenha Audience Manager e [!DNL Analytics] utilize esse método de implementação.

## Você tem duas Tarefas principais {#you-have-two-main-tasks}

Há bastante informação nesta página, e é tudo importante, claro. No entanto, **tudo se resume a duas coisas principais que você precisa fazer**:

1. Altere o código do [!DNL Client-Side] DIL para [!UICONTROL Server-Side Forwarding] código
1. Inverter o switch no [!DNL Analytics] para start o encaminhamento real de dados (por [!DNL Admin Console] [!UICONTROL report suite])

Se você ignorar esses dois, o SSF não funcionará corretamente. As etapas e os dados adicionais foram adicionados a esse documento para ajudá-lo a executar essas duas etapas corretamente para sua configuração.

## Opções de implementação {#implementation-options}

Conforme você muda de [!DNL client-side] para [!DNL server-side], uma das tarefas que você terá é mudar o código para o novo [!UICONTROL Server-Side Forwarding] código. Isso é feito usando uma das seguintes opções:

* Adobe Experience Platform Launch - nossa opção de implementação recomendada para propriedades da Web. Você verá que esta é uma tarefa muito fácil, como [!DNL Launch] fez tudo o que é difícil para você.
* Na página - Você também pode colocar o novo código SSF diretamente na `doPlugins` função dentro do seu [!DNL appMeasurement.js] arquivo, se ainda não estiver usando o Adobe Launch
* Outros gerenciadores de tags - Eles podem ser tratados da mesma forma que a opção anterior (Na página), pois você ainda colocará o código SSF em `doPlugins`, onde quer que o outro gerenciador de tags armazene o [!DNL AppMeasurement] código

Analisaremos cada um desses itens abaixo na seção Atualizando o código.

## Etapas da implementação {#implementation-steps}

### Etapa 0: Pré-requisito: Serviço de ID de Experience Cloud (ECID) {#step-prerequisite-experience-cloud-id-service-ecid}

O pré-requisito principal para mudar para [!UICONTROL Server-Side Forwarding] é ter o serviço de ID de Experience Cloud implementado. Isso é feito com mais facilidade se você estiver usando o Experience Platform Launch, caso em que você simplesmente instala a extensão ECID e ela fará o resto.

Se você estiver usando um TMS que não seja de Adobe, ou nenhum TMS, implemente o ECID para ser executado **antes** de qualquer outra solução de Adobe. Consulte a documentação [](https://marketing.adobe.com/resources/help/pt_BR/mcvid/) ECID para obter mais detalhes. O único outro pré-requisito diz respeito às versões de código, de modo que você simplesmente aplique as versões mais recentes do código nas etapas a seguir, você estará bem.

>[!NOTE]
>
>Leia este documento inteiro antes de implementar. A seção &quot;Timing&quot; abaixo contém informações importantes sobre *quando* você deve implementar cada peça, incluindo a ECID (se ainda não estiver implementada).

### Etapa 1: Registrar opções atualmente usadas do código DIL {#step-record-currently-used-options-from-dil-code}

À medida que você se prepara para ir do [!DNL Client-Side] código de DIL para [!UICONTROL Server-Side Forwarding], a primeira etapa é identificar tudo o que você está fazendo com o código de DIL, incluindo configurações personalizadas e dados enviados para AAM. As coisas a serem notadas e consideradas incluem:

* Variáveis normais, usando o módulo de [!DNL Analytics] DIL - Você não precisará se preocupar com essa, pois seu trabalho é apenas enviar as [!DNL siteCatalyst.init] [!DNL Analytics] variáveis normais, e isso acontecerá em virtude de simplesmente ter o SSF ativado.
* Subdomínio do parceiro - na função DIL.create, anote o `partner` parâmetro. Isso é conhecido como &quot;subdomínio do parceiro&quot; ou, às vezes, &quot;ID do parceiro&quot; e será necessário quando você inserir o novo código SSF.
* [!DNL Visitor Service Namespace] - Também conhecido como &quot;[!DNL Org ID]&quot; ou &quot;[!DNL IMS Org ID]&quot;, você precisará disso ao configurar o novo código SSF. Tome nota disso.
* containerNSID, uuidCookie e outras opções avançadas - Anote quaisquer opções avançadas adicionais que você esteja usando para que possa defini-las no código SSF também.
* Variáveis de página adicionais - Se outras variáveis estiverem sendo enviadas para AAM a partir da página (além das [!DNL Analytics] variáveis normais manipuladas pelo siteCatalyst.init), você precisará anotá-las para que possam ser enviadas por SSF (alerta do spoiler: por [!DNL contextData] variáveis).

### Etapa 2: Atualização do código {#step-updating-the-code}

Na seção acima intitulada &quot;Opções de implementação&quot;, várias opções são fornecidas em relação a como/onde você está implementando [!UICONTROL Server-Side Forwarding]. Para que esta seção seja eficaz, temos de a dividir nestas seções (com duas delas combinadas). Vá para o método desta seção que melhor descreve suas necessidades.

#### Adobe Experience Platform Launch {#launch-by-adobe}

Assista ao vídeo abaixo para saber mais sobre como mover as opções de implementação do código de [!DNL Client-Side] DIL para [!UICONTROL Server-Side Forwarding] o Experience Platform Launch.

>[!VIDEO](https://video.tv.adobe.com/v/26310/?quality=12)

#### &quot;Na página&quot; ou &quot;Não-Adobe Tag Manager&quot; {#on-the-page-or-non-adobe-tag-manager}

Assista ao vídeo abaixo para saber mais sobre como mover as opções de implementação do código de [!DNL Client-Side] DIL para [!UICONTROL Server-Side Forwarding] o [!DNL AppMeasurement] código, residindo em um arquivo ou em um sistema que não seja o de gerenciamento de tags do Adobe.

>[!VIDEO](https://video.tv.adobe.com/v/26312/?quality=12)

### Etapa 3: Ativar o encaminhamento (por [!UICONTROL Report Suite]) {#step-enabling-the-forwarding-per-report-suite}

Até agora, neste tutorial, passamos todo o nosso tempo mudando o código de [!DNL Client-Side DIL] código para [!UICONTROL Server-Side Forwarding]. Tudo bem, porque é a parte mais difícil. Esta seção, embora você veja que é muito fácil, é tão importante quanto atualizar o código. Neste vídeo, você verá como mudar o switch que permite o encaminhamento real de dados do Analytics para o Audience Manager.

>[!VIDEO](https://video.tv.adobe.com/v/26355/?quality-12)

**NOTA:** Conforme declarado no vídeo, lembre-se de que levará até 4 horas para que a ativação do encaminhamento seja totalmente implementada no backend do Experience Cloud.

## Tempo {#timing}

Como lembrete, há duas tarefas principais para mudar de [!DNL Client-Side DIL] para [!UICONTROL Server-Side Forwarding]:

1. Atualização do código
1. Deslizando o switch [!DNL Analytics] [!DNL Admin Console]

Mas a questão é, qual você faz primeiro? Isso importa? Ok, desculpe, isso foram duas perguntas. Mas as respostas são... Depende, e sim, *pode* importar. Como isso é vago? Vamos dividir. Mas primeiro uma questão adicional que pode surgir se você for uma grande organização com muitos sites: Eu tenho que fazer tudo de uma vez? Aquele é um pouco mais fácil. Não. Você pode fazer isso peça a peça... tipo... :)

### Mergulho um pouco mais fundo {#a-little-deeper-dive}

A razão pela qual o tempo e a ordem de compra são importantes é por causa de como o encaminhamento *realmente *funciona, que pode ser resumido nos seguintes poucos fatos técnicos:

* Se o serviço de ID do Experience Cloud (ECID) estiver implementado e o switch no [!DNL Analytics] (&quot;o switch&quot;) estiver ativado, os dados serão encaminhados de [!DNL Admin Console] [!DNL Analytics] para AAM, mesmo se você ainda não tiver atualizado o código.
* Se você não tiver o ECID implementado, os dados não serão encaminhados, mesmo se você tiver o switch ligado, e o código SSF for exibido.
* O código SSF (seja no interior [!DNL Launch] ou na página) realmente trata a resposta e é, claro, necessário para completar a migração.
* Lembre-se de que a opção SSF está ativada por [!UICONTROL Report Suite], mas que o código é manipulado pela propriedade em [!DNL Launch]ou pelo [!DNL AppMeasurement] arquivo se você não usar [!DNL Launch]

### Práticas recomendadas {#best-practices}

Com base nesses detalhes técnicos, veja a seguir as recomendações para o momento do &quot;o que fazer quando&quot;:

#### Se você NÃO tiver o ECID implementado {#if-you-do-not-have-ecid-yet-implemented}

1. Inverta o comutador para dentro [!DNL Analytics] para cada [!UICONTROL report suite] um que você ativará para SSF

   1. O encaminhamento ainda não será start porque você não tem ECID

1. Por site, atualize seu código de [!DNL Client-Side DIL] para SSF (isso pode estar na [!DNL Launch] página ou na página, como discutido em outra seção acima)

   1. O encaminhamento agora fluirá (conforme você adicionou o ECID) e você também deverá receber uma resposta JSON adequada ao seu [!DNL Analytics] beacon (consulte a seção Validação e Solução de Problemas abaixo para obter mais detalhes)

#### Se você implementou a ECID {#if-you-do-have-ecid-implemented}

1. Prepare e planeje para que você esteja pronto para atualizar seu código de DIL para SSF PER, [!UICONTROL report suite] que você habilitará para SSF:

   1. Inverta o switch para [!DNL Analytics] ativar o SSF

      1. O encaminhamento VAI start porque a ECID está ativada
   1. Assim que possível, atualize seu código de [!DNL Client-Side DIL] para SSF (isso pode estar no [!DNL Launch] ou na página, como discutido em outra seção acima)

      1. Você deve receber uma resposta JSON adequada ao seu [!DNL Analytics] beacon (consulte a seção Validação e solução de problemas abaixo para obter mais detalhes)


**NOTA 1:** É importante executar essas duas etapas o mais próximo possível, pois entre as etapas 1 e 2 acima, você terá a duplicação de dados entrando em AAM. Em outras palavras, o SSF começará a enviar dados de [!DNL Analytics] para AAM e, como o código DIL ainda está na página, também haverá uma ocorrência que vai diretamente da página para a AAM, dobrando os dados. Assim que você atualizar o código de DIL para SSF, isso será aliviado.

**NOTA 2:** Se você preferir ter uma pequena discrepância nos dados em vez de uma pequena duplicação de dados, é possível alterar a ordem das etapas 1 e 2 acima. Mover o código de DIL para SSF pararia o fluxo de dados para AAM até que você pudesse girar o switch para ligar o SSF para o [!UICONTROL report suite]. Normalmente, os clientes preferem ter uma pequena duplicação de dados em vez de perder a inserção de visitantes [!UICONTROL traits] e [!UICONTROL segments].

#### Tempo de migração quando você tem muitos sites e [!UICONTROL Report Suites] {#migration-timing-when-you-have-many-sites-and-report-suites}

Este tópico é brevemente abordado em seções anteriores, na medida em que a estratégia principal pode ser resumida pelo seguinte:

Migre um site/[!UICONTROL report suite] (ou grupo de sites/[!UICONTROL report suites]) de cada vez.

No entanto, isso pode tornar-se um pouco complicado com base em alguns cenários possíveis:

* Você tem um site que contém vários [!UICONTROL report suites]
* Você tem um site [!UICONTROL report suite] que inclui vários sites (como um global [!UICONTROL report suite])
* Você usa uma [!DNL Launch] propriedade para cobrir vários sites
* Você tem equipes de Desenvolvimento diferentes para sites diferentes

Por causa desses itens, pode ficar um pouco complicado. As melhores coisas que posso sugerir são:

* Leve algum tempo para fazer uma estratégia para migrar para o SSF, com base nas coisas que foram explicadas acima
* Com base no fato de que uma única propriedade em [!DNL Launch] (ou um único [!DNL AppMeasurement] arquivo) normalmente mapeia para 1 ou 2 diferentes [!UICONTROL report suites], você provavelmente poderá fazer um plano que funcione nesses grupos distintos um por um, atualizando sua empresa para SSF
* Se você estiver trabalhando com a Adobe Consulting, fale com eles sobre seu plano de migração, para que eles possam ajudar conforme necessário

## Validação e solução de problemas {#validation-and-troubleshooting}

A principal maneira de validar se o aplicativo [!UICONTROL Server-Side Forwarding] está funcionando é observar a resposta a qualquer uma das ocorrências do Adobe Analytics que vêm do aplicativo.

Se você não estiver fazendo [!UICONTROL server-side forwarding] de dados de [!DNL Analytics] para Audience Manager, então não há resposta para o [!DNL Analytics] beacon (além de um pixel 2x2). No entanto, se você estiver fazendo SSF, então há itens que você pode verificar na [!DNL Analytics] solicitação e na resposta que permitirão saber se [!DNL Analytics] está se comunicando corretamente com o Audience Manager, encaminhando a ocorrência e obtendo uma resposta.

>[!VIDEO](https://video.tv.adobe.com/v/26359/?quality=12)

**AVISO:** Cuidado com o falso &quot;sucesso&quot; - se houver uma resposta, e tudo parecer estar funcionando, certifique-se de que você tenha o objeto &quot;coisa&quot; na resposta. Se não, podem ver uma mensagem que diz [!DNL "status":"SUCCESS"]. Por mais louco que isso pareça, isso é na verdade prova de que NÃO esteja funcionando corretamente. Se você vir isso, isso significa que você concluiu a atualização do código em [!DNL Launch] ou [!DNL AppMeasurement], mas o encaminhamento no [!DNL Analytics] ainda não [!DNL Admin Console] foi concluído. Nesse caso, é necessário verificar se o SSF foi ativado no [!DNL Analytics] para o [!DNL Admin Console] [!UICONTROL report suite]. Se você tem, e ainda não passaram 4 horas, seja paciente, pois pode levar tanto tempo para fazer todas as mudanças necessárias no backend.

![falso sucesso](assets/falsesuccess.png)

For more information about [!UICONTROL Server-Side Forwarding], please see the [documentation](https://marketing.adobe.com/resources/help/en_US/reference/ssf.html).
