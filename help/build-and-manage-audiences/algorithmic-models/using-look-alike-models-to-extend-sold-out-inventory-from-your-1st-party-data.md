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


# Utilisation de l&#39;apparence [!UICONTROL Models] pour étendre l&#39;inventaire vendu à partir de vos [!UICONTROL First Party] données {#using-look-alike-models-to-extend-sold-out-inventory-from-your-st-party-data}

Dans ce didacticiel, nous allons passer en revue les étapes à suivre pour configurer et utiliser l&#39;apparence [!UICONTROL Models]afin que vous puissiez créer de nouvelles audiences semblables et les vendre comme une extension à votre conversion [!UICONTROL segment].

## Détails du cas d’utilisation {#use-case-details}

Vous êtes un éditeur de contenu. Si vous avez déjà épuisé l&#39;inventaire des convertisseurs de votre site, vous pensez peut-être que votre opportunité s&#39;arrête là. Saisissez l’apparence de l’AAM [!UICONTROL Models]. Grâce à cette fonctionnalité, vous pouvez étendre les stocks épuisés et vendre également des audiences de personnes qui ne se sont peut-être pas encore converties, mais qui ressemblent/se comportent comme des personnes qui ont converti. Cette audience [!UICONTROL segment] se vendrait généralement pour moins que les véritables convertisseurs, mais vous permet néanmoins d’ajouter à votre chiffre d’affaires en offrant une option d’audience supplémentaire aux annonceurs qui souhaitent placer des publicités sur votre site. L’avantage supplémentaire de ce cas d’utilisation est qu’il ne vous coûte rien d’exécuter ce modèle sur vos données propriétaires.

Les étapes de ce didacticiel sont les suivantes :

1. Identifiez/créez un utilisateur idéal (conversion) [!UICONTROL trait] ou [!UICONTROL segment]
1. Créer un [!UICONTROL model] utilisateur à l’aide de cette conversion [!UICONTROL trait]/[!UICONTROL segment] en tant qu’élément de base
1. Choisissez [!UICONTROL First party] la ou les sources de données dans le [!UICONTROL model] menu et exécutez la variable [!UICONTROL model]
1. Créez un algorithme [!UICONTROL Trait] à partir des [!UICONTROL model] résultats et ajoutez le [!UICONTROL trait] à un [!UICONTROL segment]
1. Offre [!UICONTROL segment] aux annonceurs intéressés pour étendre les [!UICONTROL segment] ventes de conversion

## Identifiez/créez un utilisateur idéal (conversion) [!UICONTROL trait] ou [!UICONTROL segment] {#identify-create-an-ideal-user-conversion-trait-or-segment}

Qu&#39;essayez-vous d&#39;amener les gens à FAIRE sur votre site ? Quel est votre événement de conversion ? Bien sûr, il existe de nombreuses réponses différentes à cette question, selon le type de site/la verticale et les objectifs de votre organisation. Dans tous les cas, il est courant en AAM de créer un [!UICONTROL trait] pour les visiteurs qui répondent à ces critères.

Dans ce cas d’utilisation, cela est déjà supposé, car vous avez épuisé le stock pour les personnes qui sont des convertisseurs. Toutefois, pour les besoins de ce tutoriel, il est bon d&#39;en parler comme référence pour le reste du cas d&#39;utilisation.

