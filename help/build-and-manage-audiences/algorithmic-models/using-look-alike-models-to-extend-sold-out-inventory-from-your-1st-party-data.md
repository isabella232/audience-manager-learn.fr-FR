---
title: Utilisation de modèles similaires pour étendre l’inventaire vendu à partir de vos données propriétaires
description: Dans ce tutoriel, nous allons passer en revue les étapes à suivre pour configurer et utiliser des modèles analogue afin que vous puissiez créer de nouvelles audiences semblables et les vendre comme extension de votre segment de conversion.
feature: Modèles algorithmiques
topics: null
activity: use
doc-type: feature video
team: Technical Marketing
thumbnail: 23523.jpg
kt: 1688
role: User, Developer, Data Engineer, Architect, Data Architect, Admin, Leader
level: Intermediate
exl-id: 6820528e-3211-4a1d-be05-50f1292179d2
source-git-commit: 4b91696f840518312ec041abdbe5217178aee405
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---

# Utilisation de l’[!UICONTROL Models] analogue pour étendre l’inventaire vendu à partir de vos données [!UICONTROL First Party] {#using-look-alike-models-to-extend-sold-out-inventory-from-your-st-party-data}

Dans ce tutoriel, nous allons passer en revue les étapes à suivre pour configurer et utiliser l’aspect ressemblant à [!UICONTROL Models], de sorte que vous puissiez créer de nouvelles audiences semblables et les vendre comme extension de votre conversion [!UICONTROL segment].

## Détails du cas d’utilisation {#use-case-details}

Vous êtes un éditeur de contenu. Si vous avez déjà épuisé l’inventaire des convertisseurs de votre site, vous pouvez penser que votre opportunité s’arrête là. Saisissez l’apparence d’AAM [!UICONTROL Models]. Grâce à cette fonctionnalité, vous pouvez étendre l’inventaire épuisé et également vendre des audiences de personnes qui n’ont peut-être pas encore effectué de conversions, mais qui ressemblent/agissent comme des personnes qui ont effectué des conversions. Cette audience [!UICONTROL segment] serait généralement vendue pour des convertisseurs inférieurs aux convertisseurs réels, mais elle vous permet néanmoins d’ajouter à vos résultats en fournissant une option d’audience supplémentaire pour les annonceurs qui souhaitent placer des publicités sur votre site. L’avantage supplémentaire de ce cas d’utilisation est qu’il ne vous coûte rien d’exécuter ce modèle sur vos données propriétaires.

Les étapes de ce tutoriel sont les suivantes :

1. Identifier/créer un utilisateur idéal (conversion) [!UICONTROL trait] ou [!UICONTROL segment]
1. Créez un [!UICONTROL model] à l’aide de cette conversion [!UICONTROL trait]/[!UICONTROL segment] en tant qu’élément de base.
1. Sélectionnez [!UICONTROL First party] source(s) de données dans la balise [!UICONTROL model] et exécutez la balise [!UICONTROL model]
1. Créez un [!UICONTROL Trait] algorithmique à partir des résultats [!UICONTROL model] et ajoutez le [!UICONTROL trait] à un [!UICONTROL segment]
1. Offrir aux annonceurs intéressés [!UICONTROL segment] d’étendre les ventes de conversion [!UICONTROL segment]

## Identifier/créer un utilisateur idéal (conversion) [!UICONTROL trait] ou [!UICONTROL segment] {#identify-create-an-ideal-user-conversion-trait-or-segment}

Qu’est-ce que vous essayez d’amener les gens à FAIRE sur votre site ? Quel est votre événement de conversion ? Bien sûr, il existe de nombreuses réponses à cette question, selon le type/la verticale de votre site et vos objectifs organisationnels. Dans tous les cas, il est courant dans AAM de créer une [!UICONTROL trait] pour les visiteurs qui répondent à ces critères.

Dans ce cas pratique, cela est déjà supposé, car vous avez épuisé l’inventaire pour les personnes qui sont des convertisseurs. Toutefois, pour les besoins de ce tutoriel, il est bon d’en parler comme référence pour le reste du cas d’utilisation.

