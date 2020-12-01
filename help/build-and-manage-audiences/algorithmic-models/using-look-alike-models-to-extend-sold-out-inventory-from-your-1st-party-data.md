---
title: Utilisation de modèles ressemblants pour étendre l'inventaire vendu à partir de vos données propriétaires
description: Dans ce didacticiel, nous allons passer en revue les étapes à suivre pour configurer et utiliser des modèles ressemblants à un look, de sorte que vous puissiez créer de nouvelles audiences semblables et les vendre comme une extension à votre segment de conversion.
feature: algorithmic models
topics: null
audience: all
activity: use
doc-type: feature video
team: Technical Marketing
kt: 1688
translation-type: tm+mt
source-git-commit: dfd549508cc223714bdb07ac6fd2aa31e6ca5586
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---


# Utilisation de l&#39;option Apparence [!UICONTROL Models] pour étendre le stock vendu à partir de vos [!UICONTROL First Party] données {#using-look-alike-models-to-extend-sold-out-inventory-from-your-st-party-data}

Dans ce didacticiel, nous allons passer en revue les étapes à suivre pour configurer et utiliser l&#39;apparence [!UICONTROL Models], de sorte que vous puissiez créer de nouvelles audiences semblables et les vendre comme extension de votre conversion [!UICONTROL segment].

## Détails du cas d&#39;utilisation {#use-case-details}

Vous êtes un éditeur de contenu. Si vous avez déjà épuisé l&#39;inventaire des convertisseurs de votre site, vous pensez peut-être que votre opportunité s&#39;arrête là. Saisissez l’apparence de l’AAM [!UICONTROL Models]. Grâce à cette fonctionnalité, vous pouvez étendre les stocks épuisés et vendre également des audiences de personnes qui ne se sont peut-être pas encore converties, mais qui ressemblent/se comportent comme des personnes qui ont converti. Cette audience [!UICONTROL segment] se vendrait généralement pour moins que les convertisseurs réels, mais elle vous permet néanmoins d&#39;ajouter à vos résultats en offrant une option d&#39;audience supplémentaire aux annonceurs qui souhaitent placer des publicités sur votre site. L’avantage supplémentaire de ce cas d’utilisation est qu’il ne vous coûte rien d’exécuter ce modèle sur vos données propriétaires.

Les étapes de ce didacticiel sont les suivantes :

1. Identifier/créer un utilisateur idéal (conversion) [!UICONTROL trait] ou [!UICONTROL segment]
1. Créez un [!UICONTROL model] en utilisant cette conversion [!UICONTROL trait]/[!UICONTROL segment] comme élément de base.
1. Sélectionnez les sources de données [!UICONTROL First party] dans le [!UICONTROL model] et exécutez le [!UICONTROL model]
1. Créez un [!UICONTROL Trait] algorithmique à partir des résultats [!UICONTROL model] et ajoutez [!UICONTROL trait] à un [!UICONTROL segment]
1. Offre de [!UICONTROL segment] aux annonceurs intéressés pour étendre la conversion [!UICONTROL segment] aux ventes

## Identifier/créer un utilisateur idéal (conversion) [!UICONTROL trait] ou [!UICONTROL segment] {#identify-create-an-ideal-user-conversion-trait-or-segment}

Qu&#39;essayez-vous d&#39;amener les gens à FAIRE sur votre site ? Quel est votre événement de conversion ? Bien sûr, il existe de nombreuses réponses différentes à cette question, selon le type de site/la verticale et les objectifs de votre organisation. Dans tous les cas, il est courant en AAM de créer un [!UICONTROL trait] pour les visiteurs qui répondent à ces critères.

Dans ce cas d’utilisation, cela est déjà supposé, car vous avez épuisé le stock pour les personnes qui sont des convertisseurs. Toutefois, pour les besoins de ce tutoriel, il est bon d&#39;en parler comme référence pour le reste du cas d&#39;utilisation.

