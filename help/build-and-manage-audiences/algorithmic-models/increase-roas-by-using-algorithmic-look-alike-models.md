---
title: Augmenter le RSDP en utilisant des modèles algorithmiques (ressemblants) dans l'Audience Manager
description: La véritable puissance de la modélisation identique à celle des Audiences Manager réside dans le fait que vous cherchez à étendre votre audience de base par rapport à un ensemble d’utilisateurs de qualité, tout nouveau, provenant de sources de données tierces et de deuxième niveau. Dans ce didacticiel, apprenez comment créer un modèle à partir de ces données.
feature: algorithmic models
topics: null
audience: all
activity: use
doc-type: feature video
team: Technical Marketing
kt: 1849
translation-type: tm+mt
source-git-commit: a108c51fdad66f4e7974eb96609b6d8f058cb6ff
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---


# Augmenter le RSDP en utilisant l&#39;algorithme (aspect) [!UICONTROL Models] dans l&#39;Audience Manager {#increase-roas-by-using-algorithmic-look-alike-models-in-audience-manager}

La véritable puissance de l&#39;apparence identique des Audiences Manager [!UICONTROL Modeling] réside dans le fait que vous cherchez à étendre votre audience de base par rapport à un ensemble d&#39;utilisateurs de qualité, flambant neuf, issus [!UICONTROL second party] et [!UICONTROL third party][!UICONTROL data sources]. Dans ce didacticiel, découvrez les étapes nécessaires à la création d’un [!UICONTROL model] formulaire à partir de ces données.

## Activation [!UICONTROL Second Party] ou [!UICONTROL Third Party] des flux de données à partir de l’Audience Marketplace {#enable-2nd-or-3rd-party-data-streams-from-the-audience-marketplace}

Pour utiliser [!UICONTROL second party] et [!UICONTROL third party] les données d&#39;une apparence identique [!UICONTROL model], nous devons d&#39;abord activer ces données dans votre interface d&#39;Audience Manager. L’Adobe dispose d’un grand nombre de fournisseurs de données [!UICONTROL second party] et de [!UICONTROL third party] données à partir desquels vous pouvez choisir. Ils sont disponibles pour vous dans une interface libre-service en AAM, via l&#39;Audience Marketplace. Accédez à l’Audience Marketplace et parcourez les possibilités. La vidéo suivante vous montrera comment procéder, y compris comment activer les flux gratuits &quot;Essayer avant d’acheter&quot;, afin que vous puissiez verrouiller les données qui seront les plus utiles à votre entreprise avant de vous engager à respecter les tarifs du fournisseur de données.