En outre, lors de l’utilisation d’événements pour créer [!UICONTROL traits], vous devez tenir compte d’un piège majeur afin de ne pas collecter plus d’utilisateurs que vous ne le devriez dans la balise [!UICONTROL trait]. Regardez la vidéo suivante pour la grande révélation. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**REMARQUE :** Dans la vidéo ci-dessus, l’exemple que je vous montre suppose que vous disposez d’Adobe Analytics. Ce n&#39;est évidemment pas le cas. Si vous disposez de Google Analytics (GA), nous disposons d’un module que vous pouvez utiliser pour envoyer des données dans AAM (voir la [documentation](https://marketing.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html)). Si votre activité de conversion sur votre site est envoyée à AAM par GA, vous pouvez créer votre caractéristique de conversion à partir de ce module. Si vous disposez d’une solution d’analyse différente (ou d’aucune solution d’analyse), vous pouvez toujours envoyer des données à AAM par l’intermédiaire de notre code de DIL et de la fonction `submit`, etc. (voir la [documentation](https://marketing.adobe.com/resources/help/en_US/aam/c_dil.html)). Ensuite, créez à nouveau la caractéristique de conversion en fonction des données envoyées lorsque l’activité de conversion est exécutée sur le site.

## Création d’une [!UICONTROL Model] analogue à partir de données [!UICONTROL First Party] {#creating-a-look-alike-model-from-first-party-data}

Au cours de cette étape, nous allons créer une [!UICONTROL First Party] analogue [!UICONTROL Model]. Cela signifie que non seulement nous allons utiliser une [!UICONTROL first party] conversion [!UICONTROL trait]/[!UICONTROL segment] pour notre base [!UICONTROL trait]/[!UICONTROL segment] (ce serait normal pour la plupart des [!UICONTROL models] de toute façon), mais que nous allons également uniquement examiner le pool de données [!UICONTROL first party] pour plus de personnes qui ressemblent aux convertisseurs. Nous ne consulterons pas les données [!UICONTROL second party] ou [!UICONTROL third party].

Dans ce cas d’utilisation, c’est important, car nous tentons de créer une [!UICONTROL segment] d’utilisateurs de notre site qui ressemblent à des convertisseurs mais qui n’ont simplement pas encore fait l’objet d’une conversion, de sorte que nous puissions vendre cet aspect identique [!UICONTROL segment] aux annonceurs intéressés.

>[!VIDEO](https://video.tv.adobe.com/v/23504/?quality-12)

## Création d’un algorithme [!UICONTROL Trait] {#creating-an-algorithmic-trait}

Ensuite, nous devrons créer un [!UICONTROL Trait] algorithmique afin que les résultats de [!UICONTROL model] puissent être utilisés. Sans créer de [!UICONTROL trait], la [!UICONTROL model] est inutile. Ainsi, une fois que [!UICONTROL model] s’exécute, veillez à accéder à la boîte de dialogue [!UICONTROL trait] et à créer un [!UICONTROL Trait] algorithmique. La vidéo suivante vous présente quelques conseils.

>[!VIDEO](https://video.tv.adobe.com/v/23523/?quality=12)

## Offre algorithmique [!UICONTROL Segment] aux annonceurs {#offering-the-algorithmic-segment-to-advertisers}

Une fois que vous avez créé un [!UICONTROL Trait] algorithmique, vous pouvez créer un [!UICONTROL segment] dans lequel vous pourrez activer les données (vous ne pouvez pas activer un [!UICONTROL trait], mais plutôt en créer un nouveau [!UICONTROL trait] [!UICONTROL segment] avec le [!UICONTROL Trait] algorithmique, de sorte que vous puissiez activer (utiliser) le [!UICONTROL segment].

Une fois que vous avez créé une [!UICONTROL segment] de [!UICONTROL first party] visiteurs ayant obtenu de bons résultats dans l’apparence [!UICONTROL model] (c’est-à-dire qui ressemblent à des convertisseurs mais n’ont pas encore été convertis), vous pouvez proposer cette [!UICONTROL segment] aux annonceurs sur votre site, même après avoir épuisé l’ensemble de votre inventaire de convertisseurs réels sur votre site. Il s’agit d’un excellent moyen d’étendre cette audience et de continuer à afficher des recettes supplémentaires en utilisant la fonction look-Alike [!UICONTROL Models] dans l’Audience Manager.
