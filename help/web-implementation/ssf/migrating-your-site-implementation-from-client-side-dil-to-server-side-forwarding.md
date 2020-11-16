---
title: Migration de l’implémentation AAM votre site du DIL côté client vers le transfert côté serveur
description: Ce didacticiel s’applique à vous si vous avez à la fois Adobe Audience Manager (AAM) et Adobe Analytics, et que vous envoyez actuellement un accès de la page à AAM à l’aide du code "DIL" (Data Integration Library), ainsi qu’un accès de la page à Adobe Analytics. Puisque vous disposez de ces deux solutions et qu’elles font toutes deux partie du Adobe Experience Cloud, vous avez la possibilité de suivre la bonne pratique consistant à activer le transfert côté serveur (SSF), qui permet aux serveurs de collecte de données Analytics de transférer les données d’analyse du site en temps réel vers l’Audience Manager, plutôt que de faire envoyer un accès supplémentaire de la page vers AAM au code côté client. Ce didacticiel vous explique comment passer de l’ancienne mise en oeuvre du DIL côté client à la nouvelle méthode de transfert côté serveur.
product: audience manager, analytics
feature: integration with analytics
topics: null
audience: implementer
activity: implement
doc-type: tutorial
team: Technical Marketing
kt: 1778
translation-type: tm+mt
source-git-commit: 133279f589bd58aef36a980c2b7248ae00fd9496
workflow-type: tm+mt
source-wordcount: '2319'
ht-degree: 0%

---


# Migration de l’implémentation AAM de votre site du [!DNL Client-Side] DIL vers [!DNL Server-Side Forwarding] {#migrating-your-site-s-aam-implementation-from-client-side-dil-to-server-side-forwarding}

Ce didacticiel s’applique à vous si vous avez à la fois Adobe Audience Manager (AAM) et Adobe Analytics, et que vous envoyez actuellement un accès de la page à AAM à l’aide du code &quot;DIL&quot; ([!DNL Data Integration Library]), ainsi qu’un accès de la page à Adobe Analytics. Puisque vous disposez de ces deux solutions et qu’elles font toutes deux partie de la Adobe Experience Cloud, vous avez la possibilité de suivre la bonne pratique consistant à activer &quot;[!DNL Server-Side Forwarding] (SSF)&quot;, ce qui permet aux serveurs de collecte de [!DNL Analytics] données de transférer les données d’analyse du site en temps réel à l’Audience Manager, au lieu d’avoir [!DNL client-side] du code pour envoyer un accès supplémentaire de la page à l’AAM. Ce didacticiel vous guide tout au long des étapes permettant de passer de l’ancienne mise en oeuvre &quot;[!DNL Client-Side DIL]&quot; à la nouvelle méthode &quot;[!DNL Server-Side forwarding]&quot;.

## [!DNL Client-Side] (DIL) ou [!DNL Server-Side] {#client-side-dil-vs-server-side}

Lors de la comparaison et de la comparaison de ces deux méthodes d’obtention de données Adobe Analytics en AAM, il peut s’avérer utile de visualiser les différences dans l’image suivante :

![côté client vers côté serveur](assets/client-side_vs_server-side_aam_implementation.png)

### [!DNL Client-side] Mise en oeuvre DIL {#client-side-dil-implementation}

Si vous utilisez cette méthode pour obtenir des données Adobe Analytics dans AAM, cela signifie que vous avez deux accès provenant de vos pages Web : L&#39;un va à [!DNL Analytics]l&#39;AAM, l&#39;autre à l&#39;(après avoir copié les [!DNL Analytics] données sur la page Web. [!UICONTROL Segments] sont renvoyés d’AAM à la page, où ils peuvent être utilisés pour la personnalisation, etc. Il s’agit d’une mise en oeuvre &quot;héritée&quot; et n’est plus recommandé.

Outre le fait qu&#39;il ne s&#39;agit pas de pratiques exemplaires, l&#39;utilisation de cette méthode présente les inconvénients suivants :

* Deux accès provenant de la page au lieu d’un seul
* [!UICONTROL Server-Side Forwarding] est requis pour le partage en temps réel des audiences AAM à [!DNL Analytics], de sorte que [!DNL Client-side] les implémentations ne permettent pas cette fonctionnalité (et potentiellement d’autres fonctionnalités dans le futur)

