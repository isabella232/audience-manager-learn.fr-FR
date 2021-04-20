---
title: Migration du serveur de suivi vers le transfert côté serveur au niveau de la Report Suite
description: Cet article et cette vidéo vous montreront comment activer le transfert côté serveur des données Analytics vers l’Audience Manager au niveau d’une suite de rapports plutôt qu’au niveau du serveur de suivi.
product: audience manager
feature: Adobe Analytics Integration
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1776
role: "Developer, Data Engineer"
level: Intermediate
exl-id: 08b81e52-a28a-43e4-a284-df2460a43016
translation-type: tm+mt
source-git-commit: 256edb05f68221550cae2ef7edaa70953513e1d4
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# Migration de [!UICONTROL Tracking Server] à [!UICONTROL Report Suite] niveau [!UICONTROL Server-Side Forwarding] {#migrating-from-tracking-server-to-report-suite-level-server-side-forwarding}

Cet article et cette vidéo vous montreront comment activer [!UICONTROL server-side forwarding] des [!DNL Analytics] données pour l&#39;Audience Manager à un niveau [!UICONTROL report suite] plutôt qu&#39;à un niveau [!UICONTROL tracking server].

## Introduction {#introduction}

Si vous disposez de Adobe Audience Manager ET Adobe Analytics, vous pouvez implémenter &quot;[!UICONTROL Server-side Forwarding]&quot; des données [!DNL Analytics] à l&#39;Audience Manager. Cela signifie que, au lieu d’envoyer deux accès à votre page (un à [!DNL Analytics] et un à l’Audience Manager), il peut simplement envoyer un accès à [!DNL Analytics] et [!DNL Analytics] transmettra ces données à l’Audience Manager. Si vous disposez déjà de cette fonctionnalité en cours d’exécution et si elle a été activée/implémentée avant octobre 2017, votre [!UICONTROL server-side forwarding] peut être basé sur votre &quot;[!UICONTROL Tracking Server]&quot;, qui doit être activé par le service à la clientèle d’Adobe ou le service de conseil en Adobe. Depuis octobre 2017, vous pouvez désormais configurer [!UICONTROL server-side forwarding] vous-même et le faire à un niveau [!UICONTROL Report Suite] (transfert PER [!UICONTROL Report Suite]). Il y a des avantages importants à cela, qui seront discutés ci-dessous.

## [!UICONTROL Tracking Server] Transfert  {#tracking-server-forwarding}

Votre [!UICONTROL tracking server] correspond à l&#39;emplacement où vous envoyez vos données [!DNL Analytics], ainsi qu&#39;au domaine sur lequel la demande d&#39;image et le cookie sont écrits. Il doit être défini dans la gestion dynamique des balises ou [!DNL Experience Platform Launch], ou dans le fichier [!DNL AppMeasurement.js] et ressemblera généralement à ceci : votre site ou votre nom d’entreprise remplacera &quot;monsite&quot; :

`s.trackingServer = "mysite.sc.omtrdc.net";`

Si [!UICONTROL server-side forwarding] est configuré pour être transféré au niveau [!UICONTROL tracking server], tout accès envoyé à cet [!UICONTROL tracking server] (SI le service d’identification des Experience Cloud est également activé) sera transmis à l’Audience Manager. Il a fallu que le service à la clientèle de l’Adobe ou le service de conseil en Adobe l’activent. Ce sont également eux qui peuvent le désactiver, APRÈS que vous ayez basculé vers le transfert [!UICONTROL report suite], comme décrit ci-dessous.

Si vous ne savez pas si [!DNL tracking server forwarding] est activé pour vous, contactez le service à la clientèle de l&#39;Adobe ou le service de conseil en Adobe, et ils devraient être en mesure de vous le faire savoir.

## [!UICONTROL Report Suite]-Level  [!UICONTROL Server-Side Forwarding] {#report-suite-level-server-side-forwarding}

L&#39;un des plus grands avantages du transfert de [!UICONTROL report suite] à partir du transfert [!UICONTROL tracking server] est que vous pouvez désormais utiliser &quot;Audience Analytics&quot;, qui est la possibilité de transférer l&#39;Audience Manager [!UICONTROL segments] dans Adobe Analytics pour une analyse [!UICONTROL segment] détaillée. Cette fonctionnalité exceptionnelle n&#39;est PAS prise en charge si vous êtes toujours en transfert [!UICONTROL tracking server] et non [!UICONTROL report suite]. Pour plus d&#39;informations sur l&#39;Audience Analytics, consultez la [documentation](https://marketing.adobe.com/resources/help/en_US/analytics/audiences/).

>[!VIDEO](https://video.tv.adobe.com/v/23701/?quality=12)

## Conseil important {#additional-resources}

Comme indiqué dans la vidéo ci-dessus, une fois que vous avez configuré toutes les options [!UICONTROL report suites] pour transférer à l&#39;Audience Manager, vous devez contacter le service à la clientèle ou le service de conseil en Adobe de l&#39;Adobe et leur demander de désactiver le transfert [!UICONTROL tracking server]. Il ne s&#39;agit pas d&#39;une urgence pour vous, car le transfert de [!UICONTROL tracking server] et de [!UICONTROL report suite] n&#39;entraîne PAS d&#39;accès au duplicata. Cependant, il est recommandé de n&#39;activer que le transfert [!UICONTROL report suite]. Si vous laissez le transfert [!UICONTROL tracking server] activé, non seulement peut-il transférer des données de [!UICONTROL report suites] que vous ne souhaitez pas transférer, mais dans le futur, après que vous (et tout le monde à votre société) avez oublié que le transfert [!UICONTROL tracking server] est activé, vous pensez peut-être que les données ne sont pas transférées pour un [!UICONTROL report suite] spécifique (parce qu&#39;elles ne sont pas activées au niveau de la suite de rapports), mais que les données sont toujours transférées. [!UICONTROL tracking server]. Ensuite, vous perdrez du temps et de l&#39;argent pour comprendre pourquoi il transfère et aussi pour payer les appels AAM serveur auxquels vous ne vous attendiez pas. Il est donc recommandé de désactiver le transfert [!UICONTROL tracking server] dès que vous avez configuré tous les éléments [!UICONTROL report suites] pour qu&#39;ils soient transférés, ce qui est logique pour vos besoins professionnels.
