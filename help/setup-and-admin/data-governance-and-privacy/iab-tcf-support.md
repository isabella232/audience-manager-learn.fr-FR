---
title: Prise en charge d’IAB TCF 2.0 en Audience Manager
description: Adobe vous offre les moyens de gérer et de communiquer les choix de confidentialité de vos utilisateurs grâce à la fonctionnalité d’inclusion et au module d’Audience Manager de la prise en charge du Cadre de transparence et de consentement IAB 2.0 (TCF 2.0). Cet article travaille en collaboration avec la documentation pour vous aider à comprendre le module d’Audience Manager à IAB TCF et comment il fonctionne avec l’objet d’inclusion d’Adobe et votre fournisseur de gestion du consentement (CMP).
feature: data governance & privacy
topics: null
audience: implementer, architect
activity: implement
doc-type: technical video
team: Technical Marketing
thumbnail: 26434.jpg
kt: 5027
translation-type: tm+mt
source-git-commit: df8afb50ed3971dc47e6506d31a8222a7f488b25
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 0%

---


# Prise en charge d’IAB TCF 2.0 en Audience Manager {#iab-tcf-support-in-audience-manager}

Adobe vous offre les moyens de gérer et de communiquer les choix de confidentialité de vos utilisateurs grâce à la fonctionnalité d’inclusion et au module d’Audience Manager de la prise en charge du Cadre de transparence et de consentement IAB 2.0 (TCF 2.0). Cet article travaille en collaboration avec la documentation pour vous aider à comprendre le module d’Audience Manager à IAB TCF et comment il fonctionne avec l’objet d’inclusion d’Adobe et votre fournisseur de gestion du consentement (CMP). Pour en savoir plus sur l&#39;IAB, consultez son site Web à l&#39;adresse [https://www.iabeurope.eu/](https://www.iabeurope.eu/).

## Première étape : Comprendre l’inclusion d’ECID {#first-step-understand-ecid-s-opt-in}