Il est recommandé de passer à une [!UICONTROL Server-Side Forwarding] méthode d’implémentation AAM.

### [!UICONTROL Server-Side Forwarding]Implémentation{#server-side-forwarding-implementation}

Comme le montre l&#39;image ci-dessus, un accès vient de la page Web à Adobe Analytics. [!DNL Analytics] transfère ensuite ces données à l’AAM en temps réel, et les visiteurs sont évalués en AAM [!UICONTROL traits] et [!UICONTROL segments], comme si l’accès provenait directement de la page.

[!UICONTROL Segments] sont renvoyés lors du même accès en temps réel à [!DNL Analytics], qui renvoie la réponse à la page Web pour la personnalisation, etc.

Le transfert côté serveur ne présente aucun inconvénient temporel. Nous recommandons vivement à toute personne qui possède à la fois une Audience Manager et qui [!DNL Analytics] utilise cette méthode d’implémentation.

## Vous Avez DEUX Tâches Principales {#you-have-two-main-tasks}

Il y a pas mal d&#39;informations sur cette page, et c&#39;est important, bien sûr. Cependant, **tout se résume à deux choses principales à faire**:

1. Changez votre code du code [!DNL Client-Side] DIL en [!UICONTROL Server-Side Forwarding] code
1. Bascule le commutateur dans le [!DNL Analytics][!DNL Admin Console] pour début du transfert réel des données (par [!UICONTROL report suite])

Si vous ignorez l’un ou l’autre de ces deux paramètres, SSF ne fonctionnera pas correctement. Des étapes et des données supplémentaires ont été ajoutées à ce document pour vous aider à effectuer ces deux étapes correctement pour votre configuration.

## Options d’implémentation {#implementation-options}

Au fur et à mesure que vous passez [!DNL client-side] à [!DNL server-side], l&#39;une des tâches que vous aurez est de changer le code en nouveau [!UICONTROL Server-Side Forwarding] code. Pour ce faire, utilisez l’une des options suivantes :

* Adobe Experience Platform Launch - Notre option d&#39;implémentation recommandée pour les propriétés Web. Vous verrez que c&#39;est une tâche très facile, comme [!DNL Launch] vous l&#39;avez fait pour vous.
* Sur la page - Vous pouvez également placer le nouveau code SSF directement dans la `doPlugins` fonction à l&#39;intérieur de votre [!DNL appMeasurement.js] fichier, si vous n&#39;utilisez pas (encore) le lancement d&#39;Adobe.
* Autres gestionnaires de balises : ils peuvent être traités comme l’option précédente (Sur la page), car vous allez toujours placer le code SSF dans `doPlugins`l’emplacement où l’autre gestionnaire de balises stocke le [!DNL AppMeasurement] code.

Nous allons examiner chacun de ces éléments ci-dessous dans la section Mise à jour du code.

## Procédure de mise en œuvre {#implementation-steps}

### Étape 0 : Condition préalable : Service d’identification des Experience Cloud (ECID) {#step-prerequisite-experience-cloud-id-service-ecid}

La principale condition préalable pour passer à [!UICONTROL Server-Side Forwarding] est la mise en oeuvre du service d’identification des Experience Cloud. Cela est plus facile si vous utilisez l&#39;Experience Platform Launch, auquel cas vous installez simplement l&#39;extension ECID et cela fera le reste.

Si vous utilisez un TMS non Adobe, ou aucun TMS du tout, implémentez l&#39;ECID pour qu&#39;il s&#39;exécute **avant** toute autre solution d&#39;Adobe. Consultez la documentation [](https://marketing.adobe.com/resources/help/fr_FR/mcvid/) ECID pour plus de détails. Le seul autre prérequis concerne les versions de code, de sorte que, comme vous appliquez simplement les versions les plus récentes du code dans les étapes suivantes, vous vous en sortirez bien.

>[!NOTE]
>
>Veuillez lire ce document entier avant de procéder à la mise en oeuvre. La section &quot;Minutage&quot; ci-dessous contient des informations importantes sur le *moment* auquel vous devez mettre en oeuvre chaque élément, y compris l&#39;ECID (s&#39;il n&#39;est pas encore mis en oeuvre).

