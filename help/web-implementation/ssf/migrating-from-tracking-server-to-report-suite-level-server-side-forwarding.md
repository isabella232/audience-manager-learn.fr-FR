---
title: Migration du serveur de suivi vers le transfert côté serveur au niveau de la Report Suite
description: Cet article et cette vidéo vous montreront comment activer le transfert côté serveur des données Analytics vers l’Audience Manager au niveau d’une suite de rapports plutôt qu’au niveau du serveur de suivi.
product: audience manager, analytics
feature: integration with analytics
topics: null
audience: implementer
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1776
translation-type: tm+mt
source-git-commit: dfd549508cc223714bdb07ac6fd2aa31e6ca5586
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# Migration de [!UICONTROL Tracking Server] vers [!UICONTROL Report Suite]niveau [!UICONTROL Server-Side Forwarding] {#migrating-from-tracking-server-to-report-suite-level-server-side-forwarding}

Cet article et cette vidéo vous montreront comment activer l&#39;Audience Manager [!UICONTROL server-side forwarding] des [!DNL Analytics] données à un [!UICONTROL report suite] niveau plutôt qu&#39;à un [!UICONTROL tracking server] niveau.

## Introduction {#introduction}

Si vous disposez de Adobe Audience Manager ET Adobe Analytics, vous pouvez implémenter &quot;[!UICONTROL Server-side Forwarding]&quot; des [!DNL Analytics] données à l’Audience Manager. Cela signifie que, au lieu d’envoyer deux accès à votre page (un à [!DNL Analytics] et un à l’Audience Manager), il peut simplement envoyer un accès à [!DNL Analytics]et [!DNL Analytics] transmettra ces données à l’Audience Manager. Si vous disposez déjà de cette fonctionnalité et si elle a été activée/mise en oeuvre avant octobre 2017, il [!UICONTROL server-side forwarding] se peut que vous utilisiez votre &quot;[!UICONTROL Tracking Server]&quot;, qui doit être activé par le service à la clientèle ou le service de conseil en Adobe de l’Adobe. Depuis octobre 2017, vous pouvez désormais vous configurer [!UICONTROL server-side forwarding] vous-même et le faire au [!UICONTROL Report Suite] niveau (transfert PER [!UICONTROL Report Suite]). Il y a des avantages importants à cela, qui seront discutés ci-dessous.

## [!UICONTROL Tracking Server] Transfert {#tracking-server-forwarding}

Il [!UICONTROL tracking server] s’agit de l’emplacement vers lequel vous envoyez vos [!DNL Analytics] données, ainsi que du domaine dans lequel la demande d’image et le cookie sont écrits. Elle doit être définie dans la gestion dynamique des balises ou [!DNL Experience Platform Launch], ou dans le [!DNL AppMeasurement.js] fichier, et ressemblera généralement à ceci, avec le remplacement de &quot;monsite&quot; par votre site ou nom de l’entreprise :

`s.trackingServer = "mysite.sc.omtrdc.net";`

Si [!UICONTROL server-side forwarding] est configuré pour transférer au [!UICONTROL tracking server] niveau, tout accès envoyé à ce niveau [!UICONTROL tracking server] (SI le service d’identification des Experience Cloud est également activé) sera transféré à l’Audience Manager. Il a fallu que le service à la clientèle de l’Adobe ou le service de conseil en Adobe l’activent. Ce sont également eux qui peuvent le désactiver, APRÈS que vous ayez basculé vers le [!UICONTROL report suite] transfert, comme décrit ci-dessous.

Si vous n’êtes pas certain que vous [!DNL tracking server forwarding] êtes activé, contactez le service à la clientèle ou le service de conseil en Adobe de l’Adobe, et ils devraient être en mesure de vous le faire savoir.

## [!UICONTROL Report Suite]-Level [!UICONTROL Server-Side Forwarding] {#report-suite-level-server-side-forwarding}

L&#39;un des plus grands avantages du passage à l&#39; [!UICONTROL report suite] expédition [!UICONTROL tracking server] est que vous pouvez maintenant utiliser &quot;Audience Analytics&quot;, qui est la capacité de transférer l&#39;Audience Manager [!UICONTROL segments] à Adobe Analytics pour une [!UICONTROL segment] analyse détaillée. Cette fonctionnalité exceptionnelle n&#39;est PAS prise en charge si vous êtes toujours en [!UICONTROL tracking server] transfert et non [!UICONTROL report suite] en transfert. Pour plus d’informations sur l’Audience Analytics, consultez la [documentation](https://marketing.adobe.com/resources/help/en_US/analytics/audiences/).

>[!VIDEO](https://video.tv.adobe.com/v/23701/?quality=12)

## Conseil important {#additional-resources}

Comme indiqué dans la vidéo ci-dessus, une fois que vous avez tous les [!UICONTROL report suites] paramètres à transférer à l’Audience Manager, vous devez contacter le service à la clientèle ou le service de conseil en Adobe Adobe et leur demander de désactiver le [!UICONTROL tracking server] transfert. Ce n&#39;est pas une urgence pour vous de faire cela, car avoir à la fois [!UICONTROL tracking server] transfert et [!UICONTROL report suite] transfert n&#39;entraînera PAS d&#39;accès au duplicata. Cependant, il est recommandé de ne faire [!UICONTROL report suite] avancer que les choses. Si vous continuez à [!UICONTROL tracking server] transmettre, non seulement peut-il transférer des données [!UICONTROL report suites] que vous ne souhaitez pas transférer, mais à l&#39;avenir, après que vous (et tout le monde de votre société) avez oublié que le [!UICONTROL tracking server] transfert est activé, vous pensez peut-être que les données ne sont pas transférées pour un élément spécifique [!UICONTROL report suite] (parce qu&#39;elles ne sont pas activées au niveau de la suite de rapports), mais que les données sont toujours transférées à cause du [!UICONTROL tracking server]. Ensuite, vous perdrez du temps et de l&#39;argent pour comprendre pourquoi il transfère et aussi pour payer les appels AAM serveur auxquels vous ne vous attendiez pas. C&#39;est donc une bonne idée de désactiver [!UICONTROL tracking server] le transfert dès que vous disposez de tous les éléments [!UICONTROL report suites] à transférer qui répondent aux besoins de votre entreprise.
