---
title: Migration du serveur de suivi vers le transfert côté serveur au niveau de la suite de rapports
description: Cet article et cette vidéo vous montrent comment activer le transfert côté serveur des données Analytics pour l’Audience Manager au niveau de la suite de rapports plutôt qu’au niveau du serveur de suivi.
product: audience manager
feature: Intégration d’Adobe Analytics
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1776
role: Developer, Data Engineer
level: Intermediate
exl-id: 08b81e52-a28a-43e4-a284-df2460a43016
source-git-commit: 4b91696f840518312ec041abdbe5217178aee405
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# Migration de [!UICONTROL Tracking Server] vers [!UICONTROL Report Suite] niveau [!UICONTROL Server-Side Forwarding] {#migrating-from-tracking-server-to-report-suite-level-server-side-forwarding}

Cet article et cette vidéo vous montrent comment activer [!UICONTROL server-side forwarding] de [!DNL Analytics] données pour l’Audience Manager à un niveau [!UICONTROL report suite] plutôt qu’à un niveau [!UICONTROL tracking server].

## Introduction {#introduction}

Si vous disposez de Adobe Audience Manager ET Adobe Analytics, vous pouvez implémenter &quot;[!UICONTROL Server-side Forwarding]&quot; des données [!DNL Analytics] à l’Audience Manager. Cela signifie que, au lieu que votre page envoie deux accès (un à [!DNL Analytics] et un à l’Audience Manager), il peut simplement envoyer un accès à [!DNL Analytics] et [!DNL Analytics] transmettra ces données à l’Audience Manager. Si cela est déjà en cours d’exécution et que vous l’avez activé/implémenté avant octobre 2017, votre [!UICONTROL server-side forwarding] peut être basé sur votre &quot;[!UICONTROL Tracking Server]&quot;, qui doit être activé par l’assistance clientèle Adobe ou par le service conseil en Adobe. Depuis octobre 2017, vous pouvez configurer vous-même [!UICONTROL server-side forwarding] et le faire à un niveau [!UICONTROL Report Suite] (transfert PER [!UICONTROL Report Suite]). Il y a des avantages significatifs à cela, qui seront abordés ci-dessous.

## [!UICONTROL Tracking Server] Transfert {#tracking-server-forwarding}

Votre [!UICONTROL tracking server] correspond à l’emplacement auquel vous envoyez vos données [!DNL Analytics], ainsi qu’au domaine sur lequel la demande d’image et le cookie sont écrits. Elle doit être définie dans la gestion dynamique des balises ou [!DNL Experience Platform Launch], ou dans le fichier [!DNL AppMeasurement.js]. Elle ressemblera généralement à ceci : votre site ou votre nom de société remplace &quot;mysite&quot; :

`s.trackingServer = "mysite.sc.omtrdc.net";`

Si [!UICONTROL server-side forwarding] est configuré pour être transféré au niveau [!UICONTROL tracking server], tout accès envoyé à cette [!UICONTROL tracking server] (SI le service d’ID Experience Cloud est également activé) sera transféré à l’Audience Manager. Cela devait être activé par le service à la clientèle d’Adobe ou par le service de conseil en Adobe. Il s’agit également de ceux qui peuvent la désactiver. APRÈS avoir basculé vers le transfert [!UICONTROL report suite], comme décrit ci-dessous.

Si vous ne savez pas si [!DNL tracking server forwarding] est activé pour vous, contactez l’assistance clientèle Adobe ou le service conseil en Adobe, et ils doivent être en mesure de vous le faire savoir.

## [!UICONTROL Report Suite]-Niveau [!UICONTROL Server-Side Forwarding] {#report-suite-level-server-side-forwarding}

L’un des plus grands avantages du passage au transfert [!UICONTROL report suite] à partir du transfert [!UICONTROL tracking server] est que vous pourrez désormais utiliser &quot;Audience Analytics&quot;, qui est la capacité de transférer l’Audience Manager [!UICONTROL segments] vers Adobe Analytics pour une analyse [!UICONTROL segment] détaillée. Cette fonctionnalité exceptionnelle n’est PAS prise en charge si vous utilisez toujours le transfert [!UICONTROL tracking server] et non le transfert [!UICONTROL report suite]. Pour plus d’informations sur l’Audience Analytics, consultez la [documentation](https://marketing.adobe.com/resources/help/en_US/analytics/audiences/).

>[!VIDEO](https://video.tv.adobe.com/v/23701/?quality=12)

## Conseil important {#additional-resources}

Comme indiqué dans la vidéo ci-dessus, une fois que tous les éléments [!UICONTROL report suites] sont définis pour être transférés à l’Audience Manager, vous devez contacter l’assistance clientèle d’Adobe ou le service de conseil d’Adobe et leur demander de désactiver le transfert [!UICONTROL tracking server]. Il n’est pas urgent que vous fassiez cela, car le transfert [!UICONTROL tracking server] et le transfert [!UICONTROL report suite] ne génèreront PAS de doublons d’accès. Toutefois, il est recommandé de n’activer que le transfert [!UICONTROL report suite]. Si vous laissez le transfert [!UICONTROL tracking server] activé, il peut non seulement transférer des données de [!UICONTROL report suites] que vous ne souhaitez pas transférer, mais, à l’avenir, après que vous (et tout le monde dans votre entreprise) avez oublié que le transfert [!UICONTROL tracking server] est activé, vous pouvez penser que les données ne sont pas transférées pour un [!UICONTROL report suite] spécifique (car il n’est pas activé au niveau de la suite de rapports), mais les données sont toujours transférées en raison de [!UICONTROL tracking server]. Ensuite, vous perdrez du temps et de l&#39;argent à comprendre pourquoi il transfère et aussi à payer pour les appels AAM serveur auxquels vous ne vous attendiez pas. Il est donc préférable de désactiver le transfert [!UICONTROL tracking server] dès que toutes les [!UICONTROL report suites] sont définies pour transférer ce qui convient aux besoins de votre entreprise.
