---
title: Utilisation des bonnes pratiques sur SPA pages lors de l’envoi de données à AAM
description: Dans ce document, nous décrirons plusieurs bonnes pratiques que vous devez suivre et connaître lorsque vous envoyez des données d’applications d’une seule page (SPA) à Adobe Audience Manager (AAM). Ce document se concentre sur l’utilisation de Launch by Adobe, qui est la méthode de mise en oeuvre recommandée.
feature: Principes de mise en oeuvre
topics: spa
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1390
topic: SPA
role: Developer, Data Engineer
level: Experienced
exl-id: 99ec723a-dd56-4355-a29f-bd6d2356b402
source-git-commit: 4b91696f840518312ec041abdbe5217178aee405
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# Utilisation des bonnes pratiques sur SPA pages lors de l’envoi de données à AAM {#using-best-practices-on-spa-pages-when-sending-data-to-aam}

Dans ce document, nous décrirons plusieurs bonnes pratiques que vous devez suivre et connaître lorsque vous envoyez des données de [!UICONTROL Single Page Applications] (SPA) à Adobe Audience Manager (AAM). Ce document se concentre sur l’utilisation de [!UICONTROL Experience Platform Launch], qui est la méthode de mise en oeuvre recommandée.

## Notes initiales

* Les éléments ci-dessous supposent que vous utilisez [!DNL Platform Launch] pour implémenter sur votre site. Les considérations persistent si vous n’utilisez pas [!DNL Platform Launch], mais vous devez les adapter à votre méthode de mise en oeuvre.
* Tous les SPA sont différents. Vous devrez peut-être donc ajuster certains des éléments suivants pour répondre le mieux à vos besoins, mais nous avons voulu partager certaines bonnes pratiques avec vous. ce à quoi vous devez réfléchir pendant l’envoi de données de SPA pages vers l’Audience Manager.

## Schéma simple de l’utilisation de SPA et d’AAM dans Experience Platform Launch {#simple-diagram-of-working-with-spas-and-aam-in-experience-platform-launch}

![spa pour aam in  [!DNL launch]](assets/spa_for_aam_in_launch.png)

>[!NOTE]
>Comme indiqué, il s’agit d’un diagramme simplifié de la manière dont SPA pages sont traitées dans une mise en oeuvre Adobe Audience Manager (sans Adobe Analytics) à l’aide de [!DNL Platform Launch]. Comme vous pouvez le voir, c&#39;est assez simple, avec la grande décision étant comment vous allez communiquer un changement d&#39;affichage (ou une action) à [!DNL Platform Launch].

## Déclenchement de [!DNL Launch] à partir de la page SPA {#triggering-launch-from-the-spa-page}

Deux des méthodes les plus courantes pour déclencher une règle dans [!DNL Platform Launch] (et donc envoyer des données en Audience Manager) sont les suivantes :

* Définition d’événements personnalisés JavaScript (voir l’exemple [HERE](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html) avec Adobe Analytics)
* Utilisation d’un [!UICONTROL Direct Call Rule]

Dans cet exemple d’Audience Manager, nous allons utiliser une balise [!UICONTROL Direct Call rule] dans [!DNL Launch] pour déclencher l’accès vers l’Audience Manager. Comme vous le verrez dans les sections suivantes, cela devient vraiment utile en définissant [!UICONTROL Data Layer] sur une nouvelle valeur, afin qu’elle puisse être récupérée par la balise [!UICONTROL Data Element] dans [!DNL Platform Launch].

## Page de démonstration {#demo-page}

Nous avons créé une petite page de démonstration qui montre comment modifier une valeur dans [!DNL data layer] et l’envoyer dans AAM, comme vous pouvez le faire sur une page SPA. Cette fonctionnalité peut être modélisée pour des modifications plus élaborées nécessaires. Vous trouverez cette page de démonstration [ICI](https://aam.enablementadobe.com/SPA-Launch.html).

## La définition de la variable [!DNL data layer] {#setting-the-data-layer}

Comme mentionné, lorsque du nouveau contenu est chargé sur la page ou lorsqu’une personne effectue une action sur le site, la balise [!DNL data layer] doit être définie dynamiquement dans l’en-tête de la page AVANT que [!DNL Launch] ne soit appelée et exécute la balise [!UICONTROL rules], de sorte que [!DNL Platform Launch] puisse sélectionner les nouvelles valeurs de la balise [!DNL data layer] et les envoyer en Audience Manager.

Si vous accédez au site de démonstration répertorié ci-dessus et que vous consultez la source de la page, vous verrez :

* [!DNL data layer] se trouve dans l’en-tête de la page, avant l’appel à [!DNL Platform Launch]
* Le code JavaScript du lien de SPA simulé modifie la balise [!UICONTROL Data Layer], puis appelle [!DNL Platform Launch] (l’appel _satellite.track() ). Si vous utilisiez des événements personnalisés JavaScript au lieu de cette [!UICONTROL Direct Call Rule], la leçon est la même. Modifiez d’abord [!DNL data layer], puis appelez [!DNL Launch].

>[!VIDEO](https://video.tv.adobe.com/v/23322/?quality=12)

## Ressources supplémentaires {#additional-resources}

* [SPA discussion sur les forums de l&#39;Adobe](https://forums.adobe.com/thread/2451022)
* [Sites d’architecture de référence pour montrer comment mettre en oeuvre SPA dans Launch by Adobe](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html)
* [Utilisation des bonnes pratiques lors du suivi des SPA dans Adobe Analytics](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html)
* [Site de démonstration utilisé pour cet article](https://aam.enablementadobe.com/SPA-Launch.html)
