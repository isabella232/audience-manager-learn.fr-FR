---
title: Augmenter le RSDP en utilisant des modèles algorithmiques (ressemblants) dans l'Audience Manager
description: La véritable puissance de la modélisation identique à celle des Audiences Manager réside dans le fait que vous cherchez à étendre votre audience de base par rapport à un ensemble d’utilisateurs de qualité, tout nouveau, provenant de sources de données tierces et de deuxième niveau. Dans ce didacticiel, apprenez comment créer un modèle à partir de ces données.
feature: Modèles algorithmiques
topics: null
activity: use
doc-type: feature video
team: Technical Marketing
thumbnail: 25188.jpg
kt: 1849
role: '"Professionnel, développeur, ingénieur de données, architecte, architecte de données, administrateur, responsable"'
level: Intermédiaire
translation-type: tm+mt
source-git-commit: a7dc335e75697a7b1720eccdadbb9605fdeda798
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---


# Augmenter le RSDP en utilisant l&#39;algorithme (ressemblance) [!UICONTROL Models] dans l&#39;Audience Manager {#increase-roas-by-using-algorithmic-look-alike-models-in-audience-manager}

La puissance réelle de l&#39;apparence de la Audience Manager [!UICONTROL Modeling] vient lorsque vous cherchez à développer votre audience de base par rapport à un ensemble d&#39;utilisateurs de [!UICONTROL second party] et [!UICONTROL third party] [!UICONTROL data sources] de qualité flambant neuf. Dans ce didacticiel, découvrez les étapes nécessaires pour créer un [!UICONTROL model] à partir de ces données.

## Activez les flux de données [!UICONTROL Second Party] ou [!UICONTROL Third Party] à partir de l’Audience Marketplace {#enable-2nd-or-3rd-party-data-streams-from-the-audience-marketplace}.

Pour utiliser les données [!UICONTROL second party] et [!UICONTROL third party] dans un look identique [!UICONTROL model], nous devons d&#39;abord activer ces données dans votre interface d&#39;Audience Manager. L’Adobe dispose d’un grand nombre de fournisseurs de données [!UICONTROL second party] et [!UICONTROL third party] à partir desquels vous pouvez choisir. Ils sont disponibles pour vous dans une interface libre-service en AAM, via l&#39;Audience Marketplace. Accédez à l’Audience Marketplace et parcourez les possibilités. La vidéo suivante vous montrera comment procéder, y compris comment activer les flux gratuits &quot;Essayer avant d’acheter&quot;, afin que vous puissiez verrouiller les données qui seront les plus utiles à votre entreprise avant de vous engager à respecter les tarifs du fournisseur de données.