En outre, lors de l&#39;utilisation de événements pour créer [!UICONTROL traits], il y a un problème majeur que vous devez garder à l&#39;esprit, afin de ne pas collecter plus d&#39;utilisateurs que vous ne devriez dans le [!UICONTROL trait]. Regardez la vidéo suivante pour la révélation générale. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**REMARQUE :** Dans la vidéo ci-dessus, l&#39;exemple que je montre suppose que vous avez Adobe Analytics. Bien sûr, ce n&#39;est peut-être pas le cas. Si vous disposez de Google Analytics (GA), nous disposons d&#39;un module que vous pouvez utiliser pour envoyer des données à AAM (voir la [documentation](https://marketing.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html)) et si votre activité de conversion sur votre site est envoyée à AAM par GA, vous pouvez créer votre caractéristique de conversion à partir de ce module. Si vous disposez d’une autre solution d’analyse (ou d’aucune solution d’analyse), vous pouvez toujours envoyer des données à AAM par l’intermédiaire de notre code DIL et de la fonction `submit`, etc. (voir la [documentation](https://marketing.adobe.com/resources/help/en_US/aam/c_dil.html)). Ensuite, créez à nouveau la caractéristique de conversion en fonction des données envoyées lorsque l’activité de conversion est effectuée sur le site.

## Création d’une apparence [!UICONTROL Model] à partir de [!UICONTROL First Party] données {#creating-a-look-alike-model-from-first-party-data}

Dans cette étape, nous allons créer une [!UICONTROL First Party] apparence [!UICONTROL Model]. Cela signifie que non seulement nous allons utiliser une conversion [!UICONTROL first party] [!UICONTROL trait]/[!UICONTROL segment] pour notre base [!UICONTROL trait]/[!UICONTROL segment] (ce serait normal pour la plupart de [!UICONTROL models] de toute façon), mais que nous allons également examiner uniquement le pool de données [!UICONTROL first party] pour plus de personnes qui ressemblent aux convertisseurs. Nous n&#39;examinerons pas les données [!UICONTROL second party] ou [!UICONTROL third party].

Dans ce cas d’utilisation, c’est important, car nous tentons de créer [!UICONTROL segment] des utilisateurs de notre site qui ressemblent à des convertisseurs mais qui n’ont tout simplement pas encore convertis, afin de pouvoir vendre cet aspect [!UICONTROL segment] aux annonceurs intéressés.

>[!VIDEO](https://video.tv.adobe.com/v/23504/?quality-12)

## Création d’un algorithme [!UICONTROL Trait] {#creating-an-algorithmic-trait}

Ensuite, nous devrons créer un algorithme [!UICONTROL Trait], afin que les résultats de [!UICONTROL model] puissent être utilisés. Sans créer de [!UICONTROL trait], le [!UICONTROL model] est inutile. Ainsi, après l&#39;exécution de [!UICONTROL model], veillez à ouvrir la boîte de dialogue [!UICONTROL trait] et à créer un algorithme [!UICONTROL Trait]. La vidéo ci-dessous vous présente quelques conseils.

>[!VIDEO](https://video.tv.adobe.com/v/23523/?quality=12)

## Offre d’algorithme [!UICONTROL Segment] aux annonceurs {#offering-the-algorithmic-segment-to-advertisers}

Une fois que vous avez créé un [!UICONTROL Trait] algorithmique, vous pouvez créer un [!UICONTROL segment] dans lequel placer les données, de sorte que vous puissiez activer les données (vous ne pouvez pas activer un [!UICONTROL trait], mais plutôt en créer un nouveau [!UICONTROL trait] [!UICONTROL segment] avec le [!UICONTROL Trait] algorithmique, afin que vous puissiez activer (utiliser) le [!UICONTROL segment].

Une fois que vous avez créé un [!UICONTROL segment] visiteur [!UICONTROL first party] ayant obtenu de bons résultats dans l’apparence [!UICONTROL model] (c’est-à-dire qui ressemble à des convertisseurs mais n’a pas encore été converti), vous pouvez l’offre [!UICONTROL segment] aux annonceurs de votre site, même après avoir épuisé tous vos stocks de convertisseurs réels sur votre site. Il s’agit d’un excellent moyen d’étendre cette audience et de continuer à percevoir des recettes supplémentaires en utilisant l’option Apparence [!UICONTROL Models] dans l’Audience Manager.
