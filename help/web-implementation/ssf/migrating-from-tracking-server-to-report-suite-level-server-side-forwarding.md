---
title: Migration du serveur de suivi vers le transfert côté serveur au niveau de la suite de rapports
description: Découvrez comment activer le transfert côté serveur des données Adobe Analytics pour l’Audience Manager au niveau de la suite de rapports plutôt qu’au niveau du serveur de suivi.
product: audience manager
feature: Adobe Analytics Integration
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1776
role: Developer, Data Engineer
level: Intermediate
exl-id: 08b81e52-a28a-43e4-a284-df2460a43016
source-git-commit: 4adaade180545bcf5f911b7453a7e9939e2ed178
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 0%

---

# Migration du serveur de suivi vers le transfert côté serveur au niveau de la suite de rapports {#migrating-from-tracking-server-to-report-suite-level-server-side-forwarding}

Cet article et cette vidéo vous montrent comment activer le transfert côté serveur de [!DNL Analytics] Données à Audience Manager lors d’une [!UICONTROL report suite] plutôt qu’à un niveau [!UICONTROL tracking server] niveau.

## Introduction {#introduction}

Si vous disposez de Adobe Audience Manager ET Adobe Analytics, vous pouvez mettre en oeuvre le transfert côté serveur de la variable [!DNL Analytics] données à Audience Manager. Cela signifie que, au lieu de votre page, envoyez deux accès (un à [!DNL Analytics] et un à l’Audience Manager), il peut envoyer un accès à [!DNL Analytics], et [!DNL Analytics] transmettra ces données à Audience Manager.

Si vous l’avez déjà activé et mis en oeuvre avant octobre 2017, le transfert côté serveur peut être basé sur vos [!UICONTROL Tracking Server], qui devait être activé par l’assistance clientèle d’Adobe ou par le service de conseil d’Adobe. Depuis octobre 2017, vous pouvez configurer vous-même le transfert côté serveur et le faire au niveau de la suite de rapports (transfert par suite de rapports). Il y a des avantages significatifs à cela, qui sont présentés ci-dessous.

## [!UICONTROL Tracking server] transfert {#tracking-server-forwarding}

Votre [!UICONTROL tracking server] est l’emplacement auquel vous envoyez votre [!DNL Analytics] et également le domaine sur lequel la demande d’image et le cookie sont écrits. Elle doit être définie dans DTM ou [!DNL Experience Platform Launch], ou dans la variable [!DNL AppMeasurement.js] et ressemblera généralement à ce qui suit : votre site ou nom de votre entreprise remplace &quot;mysite&quot; :

`s.trackingServer = "mysite.sc.omtrdc.net";`

Si le transfert côté serveur est configuré pour être transféré à l’adresse [!UICONTROL tracking server] niveau, tout accès envoyé à ce niveau [!UICONTROL tracking server] (SI le service d’ID d’Experience Cloud est également activé) est transféré à l’Audience Manager. Cela devait être activé par le service à la clientèle d’Adobe ou par le service de conseil en Adobe. Il peut également le désactiver. APRÈS avoir activé [!UICONTROL report suite] transfert, comme décrit ci-dessous.

Si vous n’êtes pas sûr si [!DNL tracking server forwarding] est activé pour vous, contactez l’assistance clientèle d’Adobe ou le service de conseil d’Adobe, et ils doivent être en mesure de vous le faire savoir.

## [!UICONTROL Report-suite]Transfert côté serveur au niveau {#report-suite-level-server-side-forwarding}

L’un des plus grands avantages de la transition vers [!UICONTROL report suite] transfert depuis [!UICONTROL tracking server] Le transfert est que vous pouvez désormais utiliser &quot;Audience Analytics&quot;, ce qui permet de transférer l’Audience Manager. [!UICONTROL segments] Revenez à Adobe Analytics pour une analyse détaillée des segments. Cette fonctionnalité exceptionnelle n’est PAS prise en charge si vous êtes toujours sur [!UICONTROL tracking server] transfert et non [!UICONTROL report suite] transfert. Pour plus d’informations sur l’Audience Analytics, voir [documentation](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html).

>[!VIDEO](https://video.tv.adobe.com/v/23701/?quality=12)

## Conseil important {#additional-resources}

Comme indiqué dans la vidéo ci-dessus, une fois que vous avez tous les [!UICONTROL report suites] si vous souhaitez transférer vers l’Audience Manager, contactez l’assistance clientèle Adobe ou le service Adobe-conseil, puis demandez-lui de désactiver la variable [!UICONTROL tracking server] transfert. Ce n&#39;est pas une urgence pour vous de le faire, parce qu&#39;avoir les deux [!UICONTROL tracking server] transfert et [!UICONTROL report suite] le transfert n’entraîne pas la duplication des accès. Toutefois, il est recommandé d’avoir uniquement [!UICONTROL report suite] transfert activé.

Si vous partez [!UICONTROL tracking server] le transfert à partir de, non seulement peut-il transférer des données depuis [!UICONTROL report suites] que vous ne voulez pas être transféré, mais à l&#39;avenir, après que vous (et tout le monde dans votre entreprise) avez oublié que [!UICONTROL tracking server] le transfert est activé, vous pensez peut-être que les données ne sont pas transférées pour un [!UICONTROL report suite]. En effet, elle n’est pas activée au niveau de la suite de rapports, mais les données sont toujours transférées en raison de la variable [!UICONTROL tracking server]. Ensuite, vous perdrez du temps et de l&#39;argent à comprendre pourquoi il transfère et aussi à payer pour les appels AAM serveur auxquels vous ne vous attendiez pas. Il est donc conseillé de désactiver [!UICONTROL tracking server] le transfert dès que vous disposez de toutes les [!UICONTROL report suites] à transférer ce qui est logique en fonction des besoins de votre entreprise.
