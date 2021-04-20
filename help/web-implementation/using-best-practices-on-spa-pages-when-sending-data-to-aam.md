---
title: Utilisation des bonnes pratiques sur les pages SPA lors de l’envoi de données à AAM
description: Dans ce document, nous décrirons plusieurs bonnes pratiques que vous devez suivre et dont vous devez tenir compte lorsque vous envoyez des données d’applications d’une seule page (SPA) à Adobe Audience Manager (AAM). Ce document se concentrera sur l’utilisation du Launch by Adobe, qui est la méthode d’implémentation recommandée.
feature: Implementation Basics
topics: spa
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1390
topic: SPA
role: "Developer, Data Engineer"
level: Experienced
translation-type: tm+mt
source-git-commit: a7dc335e75697a7b1720eccdadbb9605fdeda798
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---


# Utilisation des bonnes pratiques sur les pages SPA lors de l’envoi de données à AAM {#using-best-practices-on-spa-pages-when-sending-data-to-aam}

Dans ce document, nous décrirons plusieurs bonnes pratiques que vous devez suivre et connaître lorsque vous envoyez des données de [!UICONTROL Single Page Applications] (SPA) à Adobe Audience Manager (AAM). Ce document se concentre sur l&#39;utilisation de [!UICONTROL Experience Platform Launch], qui est la méthode d&#39;implémentation recommandée.

## Notes initiales

* Les éléments ci-dessous vont supposer que vous utilisez [!DNL Platform Launch] pour implémenter votre site. Les considérations persistent si vous n’utilisez pas [!DNL Platform Launch], mais vous devez les adapter à votre méthode d’implémentation.
* Tous les SPA sont différents, vous devrez peut-être modifier certains des éléments suivants pour mieux répondre à vos besoins, mais nous voulions partager avec vous certaines pratiques exemplaires ; à quoi vous devez penser lorsque vous envoyez des données de SPA pages à l&#39;Audience Manager.

## Diagramme simple de travail avec les SPA et les AAM en Experience Platform Launch {#simple-diagram-of-working-with-spas-and-aam-in-experience-platform-launch}

![spa pour se détendre  [!DNL launch]](assets/spa_for_aam_in_launch.png)

>[!NOTE]
>Comme indiqué, il s&#39;agit d&#39;un diagramme simplifié de la façon dont SPA pages sont gérées dans une implémentation Adobe Audience Manager (sans Adobe Analytics) à l&#39;aide de [!DNL Platform Launch]. Comme vous pouvez le voir, c&#39;est assez direct, avec la grande décision étant comment vous allez communiquer un changement de vue (ou une action) à [!DNL Platform Launch].

## Déclenchement de [!DNL Launch] à partir de la page SPA {#triggering-launch-from-the-spa-page}

Deux des méthodes les plus courantes pour déclencher une règle dans [!DNL Platform Launch] (et par conséquent envoyer des données en Audience Manager) sont les suivantes :

* Définition de événements personnalisés JavaScript (voir l’exemple [HERE](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html) avec Adobe Analytics)
* Utilisation d&#39;un [!UICONTROL Direct Call Rule]

Dans cet exemple d’Audience Manager, nous allons utiliser [!UICONTROL Direct Call rule] dans [!DNL Launch] pour déclencher l’accès qui entre en Audience Manager. Comme vous le verrez dans les sections suivantes, cela devient vraiment utile en définissant [!UICONTROL Data Layer] sur une nouvelle valeur, de sorte qu&#39;il puisse être récupéré par [!UICONTROL Data Element] dans [!DNL Platform Launch].

## Page de démonstration {#demo-page}

Nous avons créé une petite page de démonstration qui montre comment modifier une valeur dans [!DNL data layer] et l&#39;envoyer en AAM, comme vous pouvez le faire sur une page SPA. Cette fonctionnalité peut être modélisée pour des modifications plus élaborées nécessaires. Vous pouvez trouver cette page de démonstration [ICI](https://aam.enablementadobe.com/SPA-Launch.html).

## La définition de la variable [!DNL data layer] {#setting-the-data-layer}

Comme nous l&#39;avons mentionné, lorsque du nouveau contenu est chargé sur la page ou lorsqu&#39;une personne effectue une action sur le site, [!DNL data layer] doit être défini dynamiquement dans l&#39;en-tête de la page AVANT que [!DNL Launch] ne soit appelé et exécute [!UICONTROL rules], de sorte que [!DNL Platform Launch] puisse récupérer les nouvelles valeurs de [!DNL data layer] et les mettre en Audience Manager.

Si vous allez sur le site de démonstration répertorié ci-dessus et que vous regardez la source de la page, vous verrez :

* Le [!DNL data layer] se trouve dans l&#39;en-tête de la page, avant l&#39;appel à [!DNL Platform Launch]
* Le code JavaScript du lien SPA simulé modifie [!UICONTROL Data Layer], puis appelle [!DNL Platform Launch] (l’appel _satellite.track()). Si vous utilisiez des événements personnalisés JavaScript au lieu de [!UICONTROL Direct Call Rule], la leçon est la même. Modifiez d&#39;abord [!DNL data layer], puis appelez [!DNL Launch].

>[!VIDEO](https://video.tv.adobe.com/v/23322/?quality=12)

## Ressources supplémentaires {#additional-resources}

* [SPA débat sur les forums Adobes](https://forums.adobe.com/thread/2451022)
* [Sites d’architecture de référence pour montrer comment implémenter des SPA dans le Launch by Adobe](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html)
* [Utilisation des meilleures pratiques lors du suivi des SPA dans Adobe Analytics](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html)
* [Site de démonstration utilisé pour cet article](https://aam.enablementadobe.com/SPA-Launch.html)