En outre, lorsque vous utilisez des événements pour créer [!UICONTROL traits], il y a un problème majeur que vous devez garder à l&#39;esprit, de sorte que vous ne collectiez pas plus d&#39;utilisateurs que vous ne devriez dans le [!UICONTROL trait]. Regardez la vidéo suivante pour la révélation générale. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**REMARQUE :** Dans la vidéo ci-dessus, l&#39;exemple que je montre suppose que vous avez l&#39;Adobe Analytics. Bien sûr, ce n&#39;est peut-être pas le cas. Si vous disposez de Google Analytics (GA), nous disposons d&#39;un module que vous pouvez utiliser pour envoyer des données à AAM (voir la [documentation](https://marketing.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html)), et si votre activité de conversion sur votre site est envoyée à AAM par GA, vous pouvez créer votre caractéristique de conversion à partir de là. Si vous disposez d’une autre solution d’analyse (ou d’une autre solution d’analyse), vous pouvez toujours envoyer des données à AAM par l’intermédiaire de notre code DIL et de la `submit` fonction, etc. (voir la [documentation](https://marketing.adobe.com/resources/help/en_US/aam/c_dil.html)). Ensuite, créez à nouveau la caractéristique de conversion en fonction des données envoyées lorsque l’activité de conversion est effectuée sur le site.

## Création d’une apparence [!UICONTROL Model] à partir de [!UICONTROL First Party] données {#creating-a-look-alike-model-from-first-party-data}

Dans cette étape, nous allons créer une [!UICONTROL First Party] ressemblance [!UICONTROL Model]. Cela signifie que non seulement nous allons utiliser une [!UICONTROL first party] conversion [!UICONTROL trait]/[!UICONTROL segment] pour notre base [!UICONTROL trait]/[!UICONTROL segment] (ce serait normal pour la plupart [!UICONTROL models] [!UICONTROL first party] de toute façon), mais que nous allons également chercher dans le pool de données pour plus de personnes qui ressemblent aux convertisseurs. Nous n&#39;étudierons pas [!UICONTROL second party] ni [!UICONTROL third party] les données.

Dans ce cas d’utilisation, c’est important, car nous tentons de créer un groupe [!UICONTROL segment] d’utilisateurs sur notre site qui ressemblent à des convertisseurs mais qui n’ont tout simplement pas encore été convertis, afin que nous puissions vendre ce look [!UICONTROL segment] aux annonceurs intéressés.

>[!VIDEO](https://video.tv.adobe.com/v/23504/?quality-12)

## Création d’un algorithme [!UICONTROL Trait] {#creating-an-algorithmic-trait}

Ensuite, nous allons devoir créer un algorithme [!UICONTROL Trait], afin que les résultats de la [!UICONTROL model] peut être utilisé. Sans créer un [!UICONTROL trait], le [!UICONTROL model] système est inutile. Ainsi, après l&#39; [!UICONTROL model] exécution, veillez à entrer dans la [!UICONTROL trait] boîte de dialogue et à créer un algorithme [!UICONTROL Trait]. La vidéo ci-dessous vous présente quelques conseils.

>[!VIDEO](https://video.tv.adobe.com/v/23523/?quality=12)

## Offre algorithmique [!UICONTROL Segment] aux annonceurs {#offering-the-algorithmic-segment-to-advertisers}

Une fois que vous avez créé un algorithme [!UICONTROL Trait], vous pouvez en créer un nouveau [!UICONTROL segment] pour l&#39;insérer, de sorte que vous puissiez activer les données (vous ne pouvez pas activer un [!UICONTROL trait], mais plutôt créer un nouveau[!UICONTROL trait] avec l&#39;algorithme [!UICONTROL segment] dedans, de sorte que vous pouvez activer (utiliser) le [!UICONTROL Trait] [!UICONTROL segment].

Une fois que vous avez créé un [!UICONTROL segment] groupe de [!UICONTROL first party] visiteurs qui ont obtenu des scores élevés dans l’apparence identique [!UICONTROL model] [!UICONTROL segment] (c’est-à-dire qui ressemblent à des convertisseurs mais n’ont pas encore été convertis), vous pouvez l’offre aux annonceurs de votre site, même après avoir épuisé tous vos stocks de convertisseurs réels sur votre site. Il s’agit d’un excellent moyen d’étendre cette audience et de continuer à percevoir des recettes supplémentaires en utilisant l’aspect [!UICONTROL Models] de l’Audience Manager.