En outre, pour vous aider à rechercher et à décider quel fournisseur de données utiliser, une ressource intéressante est la [[!DNL Adobe Audience Finder]](https://www.adobe-audience-finder.com/).

>[!VIDEO](https://video.tv.adobe.com/v/25188/?quality=12)

## Identifiez/créez un utilisateur idéal (conversion) [!UICONTROL trait] ou [!UICONTROL segment] {#identify-create-an-ideal-user-conversion-trait-or-segment}

Qu&#39;essayez-vous d&#39;amener les gens à FAIRE sur votre site ? Quel est votre événement de conversion ? Bien sûr, il existe de nombreuses réponses différentes à cette question, selon le type de site/la verticale et les objectifs de votre organisation. Dans tous les cas, il est courant en AAM de créer un [!UICONTROL trait] pour les visiteurs qui répondent à ces critères.

Dans la vidéo ci-dessous, je vais vous montrer comment créer une conversion [!UICONTROL trait]que vous souhaitez mettre en place au fur et à mesure que vous poursuivrez ce tutoriel et créez un look [!UICONTROL model]identique.

En outre, lorsque vous utilisez des événements Adobe Analytics pour créer [!UICONTROL traits], il y a une grosse gadget à garder à l&#39;esprit, de sorte que vous ne collectez pas plus d&#39;utilisateurs que vous ne devriez dans le [!UICONTROL trait]. Regardez la vidéo suivante pour la révélation générale. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**REMARQUE :** Dans la vidéo ci-dessus, l&#39;exemple que je montre suppose que vous avez l&#39;Adobe Analytics. Bien sûr, ce n&#39;est peut-être pas le cas. Si vous disposez de Google Analytics (GA), nous disposons d&#39;un module que vous pouvez utiliser pour envoyer des données à AAM (voir la [documentation](https://marketing.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html)), et si votre activité de conversion sur votre site est envoyée à AAM par GA, vous pouvez créer votre conversion [!UICONTROL trait] à partir de ce module. Si vous disposez d’une autre solution d’analyse (ou d’une autre solution d’analyse), vous pouvez toujours envoyer des données à AAM par l’intermédiaire de notre code DIL et de la `submit` fonction, etc. (voir la [documentation](https://marketing.adobe.com/resources/help/en_US/aam/c_dil.html)). Créez ensuite la conversion [!UICONTROL trait] en fonction des données envoyées lorsque l’activité de conversion est effectuée sur le site.

## Création d’une apparence [!UICONTROL Model] à partir de [!UICONTROL Second Party][!UICONTROL Third Party] données {#create-a-look-alike-model-from-2nd-or-3rd-party-data}

Après avoir suivi les étapes ci-dessus, nous sommes maintenant prêts à créer un algorithme (identique) [!UICONTROL Model]. En configurant le [!UICONTROL model]module, nous utiliserons la conversion [!UICONTROL trait] comme base [!UICONTROL trait] [!UICONTROL third party] (visiteurs clés que nous voulons duplicata), et nous utiliserons le flux de données activé comme source de données pour notre groupe de personnes.

>[!VIDEO](https://video.tv.adobe.com/v/25190/?quality-12)

## Une bonne pratique importante {#an-important-best-practice}

Lorsque nous créons l&#39;algorithme [!UICONTROL model] en Audience Manager, nous voulons évidemment que le [!UICONTROL model] soit aussi efficace que possible. Comme la [!UICONTROL model] société prend en compte tous les [!UICONTROL traits] membres de votre base [!UICONTROL trait]ou[!UICONTROL segment] qui en font partie, cela n’aide pas la [!UICONTROL model] si TOUTES les personnes sont dans un [!UICONTROL trait]/[!UICONTROL segment]. Par conséquent, si vous avez un super générique [!UICONTROL traits] (comme tous ceux qui sont allés sur votre site, ou tous ceux qui ont reçu une publicité de votre part, etc.), assurez-vous que le [!UICONTROL data source] à lequel ils appartiennent n&#39;est PAS inclus dans le [!UICONTROL data sources] dans votre [!UICONTROL model]. Dans le cas d’utilisation de cet article, il est peu probable que vous le fassiez, car nous nous concentrons sur la recherche de [!UICONTROL third party] données pour nos nouveaux alias d’apparence, mais cela vaut la peine d’être mentionné, et cela s’applique à TOUS vos algorithmes [!UICONTROL models].

## Création d’un algorithme [!UICONTROL Trait] {#creating-an-algorithmic-trait}

Ensuite, nous allons devoir créer un algorithme [!UICONTROL Trait], afin que les résultats de l&#39; [!UICONTROL model] algorithme puissent être utilisés. Sans créer de [!UICONTROL trait]modèle, le modèle est inutile. Ainsi, après l&#39; [!UICONTROL model] exécution, veillez à entrer dans la [!UICONTROL trait] boîte de dialogue et à créer un algorithme [!UICONTROL Trait]. La vidéo ci-dessous vous présente quelques conseils.

>[!VIDEO](https://video.tv.adobe.com/v/25191/?quality=12)

## Création d’un [!UICONTROL Segment] à partir des [!UICONTROL Model] données et envoi de ce dernier à DSP {#creating-a-segment-from-the-model-data-and-sending-it-to-dsps}

Une fois que vous avez créé un algorithme [!UICONTROL Trait], vous pouvez en créer un nouveau [!UICONTROL segment] pour l’activer (vous ne pouvez pas activer un [!UICONTROL trait]mais en créer un nouveau[!UICONTROL trait] avec l’algorithme [!UICONTROL segment] dedans, de sorte que vous puissiez activer (utiliser) le [!UICONTROL Trait] [!UICONTROL segment]).

Une fois que vous avez créé un [!UICONTROL segment] fichier à partir de cet algorithme [!UICONTROL trait], vous aurez une audience de clients potentiels qui ressemblent à des personnes qui ont déjà effectué des conversions sur votre site. Vous pouvez maintenant mapper ceci [!UICONTROL segment] à n&#39;importe quelle DSP [!UICONTROL destinations] en Audience Manager. Vous serez en mesure de cible votre marketing à ces &quot;look&quot;, qui sont plus susceptibles de convertir sur votre site que le public ordinaire, augmentant ainsi votre Retour sur dépenses publicitaires. Bonne chance !