### Étape 1 : Enregistrer les options actuellement utilisées à partir du code DIL {#step-record-currently-used-options-from-dil-code}

Lorsque vous vous préparez à passer du code du [!DNL Client-Side] DIL à [!UICONTROL Server-Side Forwarding]la première étape consiste à identifier tout ce que vous faites avec le code du DIL, y compris les paramètres personnalisés et les données envoyées à l&#39;AAM. Voici les points à prendre en compte :

* Les [!DNL Analytics] variables normales, à l’aide du module [!DNL siteCatalyst.init] DIL - Vous n’aurez pas à vous inquiéter de celle-ci, parce que son travail est juste d’envoyer les [!DNL Analytics] variables normales, et cela se fera simplement en ayant SSF activé.
* Sous-domaine partenaire : dans la fonction DIL.create, notez le `partner` paramètre. Il s’agit de votre &quot;sous-domaine partenaire&quot;, ou parfois de votre &quot;identifiant partenaire&quot;, qui sera nécessaire lorsque vous placerez le nouveau code SSF.
* [!DNL Visitor Service Namespace] - Également appelé &quot;[!DNL Org ID]&quot; ou &quot;[!DNL IMS Org ID]&quot;, vous en aurez également besoin lorsque vous configurerez le nouveau code SSF. En prends note.
* containerNSID, uuidCookie et d&#39;autres options avancées : notez les options avancées supplémentaires que vous utilisez afin de pouvoir les définir également dans le code SSF.
* Variables de page supplémentaires - Si d&#39;autres variables sont envoyées à l&#39;AAM à partir de la page (en plus des [!DNL Analytics] variables normales gérées par siteCatalyst.init), vous devez en prendre note afin qu&#39;elles puissent être envoyées via SSF (spoiler alert : par [!DNL contextData] le biais de variables).

### Étape 2 : Mise à jour du code {#step-updating-the-code}

Dans la section ci-dessus intitulée &quot;Options d’implémentation&quot;, plusieurs options sont fournies concernant la manière et l’emplacement de la mise en oeuvre [!UICONTROL Server-Side Forwarding]. Pour que cette section soit efficace, nous devons la diviser en deux sections (dont deux sont combinées). Accédez à la méthode de cette section qui décrit le mieux vos besoins.

#### Adobe Experience Platform Launch {#launch-by-adobe}

Regardez la vidéo ci-dessous pour en savoir plus sur le déplacement des options de mise en oeuvre du code du [!DNL Client-Side] DIL vers [!UICONTROL Server-Side Forwarding] l’Experience Platform Launch.

