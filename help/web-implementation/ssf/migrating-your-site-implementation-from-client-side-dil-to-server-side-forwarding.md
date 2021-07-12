---
title: Migration de l’implémentation AAM de votre site du DIL côté client vers le transfert côté serveur
description: Ce tutoriel s’applique à vous si vous disposez à la fois de Adobe Audience Manager (AAM) et d’Adobe Analytics. Vous envoyez actuellement un accès de la page à AAM à l’aide du code "DIL" (Data Integration Library) et envoyez également un accès de la page à Adobe Analytics. Puisque vous disposez de ces deux solutions et qu’elles font toutes deux partie de Adobe Experience Cloud, vous avez la possibilité de suivre la bonne pratique consistant à activer le transfert côté serveur (SSF), qui permet aux serveurs de collecte de données Analytics de transférer les données d’analyse de site en temps réel vers l’Audience Manager, au lieu d’avoir un code côté client qui envoie un accès supplémentaire de la page à AAM. Ce tutoriel vous guide tout au long des étapes permettant de passer de l’ancienne mise en oeuvre du "DIL côté client" à la nouvelle méthode de "transfert côté serveur".
product: audience manager
feature: Intégration d’Adobe Analytics
topics: null
activity: implement
doc-type: tutorial
team: Technical Marketing
kt: 1778
role: Developer, Data Engineer
level: Intermediate
exl-id: bcb968fb-4290-4f10-b1bb-e9f41f182115
source-git-commit: 4b91696f840518312ec041abdbe5217178aee405
workflow-type: tm+mt
source-wordcount: '2322'
ht-degree: 0%

---

# Migration de l’implémentation AAM de votre site du DIL [!DNL Client-Side] vers [!DNL Server-Side Forwarding] {#migrating-your-site-s-aam-implementation-from-client-side-dil-to-server-side-forwarding}

Ce tutoriel s’applique à vous si vous disposez à la fois de Adobe Audience Manager (AAM) et d’Adobe Analytics. Vous envoyez actuellement un accès de la page à AAM à l’aide du code &quot;DIL&quot; ([!DNL Data Integration Library]) et envoyez également un accès de la page à Adobe Analytics. Puisque vous disposez de ces deux solutions et qu’elles font toutes deux partie de Adobe Experience Cloud, vous avez la possibilité de suivre la bonne pratique d’activation de &quot;[!DNL Server-Side Forwarding] (SSF)&quot;, qui permet aux serveurs de collecte de données [!DNL Analytics] de transférer les données d’analyse de site en temps réel vers l’Audience Manager, au lieu d’avoir du code [!DNL client-side] qui envoie un accès supplémentaire de la page à AAM. Ce tutoriel vous guide tout au long des étapes permettant de passer de l’ancienne mise en oeuvre &quot;[!DNL Client-Side DIL]&quot; à la nouvelle méthode &quot;[!DNL Server-Side forwarding]&quot;.

## [!DNL Client-Side] (DIL) ou  [!DNL Server-Side] {#client-side-dil-vs-server-side}

Lors de la comparaison et de la comparaison de ces deux méthodes pour obtenir des données Adobe Analytics dans AAM, il peut s’avérer utile de visualiser les différences dans l’image suivante :

![côté client vers côté serveur](assets/client-side_vs_server-side_aam_implementation.png)

### [!DNL Client-side] Mise en oeuvre du DIL {#client-side-dil-implementation}