En outre, pour vous aider à rechercher et à décider quel fournisseur de données utiliser, une ressource intéressante est [[!DNL Adobe Audience Finder]](https://www.adobe-audience-finder.com/).

>[!VIDEO](https://video.tv.adobe.com/v/25188/?quality=12)

## Identifier/créer un utilisateur idéal (conversion) [!UICONTROL trait] ou [!UICONTROL segment] {#identify-create-an-ideal-user-conversion-trait-or-segment}

Qu&#39;essayez-vous d&#39;amener les gens à FAIRE sur votre site ? Quel est votre événement de conversion ? Bien sûr, il existe de nombreuses réponses différentes à cette question, selon le type de site/la verticale et les objectifs de votre organisation. Dans tous les cas, il est courant en AAM de créer un [!UICONTROL trait] pour les visiteurs qui répondent à ces critères.

Dans la vidéo ci-dessous, je vais vous montrer comment créer une conversion [!UICONTROL trait], que vous souhaiterez mettre en place au fur et à mesure que vous poursuivrez ce didacticiel et créez une apparence [!UICONTROL model].

En outre, lors de l&#39;utilisation des événements Adobe Analytics pour créer [!UICONTROL traits], il y a un problème majeur que vous devez garder à l&#39;esprit, afin de ne pas collecter plus d&#39;utilisateurs que vous ne devriez dans le [!UICONTROL trait]. Regardez la vidéo suivante pour la révélation générale. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**REMARQUE :** Dans la vidéo ci-dessus, l&#39;exemple que je montre suppose que vous avez Adobe Analytics. Bien sûr, ce n&#39;est peut-être pas le cas. Si vous disposez de Google Analytics (GA), nous disposons d&#39;un module que vous pouvez utiliser pour envoyer des données à AAM (voir la [documentation](https://marketing.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html)) et si votre activité de conversion sur votre site est envoyée à AAM par GA, vous pouvez créer votre conversion [!UICONTROL trait] à partir de ce module. Si vous disposez d’une autre solution d’analyse (ou d’aucune solution d’analyse), vous pouvez toujours envoyer des données à AAM par l’intermédiaire de notre code DIL et de la fonction `submit`, etc. (voir la [documentation](https://marketing.adobe.com/resources/help/en_US/aam/c_dil.html)). Créez ensuite la conversion [!UICONTROL trait] en fonction des données envoyées lorsque l’activité de conversion est effectuée sur le site.

## Créer un look identique [!UICONTROL Model] à partir de [!UICONTROL Second Party] ou de [!UICONTROL Third Party] données {#create-a-look-alike-model-from-2nd-or-3rd-party-data}

Après avoir suivi les étapes ci-dessus, nous sommes maintenant prêts à créer un algorithme (apparence) [!UICONTROL Model]. Au moment de la configuration de [!UICONTROL model], nous utiliserons la conversion [!UICONTROL trait] comme base [!UICONTROL trait] (visiteurs clés que nous voulons duplicata), et nous utiliserons le flux de données [!UICONTROL third party] activé pour attirer notre groupe de personnes.

>[!VIDEO](https://video.tv.adobe.com/v/25190/?quality-12)

## Une bonne pratique importante {#an-important-best-practice}

Lors de la création de l&#39;algorithme [!UICONTROL model] en Audience Manager, nous voulons évidemment que [!UICONTROL model] soit aussi efficace que possible. Comme le [!UICONTROL model] prend en compte tous les [!UICONTROL traits] dont font partie les membres de votre base [!UICONTROL trait]/[!UICONTROL segment], il n’aide pas le [!UICONTROL model] si TOUTES les personnes sont dans un [!UICONTROL trait]/[!UICONTROL segment]. Par conséquent, si vous avez un [!UICONTROL traits] super générique (comme tous ceux qui sont allés sur votre site, ou tous ceux qui ont reçu une publicité de votre part, etc.), assurez-vous que le [!UICONTROL data source] auquel ils appartiennent n&#39;est PAS inclus dans le [!UICONTROL data sources] de votre [!UICONTROL model]. Dans le cas d’utilisation de cet article, il est peu probable que vous le fassiez, car nous nous concentrons sur l’analyse des données [!UICONTROL third party] pour nos nouveaux alias d’apparence, mais cela vaut la peine d’être mentionné, et cela s’applique à TOUTES vos données algorithmiques [!UICONTROL models].

## Création d’un algorithme [!UICONTROL Trait] {#creating-an-algorithmic-trait}

Ensuite, nous devrons créer un algorithme [!UICONTROL Trait], afin que les résultats de [!UICONTROL model] puissent être utilisés. Sans créer de [!UICONTROL trait], le modèle est inutile. Ainsi, après l&#39;exécution de [!UICONTROL model], veillez à ouvrir la boîte de dialogue [!UICONTROL trait] et à créer un algorithme [!UICONTROL Trait]. La vidéo ci-dessous vous présente quelques conseils.

>[!VIDEO](https://video.tv.adobe.com/v/25191/?quality=12)

## Création d&#39;une [!UICONTROL Segment] à partir des données [!UICONTROL Model] et envoi de celle-ci à DSP {#creating-a-segment-from-the-model-data-and-sending-it-to-dsps}

Une fois que vous avez créé un [!UICONTROL Trait] algorithmique, vous pouvez créer un [!UICONTROL segment] pour l&#39;insérer, de sorte que vous puissiez activer les données (vous ne pouvez pas activer un [!UICONTROL trait], mais plutôt en créer un nouveau [!UICONTROL trait] [!UICONTROL segment] avec le [!UICONTROL Trait] algorithmique, de sorte que vous puissiez activer (utiliser) le [!UICONTROL segment]).

Une fois que vous avez créé un [!UICONTROL segment] à partir de cet algorithme [!UICONTROL trait], vous aurez une audience de clients potentiels qui ressemblent à des personnes qui ont déjà effectué des conversions sur votre site. Vous pouvez maintenant mapper [!UICONTROL segment] à l&#39;une de vos DSP [!UICONTROL destinations] en Audience Manager. Vous serez en mesure de cible votre marketing à ces &quot;look&quot;, qui sont plus susceptibles de convertir sur votre site que le public ordinaire, augmentant ainsi votre Retour sur dépenses publicitaires. Bonne chance !