>[!VIDEO](https://video.tv.adobe.com/v/26310/?quality=12)

#### &quot;Sur la page&quot; ou non-Adobe Tag Manager {#on-the-page-or-non-adobe-tag-manager}

Regardez la vidéo ci-dessous pour en savoir plus sur le déplacement des options d’implémentation du code du [!DNL Client-Side] DIL [!UICONTROL Server-Side Forwarding] dans le code [!DNL AppMeasurement] , résidant dans un fichier ou dans un système de gestion des balises non Adobe.

>[!VIDEO](https://video.tv.adobe.com/v/26312/?quality=12)

### Étape 3 : Activation du transfert (par [!UICONTROL Report Suite]défaut) {#step-enabling-the-forwarding-per-report-suite}

Jusqu&#39;à présent dans ce tutoriel nous avons passé tout notre temps à changer le code du [!DNL Client-Side DIL] code au [!UICONTROL Server-Side Forwarding]. C&#39;est bien, parce que c&#39;est la partie la plus difficile. Cette section, bien que vous verrez qu&#39;elle est très facile, est tout aussi importante que la mise à jour du code. Dans cette vidéo, vous verrez comment basculer le commutateur qui permet le transfert réel des données d’Analytics vers l’Audience Manager.

>[!VIDEO](https://video.tv.adobe.com/v/26355/?quality-12)

**REMARQUE :** Comme indiqué dans la vidéo, n&#39;oubliez pas qu&#39;il faudra jusqu&#39;à 4 heures pour que l&#39;activation du transfert soit entièrement mise en oeuvre sur le serveur principal Experience Cloud.

## Minutage {#timing}

Pour rappel, il existe deux tâches principales pour passer d&#39; [!DNL Client-Side DIL] à [!UICONTROL Server-Side Forwarding]:

1. Mise à jour du code
1. Faire basculer le commutateur dans la fonction [!DNL Analytics] [!DNL Admin Console]

Mais la question est, laquelle faites-vous en premier ? Est-ce important ? OK, désolé, c&#39;était deux questions. Mais les réponses sont... ça dépend, et oui, ça *peut* compter. Comment cela est-il vague ? Partageons-le. Mais d&#39;abord une question supplémentaire qui peut se poser si vous êtes une grande organisation avec beaucoup de sites : Dois-je tout faire en même temps ? Celle-là est un peu plus facile. Non. Vous pouvez le faire morceau par morceau... en quelque sorte. :)

### Un peu plus profond {#a-little-deeper-dive}

La raison pour laquelle le timing et la commande sont importants est la façon dont le transfert *fonctionne vraiment, ce qui peut être résumé dans les quelques faits techniques suivants :

* Si le service d’identification des Experience Cloud (ECID) est mis en oeuvre et que le commutateur est activé dans le [!DNL Analytics][!DNL Admin Console] (&quot;le commutateur&quot;), les données seront transférées de [!DNL Analytics] à AAM, même si vous n’avez pas encore mis à jour le code.
* Si l&#39;ECID n&#39;est pas implémenté, les données ne seront pas transférées, même si le commutateur est activé et que le code SSF est activé.
* Le code SSF (que ce soit dans [!DNL Launch] ou sur la page) traite réellement la réponse et est bien sûr nécessaire pour terminer la migration.
* N&#39;oubliez pas que le commutateur SSF est activé par [!UICONTROL Report Suite], mais que le code est géré par propriété dans [!DNL Launch]ou par [!DNL AppMeasurement] fichier si vous n&#39;utilisez pas [!DNL Launch]

### Bonnes pratiques {#best-practices}

Sur la base de ces détails techniques, voici les recommandations concernant le calendrier de &quot;quoi faire quand&quot; :

#### Si vous n’avez PAS encore implémenté ECID {#if-you-do-not-have-ecid-yet-implemented}

1. Retourner le commutateur [!DNL Analytics] pour chaque [!UICONTROL report suite] que vous activez pour SSF

   1. Le transfert ne sera pas encore début car vous n’avez pas ECID

1. Par site, mettez à jour votre code [!DNL Client-Side DIL] au format SSF (il peut s’agir de [!DNL Launch] ou de la page, comme expliqué dans une autre section ci-dessus).

   1. Désormais, le transfert s’effectue (comme vous avez ajouté l’ECID) et vous devriez également recevoir une réponse JSON appropriée à votre [!DNL Analytics] balise (voir la section Validation et dépannage ci-dessous pour plus d’informations).

#### Si ECID est implémenté {#if-you-do-have-ecid-implemented}

1. Préparez et planifiez pour que vous soyez prêt à mettre à jour votre code du DIL vers SSF PAR [!UICONTROL report suite] que vous activez pour SSF :

   1. Basculer le commutateur [!DNL Analytics] pour activer SSF

      1. Transfert WILL début car l&#39;ECID est activé
   1. Dans les plus brefs délais, mettez à jour votre code [!DNL Client-Side DIL] vers SSF (il peut s’agir de [!DNL Launch] ou de la page, comme expliqué dans une autre section ci-dessus).

      1. Vous devez recevoir une réponse JSON appropriée à votre [!DNL Analytics] balise (voir la section Validation et dépannage ci-dessous pour plus de détails).


**NOTE 1 :** Il est important de faire ces deux étapes aussi près que possible, car entre les étapes 1 et 2 ci-dessus, vous aurez la duplication des données en AAM. En d’autres termes, SSF aura commencé à envoyer des données de [!DNL Analytics] à l’AAM, et comme le code du DIL est toujours sur la page, il y aura également un accès allant directement de la page à l’AAM, doublant ainsi les données. Dès que vous mettez à jour le code du DIL vers SSF, cela sera allégé.

**NOTE 2 :** Si vous préférez une légère incohérence des données plutôt qu’une petite duplication des données, vous pouvez changer l’ordre des étapes 1 et 2 ci-dessus. Si vous déplacez le code du DIL vers SSF, le flux de données vers l&#39;AAM s&#39;arrêterait jusqu&#39;à ce que vous puissiez inverser le commutateur pour activer le SSF pour le [!UICONTROL report suite]fichier. En règle générale, les clients préfèrent avoir un petit doublement de données plutôt que de ne pas avoir à faire entrer les visiteurs dans [!UICONTROL traits] et [!UICONTROL segments].

#### Minutage de la migration lorsque vous disposez de plusieurs sites et [!UICONTROL Report Suites] {#migration-timing-when-you-have-many-sites-and-report-suites}

Cette question est brièvement abordée dans les sections précédentes, en ce sens que la stratégie principale peut être résumée comme suit :

Migrez un site/[!UICONTROL report suite] (ou groupe de sites/[!UICONTROL report suites]) à la fois.

Cependant, cela peut se révéler délicat en fonction de quelques scénarios possibles :

* Vous disposez d’un site qui contient plusieurs éléments distincts. [!UICONTROL report suites]
* Vous disposez d’un [!UICONTROL report suite] qui comprend plusieurs sites (par exemple, un site global [!UICONTROL report suite]).
* Vous utilisez une [!DNL Launch] propriété pour couvrir plusieurs sites.
* Vous avez différentes équipes de développement pour différents sites

A cause de ces éléments, ça peut devenir un peu compliqué. Les meilleures choses que je puisse suggérer sont les suivantes :

* Prenez le temps d&#39;élaborer une stratégie de migration vers le SSF, en fonction des éléments décrits ci-dessus.
* En vous basant sur le fait qu&#39;une seule propriété dans [!DNL Launch] (ou un seul [!DNL AppMeasurement] fichier) correspond généralement à 1 ou 2 propriétés distinctes [!UICONTROL report suites], vous serez probablement en mesure de faire un plan qui fonctionne sur ces groupes distincts un par un, mettant à jour votre entreprise au format SSF.
* Si vous travaillez avec Adobe Consulting, contactez-les au sujet de votre plan de migration afin qu’ils puissent vous aider au besoin.

## Validation et dépannage {#validation-and-troubleshooting}

La méthode principale pour vérifier que le [!UICONTROL Server-Side Forwarding] programme est en cours d’exécution consiste à examiner la réponse à n’importe quel accès Adobe Analytics provenant de l’application.

Si vous ne faites pas [!UICONTROL server-side forwarding] de données de [!DNL Analytics] à l&#39;Audience Manager, il n&#39;y a vraiment pas de réponse à la [!DNL Analytics] balise (à part un pixel 2x2). Cependant, si vous utilisez SSF, il y a des éléments que vous pouvez vérifier dans la [!DNL Analytics] demande et la réponse qui vous informeront que [!DNL Analytics] la communication avec l’Audience Manager est correcte, que vous pouvez transférer l’accès et obtenir une réponse.

>[!VIDEO](https://video.tv.adobe.com/v/26359/?quality=12)

**AVERTISSEMENT :** Méfiez-vous du faux &quot;succès&quot; - S&#39;il y a une réponse et que tout semble fonctionner, assurez-vous que vous avez l&#39;objet &quot;machin&quot; dans la réponse. Si vous ne le faites pas, vous verrez peut-être un message qui dit [!DNL "status":"SUCCESS"]. Aussi fou que cela paraisse, c&#39;est en fait BAT qu&#39;il ne fonctionne PAS correctement. Si vous voyez cela, cela signifie que vous avez terminé la mise à jour du code dans [!DNL Launch] ou [!DNL AppMeasurement], mais que le transfert dans le [!DNL Analytics] [!DNL Admin Console] n&#39;est pas encore terminé. Dans ce cas, vous devez vérifier que vous avez activé SSF dans le [!DNL Analytics][!DNL Admin Console] pour votre [!UICONTROL report suite]application. Si vous l&#39;avez fait, et cela n&#39;a pas encore été 4 heures, soyez patient, car cela peut prendre autant de temps pour apporter tous les changements nécessaires sur le serveur principal.

![faux succès](assets/falsesuccess.png)

For more information about [!UICONTROL Server-Side Forwarding], please see the [documentation](https://marketing.adobe.com/resources/help/en_US/reference/ssf.html).