Pour comprendre comment travailler avec le TCF IAB, vous devez d’abord comprendre la fonctionnalité [!DNL Opt-in], qui fait partie de la bibliothèque ECID (Experience Cloud ID Service). Si vous ne connaissez pas le fonctionnement de l’inclusion, consultez [cet article très utile](https://docs.adobe.com/content/help/en/core-services-learn/tutorials/id-service/use-opt-in-to-control-experience-cloud-activities-based-on-user-consent.html) en premier. Vous devez également consulter la [documentation relative à l’inclusion](https://docs.adobe.com/content/help/fr-FR/id-service/using/implementation/opt-in-service/optin-overview.html). Une fois que vous avez accédé à ces ressources, revenez à cette page et continuez.

## Module d&#39;Audience Manager pour le TCF IAB {#the-audience-manager-plug-in-for-iab-tcf}

Maintenant que vous connaissez au moins le fonctionnement du service d’inclusion, l’Audience Manager peut y ajouter une couche de prise en charge [!DNL IAB Transparency and Consent Framework (TCF)], qui est effectuée via un module externe dans l’objet d’inclusion.

Le module externe d’Audience Manager pour IAB TCF étend les fonctionnalités de l’inclusion et permet aux clients AAM d’évaluer, d’honorer et de transférer les choix de confidentialité des utilisateurs aux partenaires en aval, conformément à IAB TCF. Il fournit une norme que les contrôleurs de données (c’est-à-dire vous en tant que client d’Adobe) et les fournisseurs (DMP, DSP, SSP, Ad Servers, etc.) peut être utilisé pour comprendre le consentement dans le paysage du consentement.

## Activation de l&#39;IAB TCF {#enabling-iab-tcf}

L’activation du module externe d’Audience Manager pour IAB TCF est facile si vous utilisez Adobe Experience Platform Launch, car il s’agit d’une simple case à cocher, comme le montre la courte vidéo ci-dessous :

>[!VIDEO](https://video.tv.adobe.com/v/26433/?quality=12)

Si vous n’utilisez pas le lancement, vous pouvez également utiliser `isIabContext=true` pour l’activer lorsque vous instanciez le Visiteur Experience Cloud. Cela initie le flux de TCF IAB, c&#39;est-à-dire ajoute une autre étape à la collecte de consentement, en utilisant le TCF IAB pour la requête de la chaîne de TC IAB et le remet à l&#39;inclusion, qui à son tour communique avec les solutions Experience Cloud.

## Chaîne de TC IAB {#iab-tcf-consent-string}

L&#39;une des normes que l&#39;IAB fournit est une &quot;chaîne de consentement&quot; (également connue sous le nom de &quot;DaisyBit&quot;), qui est en fait deux listes réunies :

1. Objectifs : **Que** le consentement est-il donné pour faire ?
1. Fournisseurs : **À qui** le consentement est-il donné ?

### Objectifs {#purposes}

Avec IAB TCF 2.0, il existe dix &quot;fins&quot; pour recueillir le consentement (ce que les fournisseurs peuvent faire avec les données du visiteur). Adobe Audience Manager n&#39;exige pas les dix, mais seulement le consentement aux fins suivantes, en plus du consentement du vendeur :

* **But 1 :** Stocker et/ou accéder aux renseignements sur un appareil ;
* **But 10 :** Élaborer et améliorer des produits ;
* **Objectif spécial 1 :** assurer la sécurité, prévenir les fraudes et déboguer.

Il s’agit de la première partie de la chaîne TC de l’IAB et elle est simplement enregistrée sous la forme 1 et 0, ce qui détermine si cet objectif/cette activité est approuvé ou non.

>[!NOTE]
>
>Conformément aux règlements du CCI, l&#39;objectif spécial 1 (assurer la sécurité, prévenir la fraude et déboguer) est toujours accepté et les utilisateurs ne peuvent s&#39;y opposer.

### Fournisseurs {#vendors}

Une autre partie de la chaîne CCI de l&#39;IAB est une longue liste de plusieurs centaines de fournisseurs, de sorte que les visiteurs puissent se voir présenter une liste de fournisseurs applicables qui ont des balises sur le site et peuvent choisir les fournisseurs à utiliser. Les vendeurs conservent leur place sur la liste. Par exemple, le numéro de fournisseur de Adobe Audience Manager sur cette liste est 565. Si ce numéro de la liste comporte un &quot;1&quot;, l’Audience Manager peut alors réaliser les objectifs approuvés à l’avant de la liste. Si le spot AAM a un &quot;0&quot;, il ne peut rien faire avec les données.

**Pour que l’Audience Manager puisse fournir une interface utilisateur aux clients afin qu’ils puissent utiliser le TCF de l’IAB pour choisir ces objectifs et fournisseurs, ou pour approuver/désapprouver toute activité, vous devez utiliser un partenaire CMP enregistré avec le TCF de l’IAB ou en créer un qui prend en charge le TCF de l’IAB et qui est enregistré avec le TCF de l’IAB.**

## Inscription : Traduction entre l’IAB et les solutions d’Adobe {#opt-in-translating-between-iab-and-adobe-solutions}

L&#39;un des avantages de l&#39;utilisation du TCF de l&#39;IAB est que les objectifs standard énumérés ci-dessus donnent probablement à l&#39;utilisateur final plus d&#39;idée de ce qu&#39;il approuve qu&#39;une liste de solutions d&#39;Adobe. Les utilisateurs finaux ne savent peut-être pas ce que signifie &quot;approuver&quot; l&#39;Audience Manager ou [!DNL Target], mais &quot;stocker et/ou accéder aux informations sur un appareil&quot; ou &quot;développer et améliorer des produits&quot; est probablement plus facile à comprendre et à accepter.

Pour que l&#39;Audience Manager soit approuvée (c.-à-d. pour que la traduction des fins de l&#39;IAB pour l&#39;inscription donne AAM &quot;oui&quot;), les buts 1 et 10, énumérés ci-dessus, doivent recevoir le consentement de l&#39;utilisateur final. Si l&#39;un ou l&#39;autre n&#39;est pas approuvé, ou si un fournisseur n&#39;est pas approuvé, AAM n&#39;exécutera pas les incendies de pixels ou ne définira pas de cookies. Il est également bon de savoir que de nombreux clients choisissent simplement de fournir à l&#39;utilisateur final une interface utilisateur &quot;tout ou rien&quot;, qui permettrait, bien sûr, ou refuserait l&#39;utilisation de l&#39;Audience Manager (et les autres solutions Experience Cloud).

La [documentation](https://marketing.adobe.com/resources/help/en_US/aam/aam-iab-plugin.html) contient de superbes informations sur la façon dont le flux du module externe d’Audience Manager pour IAB TCF s’applique aux cas d’utilisation de l’éditeur et de l’annonceur.

## IAB : Envoi du consentement en aval {#iab-sending-consent-downstream}

Lorsque le module externe d’Audience Manager pour IAB TCF est utilisé, les choix de consentement de l’utilisateur sont également envoyés à la synchronisation des identifiants au niveau de la plateforme (tierce) pour les partenaires présents sur la Liste du fournisseur global, de sorte que le partenaire dispose des informations de consentement de l’utilisateur et puisse agir en conséquence. Ces informations sont envoyées dans deux variables :

* gdpr = 1
* gdpr_consentement = [chaîne de consentement codée]

La mise en garde est que si l’utilisateur se trouve dans le contexte IAB et ne donne pas son consentement (ou ne donne pas son consentement négatif), l’Audience Manager ne collecte pas du tout la chaîne de CT IAB et, de ce fait, supprime les appels. Donc, dans ce cas... aucun transfert de consentement en aval.

## Démonstration{#demo}

Dans la vidéo ci-dessous, voir comment les cookies et les balises de l’ECID et des solutions sont affectés par les sélections de choix des utilisateurs de l’IAB.

>[!VIDEO](https://video.tv.adobe.com/v/26434/?quality=12)

Pour plus d’informations sur le module externe d’Audience Manager pour IAB TCF 2.0, y compris sur la mise en oeuvre et le test, les cas d’utilisation et le flux de travail, voir la [documentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).
