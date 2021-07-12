---
title: Augmentation du retour sur investissement en utilisant des modèles algorithmiques (analogue) dans l’Audience Manager
description: La puissance réelle de la modélisation look-alike d’Audience Manager réside dans le fait que vous cherchez à étendre votre audience de base par rapport à un nouvel ensemble d’utilisateurs de qualité provenant de sources de données tierces et de deuxième niveau. Dans ce tutoriel, découvrez les étapes de création d’un modèle à partir de ces données.
feature: Modèles algorithmiques
topics: null
activity: use
doc-type: feature video
team: Technical Marketing
thumbnail: 25188.jpg
kt: 1849
role: User, Developer, Data Engineer, Architect, Data Architect, Admin, Leader
level: Intermediate
exl-id: 6626ae11-8709-4302-9e03-0d55878d2409
source-git-commit: 4b91696f840518312ec041abdbe5217178aee405
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 0%

---

# Augmentez le retour sur investissement en utilisant l’algorithme (analogue) [!UICONTROL Models] dans l’Audience Manager {#increase-roas-by-using-algorithmic-look-alike-models-in-audience-manager}

La puissance réelle de l’apparence identique de l’Audience Manager est [!UICONTROL Modeling] lorsque vous cherchez à étendre votre audience de base par rapport à un ensemble d’utilisateurs de [!UICONTROL second party] et [!UICONTROL third party] [!UICONTROL data sources] de qualité tout nouveau. Dans ce tutoriel, découvrez les étapes nécessaires à la création d’un [!UICONTROL model] à partir de ces données.

## Activez les flux de données [!UICONTROL Second Party] ou [!UICONTROL Third Party] à partir de l’Audience Marketplace. {#enable-2nd-or-3rd-party-data-streams-from-the-audience-marketplace}

Pour utiliser les données [!UICONTROL second party] et [!UICONTROL third party] dans un [!UICONTROL model] analogue, nous devons d’abord activer ces données dans l’interface d’Audience Manager. Adobe comporte un grand nombre de fournisseurs de données [!UICONTROL second party] et [!UICONTROL third party] à partir desquels vous pouvez choisir. Elles sont disponibles pour vous dans une interface en libre-service dans AAM, via l’Audience Marketplace. Accédez à l’Audience Marketplace et parcourez les possibilités. La vidéo suivante vous explique comment procéder, notamment comment activer les flux &quot;Essayer avant d’acheter&quot; gratuits, de sorte que vous puissiez verrouiller les données qui seront les plus utiles à votre organisation avant de vous engager dans la tarification du fournisseur de données.