Si vous utilisez cette méthode pour obtenir des données Adobe Analytics dans AAM, deux accès provenant de vos pages web sont nécessaires : L’une se rend à [!DNL Analytics] et l’autre à l’AAM (après avoir copié les données [!DNL Analytics] sur la page Web. [!UICONTROL Segments] sont renvoyés d’AAM à la page, où ils peuvent être utilisés pour la personnalisation, etc. Cette implémentation est considérée comme &quot;héritée&quot; et n’est plus recommandée.

Outre le fait qu’il ne s’agit pas de suivre les bonnes pratiques, l’utilisation de cette méthode présente les inconvénients suivants :

* Deux accès provenant de la page au lieu d’un seul
* [!UICONTROL Server-Side Forwarding] est requis pour le partage en temps réel des audiences d’AAM vers  [!DNL Analytics], de sorte que les  [!DNL Client-side] mises en oeuvre ne permettent pas cette fonctionnalité (et potentiellement d’autres fonctionnalités à l’avenir).

Il est recommandé de passer à une méthode [!UICONTROL Server-Side Forwarding] d’AAM de mise en oeuvre.

### [!UICONTROL Server-Side Forwarding] Mise en œuvre {#server-side-forwarding-implementation}

Comme illustré dans l’image ci-dessus, un accès provient de la page Web vers Adobe Analytics. [!DNL Analytics] transfère ensuite ces données à AAM en temps réel et les visiteurs sont évalués en AAM  [!UICONTROL traits] et  [!UICONTROL segments], comme si l’accès provenait directement de la page.

[!UICONTROL Segments] sont renvoyés lors du même accès en temps réel à  [!DNL Analytics], qui transfère la réponse vers la page Web pour la personnalisation, etc.

Il n’y a aucun inconvénient à ce que le transfert côté serveur soit effectué. Nous recommandons vivement à toute personne disposant à la fois d’une Audience Manager et d’[!DNL Analytics] d’utiliser cette méthode de mise en oeuvre.

## Vous Avez Deux Tâches Principales {#you-have-two-main-tasks}

Il y a pas mal d&#39;informations sur cette page, et c&#39;est important, bien sûr. Cependant, il se résume **à deux choses principales que vous devez faire** :

1. Remplacez votre code de [!DNL Client-Side] code de DIL par [!UICONTROL Server-Side Forwarding] code  .
1. Retourner le commutateur dans [!DNL Analytics] [!DNL Admin Console] pour lancer le transfert réel des données (par [!UICONTROL report suite]).

Si vous ignorez l’un de ces deux paramètres, le transfert côté serveur ne fonctionnera pas correctement. Des étapes et des données supplémentaires ont été ajoutées à ce document pour vous aider à effectuer ces deux étapes correctement pour votre configuration.

## Options d’implémentation {#implementation-options}

Lorsque vous passez de [!DNL client-side] à [!DNL server-side], l’une des tâches qui s’affiche est de remplacer le code par le nouveau code [!UICONTROL Server-Side Forwarding]. Pour ce faire, utilisez l’une des options suivantes :

* Adobe Experience Platform Launch : option de mise en oeuvre recommandée pour les propriétés web. Vous verrez que c&#39;est une tâche très facile, car [!DNL Launch] a fait toutes les choses difficiles pour vous.
* Sur la page : vous pouvez également placer le nouveau code SSF directement dans la fonction `doPlugins` à l’intérieur de votre fichier [!DNL appMeasurement.js], si vous n’utilisez pas (encore) Adobe Launch.
* Autres gestionnaires de balises : ils peuvent être traités comme l’option précédente (Sur la page), car vous allez toujours placer le code SSF dans `doPlugins`, où l’autre gestionnaire de balises stocke le code [!DNL AppMeasurement].

Chacune de ces informations est examinée dans la section Mise à jour du code .

## Procédure d’implémentation {#implementation-steps}

### Étape 0 : Condition requise : Service d’ID Experience Cloud (ECID) {#step-prerequisite-experience-cloud-id-service-ecid}

La condition principale pour passer à [!UICONTROL Server-Side Forwarding] est de mettre en oeuvre le service d’ID Experience Cloud. Cela est plus facile si vous utilisez Experience Platform Launch, auquel cas vous installez simplement l’extension ECID et cela fera le reste.

Si vous utilisez un TMS non Adobe, ou aucun TMS du tout, implémentez ECID pour exécuter **avant** toute autre solution d’Adobe. Pour plus d’informations, voir la [documentation ECID](https://marketing.adobe.com/resources/help/fr_FR/mcvid/) . La seule autre condition préalable concerne les versions de code. Par conséquent, comme vous appliquez simplement les versions les plus récentes du code dans les étapes suivantes, tout ira bien.

>[!NOTE]
>
>Veuillez lire l’intégralité de ce document avant de procéder à l’implémentation. La section &quot;Minutage&quot; ci-dessous contient des informations importantes sur *quand* vous devez implémenter chaque élément, y compris l’ECID (s’il n’est pas encore implémenté).

### Étape 1 : Enregistrer les options actuellement utilisées du code DIL {#step-record-currently-used-options-from-dil-code}

Lorsque vous vous préparez à passer du code du DIL [!DNL Client-Side] à [!UICONTROL Server-Side Forwarding], la première étape consiste à identifier tout ce que vous faites avec le code du DIL, y compris les paramètres personnalisés et les données envoyées à AAM. Voici quelques éléments à noter et à prendre en compte :

* Variables [!DNL Analytics] normales, à l’aide du module de DIL [!DNL siteCatalyst.init] - Vous n’aurez pas à vous soucier de celle-ci, car sa tâche consiste simplement à envoyer les variables [!DNL Analytics] normales, ce qui se produira simplement en activant le transfert côté serveur.
* Sous-domaine du partenaire : dans la fonction DIL.create, notez le paramètre `partner`. Il s’agit de votre &quot;sous-domaine partenaire&quot;, ou parfois de votre &quot;identifiant partenaire&quot;, qui sera nécessaire lorsque vous placerez le nouveau code SSF.
* [!DNL Visitor Service Namespace] - Également appelé &quot;[!DNL Org ID]&quot; ou &quot;[!DNL IMS Org ID]&quot;, vous en aurez également besoin lorsque vous configurerez le nouveau code SSF. Fais-en une note !
* containerNSID, uuidCookie et autres options avancées - Notez toutes les options avancées supplémentaires que vous utilisez afin que vous puissiez les définir également dans le code SSF.
* Variables de page supplémentaires : si d’autres variables sont envoyées à l’AAM à partir de la page (en plus des variables [!DNL Analytics] normales gérées par siteCatalyst.init), vous devez en prendre note afin qu’elles puissent être envoyées via SSF (alerte de spoiler : via les variables [!DNL contextData]).

### Étape 2 : Mise à jour du code {#step-updating-the-code}

Dans la section ci-dessus intitulée &quot;Options d’implémentation&quot;, plusieurs options sont fournies concernant la manière/l’emplacement de l’implémentation de [!UICONTROL Server-Side Forwarding]. Pour que cette section soit efficace, nous devons la diviser en deux sections (dont deux combinées). Accédez à la méthode de cette section qui décrit le mieux vos besoins.

#### Adobe Experience Platform Launch {#launch-by-adobe}

Regardez la vidéo ci-dessous pour en savoir plus sur le déplacement des options de mise en oeuvre du code du DIL [!DNL Client-Side] vers [!UICONTROL Server-Side Forwarding] en Experience Platform Launch.

>[!VIDEO](https://video.tv.adobe.com/v/26310/?quality=12)

#### &quot;Sur la page&quot; ou hors d’Adobe Tag Manager {#on-the-page-or-non-adobe-tag-manager}

Regardez la vidéo ci-dessous pour en savoir plus sur le déplacement des options de mise en oeuvre du code du DIL [!DNL Client-Side] vers [!UICONTROL Server-Side Forwarding] dans le code [!DNL AppMeasurement], résidant dans un fichier ou dans un système de gestion des balises non Adobe.

>[!VIDEO](https://video.tv.adobe.com/v/26312/?quality=12)

### Étape 3 : Activation du transfert (par [!UICONTROL Report Suite]) {#step-enabling-the-forwarding-per-report-suite}

Jusqu’à présent, dans ce tutoriel, nous avons passé tout notre temps à changer le code de [!DNL Client-Side DIL] en [!UICONTROL Server-Side Forwarding]. C&#39;est bien, parce que c&#39;est la partie la plus difficile. Bien que cette section soit très facile à voir, elle est tout aussi importante que la mise à jour du code. Dans cette vidéo, vous allez découvrir comment changer le commutateur qui permet le transfert réel des données d’Analytics vers l’Audience Manager.

>[!VIDEO](https://video.tv.adobe.com/v/26355/?quality-12)

**REMARQUE :**  comme indiqué dans la vidéo, n’oubliez pas que l’activation du transfert prendra jusqu’à 4 heures pour être entièrement mise en oeuvre sur le serveur principal Experience Cloud.

## Minutage {#timing}

Pour rappel, il existe deux tâches principales pour passer de [!DNL Client-Side DIL] à [!UICONTROL Server-Side Forwarding] :

1. Mise à jour du code
1. Changement de la balise [!DNL Analytics] [!DNL Admin Console]

Mais la question est, laquelle faites-vous en premier ? Est-ce important ? OK, désolé, c&#39;était deux questions. Mais les réponses sont... ça dépend, et oui, ça *peut* compter. En quoi est-ce vague ? Faisons une ventilation. Mais commencez par une question supplémentaire qui peut s’afficher si vous êtes une grande organisation qui possède de nombreux sites : Dois-je tout faire en même temps ? Celle-là est un peu plus facile. Non. Vous pouvez le faire morceau par morceau... en quelque sorte. :)

### Un peu plus profond {#a-little-deeper-dive}

La raison pour laquelle le timing et la commande sont importants est la façon dont le transfert *fonctionne vraiment*, qui peut être résumé dans les quelques faits techniques suivants :

* Si le service d’ID d’Experience Cloud (ECID) est mis en oeuvre et que le commutateur dans [!DNL Analytics] [!DNL Admin Console] (&quot;le commutateur&quot;) est activé, les données seront transférées de [!DNL Analytics] vers AAM, même si vous n’avez pas encore mis à jour le code.
* Si ECID n’est pas mis en oeuvre, les données ne seront pas transférées, même si le commutateur est activé, et que le code SSF est activé.
* Le code SSF (que ce soit dans [!DNL Launch] ou sur la page) gère réellement la réponse et est bien sûr nécessaire pour terminer la migration.
* N’oubliez pas que le commutateur SSF est activé par [!UICONTROL Report Suite], mais que le code est géré par propriété dans [!DNL Launch] ou par fichier [!DNL AppMeasurement] si vous n’utilisez pas [!DNL Launch]

### Bonnes pratiques {#best-practices}

Sur la base de ces détails techniques, voici les recommandations pour le calendrier de &quot;quoi faire lorsque&quot; :

#### Si vous n’avez PAS encore implémenté ECID {#if-you-do-not-have-ecid-yet-implemented}

1. Retourner le commutateur dans [!DNL Analytics] pour chaque [!UICONTROL report suite] que vous activerez pour SSF

   1. Le transfert ne démarre pas encore car vous ne disposez pas d’ECID

1. Par site, mettez à jour votre code de [!DNL Client-Side DIL] vers SSF (il peut s’agir de [!DNL Launch] ou sur la page, comme indiqué dans une autre section ci-dessus).

   1. Le transfert s’effectue désormais (comme vous avez ajouté l’ECID) et vous devriez également recevoir une réponse JSON appropriée à votre balise [!DNL Analytics] (voir la section Validation et dépannage ci-dessous pour plus d’informations).

#### Si ECID est implémenté {#if-you-do-have-ecid-implemented}

1. Préparez et planifiez afin que vous soyez prêt à mettre à jour votre code du DIL au transfert côté serveur par [!UICONTROL report suite] que vous activerez pour le transfert côté serveur :

   1. Symétrie du commutateur dans [!DNL Analytics] pour activer SSF

      1. Le transfert commencera car ECID est activé
   1. Mettez votre code à jour dès que possible de [!DNL Client-Side DIL] vers SSF (il peut s’agir de [!DNL Launch] ou sur la page, comme expliqué dans une autre section ci-dessus).

      1. Vous devriez recevoir une réponse JSON appropriée à votre balise [!DNL Analytics] (voir la section Validation et dépannage ci-dessous pour plus d’informations).


**REMARQUE 1 :** Il est important de réaliser ces deux étapes aussi près que possible, car entre les étapes 1 et 2 ci-dessus, vous aurez une duplication des données en AAM. En d’autres termes, le transfert côté serveur a commencé à envoyer des données de [!DNL Analytics] vers AAM, et comme le code du DIL se trouve toujours sur la page, un accès se déplace directement de la page vers AAM, ce qui double les données. Dès que vous mettez à jour le code du DIL vers le transfert côté serveur, cela sera facilité.

**REMARQUE 2 :** Si vous préférez une légère incohérence des données plutôt qu’une petite duplication des données, vous pouvez changer l’ordre des étapes 1 et 2 ci-dessus. Le déplacement du code de DIL vers SSF interrompt le flux de données vers AAM jusqu’à ce que vous puissiez inverser le commutateur pour activer le transfert côté serveur de [!UICONTROL report suite]. En règle générale, les clients préfèrent un doublement de données plutôt que de ne pas intégrer les visiteurs dans [!UICONTROL traits] et [!UICONTROL segments].

#### Minutage de migration lorsque vous disposez de plusieurs sites et [!UICONTROL Report Suites] {#migration-timing-when-you-have-many-sites-and-report-suites}

Cette rubrique est brièvement abordée dans les sections précédentes, dans la mesure où la stratégie principale peut être résumée comme suit :

Migrez un site/[!UICONTROL report suite] (ou groupe de sites/[!UICONTROL report suites]) à la fois.

Cependant, cela peut devenir un peu délicat en fonction de quelques scénarios possibles :

* Vous disposez d’un site qui contient plusieurs [!UICONTROL report suites] distincts.
* Vous disposez d’un [!UICONTROL report suite] qui comprend plusieurs sites (comme un [!UICONTROL report suite] global).
* Vous utilisez une propriété [!DNL Launch] pour couvrir plusieurs sites.
* Vous disposez de différentes équipes de développement pour différents sites.

A cause de ces éléments, ça peut devenir un peu compliqué. Les meilleures choses que je puisse suggérer sont les suivantes :

* Prenez le temps d’élaborer une stratégie de migration vers le transfert côté serveur, en fonction des éléments expliqués ci-dessus.
* En fonction du fait qu’une seule propriété de [!DNL Launch] (ou un seul fichier [!DNL AppMeasurement]) correspond généralement à 1 ou 2 [!UICONTROL report suites] distincts, vous serez probablement en mesure de créer un plan qui fonctionne sur ces groupes distincts un par un, mettant à jour votre entreprise en transfert côté serveur.
* Si vous travaillez avec Adobe Consulting, contactez-le au sujet de votre plan de migration, afin qu’il puisse vous aider si nécessaire.

## Validation et dépannage {#validation-and-troubleshooting}

La principale façon de vérifier que [!UICONTROL Server-Side Forwarding] est opérationnel consiste à examiner la réponse à l’un de vos accès Adobe Analytics provenant de l’application.

Si vous n’effectuez pas [!UICONTROL server-side forwarding] de données de [!DNL Analytics] vers l’Audience Manager, aucune réponse n’est apportée à la balise [!DNL Analytics] (hormis un pixel 2x2). Cependant, si vous effectuez un transfert côté serveur, vous pouvez vérifier certains éléments dans la requête [!DNL Analytics] et la réponse qui vous permettront de savoir que [!DNL Analytics] communique correctement avec l’Audience Manager, de transférer l’accès et d’obtenir une réponse.

>[!VIDEO](https://video.tv.adobe.com/v/26359/?quality=12)

**AVERTISSEMENT :** Attention au faux &quot;Succès&quot; - S’il y a une réponse et que tout semble fonctionner, assurez-vous que la réponse contient l’objet &quot;stuff&quot;. Si ce n’est pas le cas, un message peut s’afficher, indiquant [!DNL "status":"SUCCESS"]. Aussi fou que cela paraisse, c&#39;est en fait la preuve qu&#39;il ne fonctionne PAS correctement. Si cela s’affiche, cela signifie que vous avez terminé la mise à jour du code dans [!DNL Launch] ou [!DNL AppMeasurement], mais que le transfert dans la balise [!DNL Analytics] [!DNL Admin Console] n’est pas encore terminé. Dans ce cas, vous devez vérifier que vous avez activé le transfert côté serveur dans la balise [!DNL Analytics] [!DNL Admin Console] de votre balise [!UICONTROL report suite]. Si vous l&#39;avez fait, et que cela n&#39;a pas encore été 4 heures, soyez patient, car cela peut prendre autant de temps pour apporter toutes les modifications nécessaires sur le serveur principal.

![faux succès](assets/falsesuccess.png)

Pour plus d’informations sur [!UICONTROL Server-Side Forwarding], consultez la [documentation](https://marketing.adobe.com/resources/help/en_US/reference/ssf.html).
