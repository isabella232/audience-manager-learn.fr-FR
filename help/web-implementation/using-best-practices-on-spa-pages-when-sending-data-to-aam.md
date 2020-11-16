---
title: Utilisation des bonnes pratiques sur les pages SPA lors de l’envoi de données à AAM
description: Dans ce document, nous décrirons plusieurs bonnes pratiques que vous devez suivre et dont vous devez tenir compte lorsque vous envoyez des données d’applications d’une seule page (SPA) à Adobe Audience Manager (AAM). Ce document se concentrera sur l’utilisation du Launch by Adobe, qui est la méthode d’implémentation recommandée.
feature: implementation basics
topics: spa
audience: implementer
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1390
translation-type: tm+mt
source-git-commit: a108c51fdad66f4e7974eb96609b6d8f058cb6ff
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# Utilisation des bonnes pratiques sur les pages SPA lors de l’envoi de données à AAM {#using-best-practices-on-spa-pages-when-sending-data-to-aam}

Dans ce document, nous décrirons plusieurs bonnes pratiques que vous devez suivre et connaître lorsque vous envoyez des données de [!UICONTROL Single Page Applications] (SPA) à Adobe Audience Manager (AAM). Ce document se concentre sur l’utilisation [!UICONTROL Experience Platform Launch], qui est la méthode d’implémentation recommandée.

## Notes initiales

* Les éléments ci-dessous partent du principe que vous utilisez [!DNL Platform Launch] pour la mise en oeuvre sur votre site. Si vous n’utilisez pas [!DNL Platform Launch]les éléments à prendre en compte, vous devrez les adapter à votre méthode d’implémentation.
* Tous les SPA sont différents, vous devrez peut-être modifier certains des éléments suivants pour mieux répondre à vos besoins, mais nous voulions partager avec vous certaines pratiques exemplaires ; à quoi vous devez penser lorsque vous envoyez des données de SPA pages à l&#39;Audience Manager.

## Diagramme simple de travail avec les SPA et les AAM dans l’Experience Platform Launch {#simple-diagram-of-working-with-spas-and-aam-in-experience-platform-launch}

![spa pour se détendre [!DNL launch]](assets/spa_for_aam_in_launch.png)

>[!NOTE]
>Comme indiqué, il s’agit d’un diagramme simplifié de la façon dont SPA pages sont gérées dans une implémentation Adobe Audience Manager (sans Adobe Analytics) utilisée [!DNL Platform Launch]. Comme vous pouvez le voir, c&#39;est assez direct, avec la grande décision étant comment vous allez communiquer un changement de vue (ou une action) à [!DNL Platform Launch].

## Déclenchement [!DNL Launch] à partir de la page SPA {#triggering-launch-from-the-spa-page}

Deux des méthodes les plus courantes pour déclencher une règle dans [!DNL Platform Launch] (et par conséquent envoyer des données en Audience Manager) sont les suivantes :

* Définition de événements personnalisés JavaScript (voir l’exemple [ICI](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html) avec Adobe Analytics)
* Utilisation d’un [!UICONTROL Direct Call Rule]

Dans cet exemple d&#39;Audience Manager, nous allons utiliser un [!UICONTROL Direct Call rule] point pour [!DNL Launch] déclencher l&#39;accès en Audience Manager. Comme vous le verrez dans les sections suivantes, cela devient vraiment utile en définissant la valeur [!UICONTROL Data Layer] sur une nouvelle valeur, afin qu’elle puisse être récupérée par le [!UICONTROL Data Element] dans [!DNL Platform Launch].

## Page de démonstration {#demo-page}

Nous avons créé une petite page de démonstration qui montre comment modifier une valeur dans le [!DNL data layer] et l&#39;envoyer en AAM, comme vous pouvez le faire sur une page SPA. Cette fonctionnalité peut être modélisée pour des modifications plus élaborées nécessaires. Vous pouvez trouver cette page de démonstration [ICI](https://aam.enablementadobe.com/SPA-Launch.html).

## La définition de la variable [!DNL data layer] {#setting-the-data-layer}

Comme nous l’avons mentionné, lorsque du nouveau contenu est chargé sur la page ou lorsqu’une personne effectue une action sur le site, il [!DNL data layer] faut le définir dynamiquement dans l’en-tête de la page AVANT [!DNL Launch] d’appeler et d’exécuter le [!UICONTROL rules], de sorte que [!DNL Platform Launch] les nouvelles valeurs puissent être récupérées dans la [!DNL data layer] page et les mettre en Audience Manager.

Si vous allez sur le site de démonstration répertorié ci-dessus et que vous regardez la source de la page, vous verrez :

* Le [!DNL data layer] est dans l’en-tête de la page, avant l’appel à la fonction [!DNL Platform Launch]
* Le code JavaScript dans le lien de SPA simulé modifie le [!UICONTROL Data Layer], puis appelle [!DNL Platform Launch] (l’appel _satellite.track()). Si vous utilisiez des événements personnalisés JavaScript au lieu de [!UICONTROL Direct Call Rule]cela, la leçon est la même. Modifiez d’abord le [!DNL data layer], puis appelez [!DNL Launch].

>[!VIDEO](https://video.tv.adobe.com/v/23322/?quality=12)

## Ressources supplémentaires {#additional-resources}

* [SPA débat sur les forums Adobes](https://forums.adobe.com/thread/2451022)
* [Sites d’architecture de référence pour montrer comment implémenter des SPA dans le Launch by Adobe](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html)
* [Utilisation des meilleures pratiques lors du suivi des SPA dans Adobe Analytics](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html)
* [Site de démonstration utilisé pour cet article](https://aam.enablementadobe.com/SPA-Launch.html)