En outre, pour vous aider à rechercher et à décider quel fournisseur de données utiliser, une ressource intéressante est la [[!DNL Adobe Audience Finder]](https://www.adobe-audience-finder.com/).

>[!VIDEO](https://video.tv.adobe.com/v/25188/?quality=12)

## Identifier/créer un utilisateur idéal (conversion) [!UICONTROL trait] ou [!UICONTROL segment] {#identify-create-an-ideal-user-conversion-trait-or-segment}

Qu’est-ce que vous essayez d’amener les gens à FAIRE sur votre site ? Quel est votre événement de conversion ? Bien sûr, il existe de nombreuses réponses à cette question, selon le type/la verticale de votre site et vos objectifs organisationnels. Dans tous les cas, il est courant dans AAM de créer une [!UICONTROL trait] pour les visiteurs qui répondent à ces critères.

Dans la vidéo ci-dessous, je vous montrerai comment créer une conversion [!UICONTROL trait], que vous souhaitez mettre en place au fur et à mesure que vous poursuivrez ce tutoriel et créez une apparence [!UICONTROL model].

En outre, lorsque vous utilisez des événements Adobe Analytics pour créer [!UICONTROL traits], il existe un obstacle majeur à garder à l’esprit, de sorte que vous ne collectez pas plus d’utilisateurs que vous ne le devriez dans la balise [!UICONTROL trait]. Regardez la vidéo suivante pour la grande révélation. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**REMARQUE :** Dans la vidéo ci-dessus, l’exemple que je vous montre suppose que vous disposez d’Adobe Analytics. Ce n&#39;est évidemment pas le cas. Si vous disposez de Google Analytics (GA), nous disposons d’un module que vous pouvez utiliser pour envoyer des données dans AAM (voir la [documentation](https://marketing.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html)), et si votre activité de conversion sur votre site est envoyée à AAM par GA, vous pouvez créer votre conversion [!UICONTROL trait] à partir de ce module. Si vous disposez d’une solution d’analyse différente (ou d’aucune solution d’analyse), vous pouvez toujours envoyer des données à AAM par l’intermédiaire de notre code de DIL et de la fonction `submit`, etc. (voir la [documentation](https://marketing.adobe.com/resources/help/en_US/aam/c_dil.html)). Créez ensuite la conversion [!UICONTROL trait] en fonction des données envoyées lorsque l’activité de conversion est effectuée sur le site.

## Créer un look-alike [!UICONTROL Model] à partir des données [!UICONTROL Second Party] ou [!UICONTROL Third Party] {#create-a-look-alike-model-from-2nd-or-3rd-party-data}

Après avoir suivi les étapes ci-dessus, nous sommes maintenant prêts à créer un algorithme (analogue) [!UICONTROL Model]. Au moment de la configuration de [!UICONTROL model], nous utiliserons la conversion [!UICONTROL trait] comme base [!UICONTROL trait] (visiteurs clés que nous voulons dupliquer) et nous utiliserons le flux de données [!UICONTROL third party] activé comme groupe de personnes à partir duquel nous pouvons extraire.

>[!VIDEO](https://video.tv.adobe.com/v/25190/?quality-12)

## Bonne pratique importante {#an-important-best-practice}

Lors de la création de l’algorithme [!UICONTROL model] en Audience Manager, nous voulons évidemment que [!UICONTROL model] soit aussi efficace que possible. Comme le [!UICONTROL model] prend en compte toutes les [!UICONTROL traits] dont font partie les membres de votre base [!UICONTROL trait]/[!UICONTROL segment], il n’aide pas le [!UICONTROL model] si TOUTES les personnes se trouvent dans un [!UICONTROL trait]/[!UICONTROL segment]. Par conséquent, si vous disposez d’un [!UICONTROL traits] super générique (comme toutes les personnes qui sont allées sur votre site, ou toutes celles qui ont reçu une publicité de votre part, etc.), assurez-vous que la [!UICONTROL data source] à laquelle elles appartiennent n’est PAS incluse dans la [!UICONTROL data sources] de votre [!UICONTROL model]. Dans le cas d’utilisation de cet article, il est peu probable que vous le fassiez, car nous nous concentrons sur les [!UICONTROL third party] données de nos nouveaux alias d’affichage, mais cela vaut la peine d’être mentionné et cela s’applique à TOUS vos [!UICONTROL models] algorithmiques.

## Création d’un algorithme [!UICONTROL Trait] {#creating-an-algorithmic-trait}

Ensuite, nous devrons créer un [!UICONTROL Trait] algorithmique afin que les résultats de [!UICONTROL model] puissent être utilisés. Sans créer de [!UICONTROL trait], le modèle est inutile. Ainsi, une fois que [!UICONTROL model] s’exécute, veillez à accéder à la boîte de dialogue [!UICONTROL trait] et à créer un [!UICONTROL Trait] algorithmique. La vidéo suivante vous guide et vous montre quelques conseils.

>[!VIDEO](https://video.tv.adobe.com/v/25191/?quality=12)

## Création d’une [!UICONTROL Segment] à partir des [!UICONTROL Model] données et envoi à DSP {#creating-a-segment-from-the-model-data-and-sending-it-to-dsps}

Une fois que vous avez créé un [!UICONTROL Trait] algorithmique, vous pouvez créer un [!UICONTROL segment] dans lequel activer les données (vous ne pouvez pas activer un [!UICONTROL trait], mais en créer un nouveau [!UICONTROL trait] [!UICONTROL segment] avec le [!UICONTROL Trait] algorithmique, de sorte que vous puissiez activer (utiliser) le [!UICONTROL segment]).

Une fois que vous avez créé une [!UICONTROL segment] à partir de cette [!UICONTROL trait] algorithmique, vous disposez d’une audience de clients potentiels qui ressemblent à des personnes qui ont déjà effectué des conversions sur votre site. Vous pouvez maintenant mapper cette [!UICONTROL segment] à l’une de vos DSP [!UICONTROL destinations] en Audience Manager. Vous pourrez cibler votre marketing sur ces pseudonymes, qui sont plus susceptibles de convertir votre visite sur votre site que le public normal, ce qui augmentera votre retour sur dépenses publicitaires. Bonne chance !
