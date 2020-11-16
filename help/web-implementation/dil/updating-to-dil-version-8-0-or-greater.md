---
title: Mise à jour vers la version DIL 8.0 de Adobe Audience Manager (ou ultérieure)
description: Cet article décrit les étapes et recommandations de la mise à jour du code du Data Integration Library (DIL) Adobe Audience Manager (AAM) vers la version 8.0 ou ultérieure. Il s’agit de l’implémentation du DIL "côté client", et non du transfert côté serveur des données Adobe Analytics, qui couvrira la gestion dynamique des balises, les Launch by Adobe et les implémentations sans solution Adobe Tag Manager.
feature: dil implementation
topics: null
audience: implementer
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1841
translation-type: tm+mt
source-git-commit: dfd549508cc223714bdb07ac6fd2aa31e6ca5586
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 1%

---


# Mise à jour vers la version DIL 8.0 de Adobe Audience Manager (ou ultérieure) {#updating-to-adobe-audience-manager-s-dil-version-or-greater}

Cet article décrit les étapes et recommandations de la mise à jour du code Adobe Audience Manager (AAM) [!DNL Data Integration Library] (DIL) vers la version 8.0 ou ultérieure. Il s’agit de l’implémentation du DIL &quot;côté client&quot;, et non du transfert côté serveur des données Adobe Analytics, qui couvrira la gestion dynamique des balises, les Launch by Adobe et les implémentations sans solution Adobe Tag Manager.

## Présentation {#overview}

Le code de l’Audience Manager [!DNL Data Integration Library] (DIL) vous permet de mettre en oeuvre AAM sur votre site Web*. Lors de la mise en oeuvre des versions précédentes d’un DIL, il n’était pas nécessaire que le service d’identification des Experience Cloud (ECID) de l’Adobe soit également mis en oeuvre (même si c’était une très bonne idée). A partir de la version 8.0 du DIL, il existe une dépendance stricte sur ECID version 3.3 ou ultérieure. Si vous implémentez DIL 8.0 ou une version ultérieure sans ECID 3.3, ou avec une version antérieure, vous obtenez une erreur et elle ne fonctionnera pas. Comme il existe plusieurs façons de mettre en oeuvre l&#39;AAM, nous avons créé cette page pour vous donner quelques étapes à suivre, ainsi que quelques recommandations. Vous trouverez ci-dessous les étapes et recommandations ventilées par plateforme/méthode d’implémentation. Pour plus d’informations sur le DIL, consultez la [documentation](https://marketing.adobe.com/resources/help/en_US/aam/c_dil.html).

* Comme indiqué dans la description de cette page, cela ne couvrira que les implémentations de DIL &quot;côté client&quot;, utilisées par AAM clients qui n’ont pas d’Adobe Analytics. Si vous possédez Adobe Analytics, vous devez utiliser la méthode de transfert côté serveur pour implémenter AAM. Cette méthode est décrite dans la [documentation](https://marketing.adobe.com/resources/help/en_US/reference/ssf.html).

## Duplicata et éléments et méthodes obsolètes {#duplicate-and-deprecated-elements-and-methods}

Dans les versions antérieures du DIL et de l&#39;ECID, il y avait des méthodes en double (méthodes qui fonctionnent de la même façon dans le DIL et l&#39;ECID), ce qui entraînait une confusion quant à l&#39;utilisation à utiliser. En général, vous deviez les utiliser et les faire correspondre, et ce message n&#39;était pas bien communiqué à nos clients. A compter de la version 8.0 de DIL, ces méthodes et éléments de duplicata ont été abandonnés dans DIL et il est recommandé d’utiliser la version ECID.

Par exemple :

* Lors de l’utilisation [!DNL DIL.create]de certains éléments, ceux-ci ont été abandonnés et vous devez utiliser les éléments ECID à la place. Ces éléments sont décrits dans la [[!DNL DIL.create] documentation](https://marketing.adobe.com/resources/help/en_US/aam/r_dil_create.html).
* La méthode au niveau de l’ [!DNL idSync] instance a également été abandonnée, comme indiqué dans la [documentation](https://marketing.adobe.com/resources/help/en_US/aam/r_dil_idsync.html)de la méthode.

## Synchronisation des identifiants avec un ID de client {#id-syncing-with-a-customer-id}

Dans AAM, vous pouvez synchroniser votre UUID (identifiant utilisateur unique anonyme) sur l’ordinateur avec un ID de client, de sorte que vous puissiez télécharger des données hors ligne sur ce client et les lier à leur comportement en ligne, afin de mieux comprendre vos clients. Dans le passé, cela s&#39;est fait de deux manières :

* Méthode de niveau [!DNL idSync] instance
* L’ [!DNL declaredId] élément dans [!DNL DIL.create]

Si vous avez utilisé l’une ou l’autre de ces anciennes méthodes pour la synchronisation avec un ID de client, il est vivement recommandé de procéder à la mise à jour vers l’utilisation de la [!DNL setCustomerIDs] méthode, qui fait partie du service ECID. Pour plus d’informations sur [!DNL setCustomerIDs] cette méthode, consultez la [documentation](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid_setcustomerids.html)de la méthode.

**Conseil rapide :** Lors de l&#39;utilisation précédente de l&#39;une des méthodes ci-dessus, vous avez référencé l&#39;AAM [!UICONTROL Data Source] avec l&#39; [!UICONTROL Data Source] ID (AKA le &quot;DPID&quot;). Lors de la mise à jour vers [!DNL setCustomerIDs], vous devez utiliser plutôt le &quot; [!UICONTROL Data Source]&quot; de l’AAM[!UICONTROL Integration Code]. Il pointe toujours vers le même [!UICONTROL Data Source] mais n&#39;est qu&#39;un identifiant différent. Ceci est montré dans la vidéo ci-dessous.

>[!VIDEO](https://video.tv.adobe.com/v/23873/?quality=12)

Les sections suivantes liste les étapes et les recommandations de mise à jour vers DIL 8.0 en fonction de votre méthode d’implémentation :

## Mise à jour vers DIL 8.0 dans Adobe Experience Platform Launch {#updating-to-dil-in-experience-platform-launch}

Étapes de base de la mise à jour vers DIL 8.0

1. Si vous utilisez un DIL antérieur à la version 8.0, avant de procéder à la mise à niveau, accédez à la configuration du DIL dans l’extension AAM et notez les options avancées que vous utilisez (à utiliser dans une étape ultérieure).
1. Mettez à jour votre extension AAM vers la version 8.0 ou ultérieure
1. Vérifiez que l’extension du service d’identification des Experience Cloud est de la version 3.3.0 ou supérieure.
1. Pour les méthodes/éléments obsolètes (tels que &quot;[!DNL disableIDSyncs]&quot;) qui se trouvaient dans votre extension AAM antérieure à la version 8.0 ou dans le code personnalisé du DIL, activez les méthodes ECID dans l’extension ECID.

   1. (DIL) disableDestinationPublishingIframe -> (ECID) disableIdSyncs
   1. (DIL) disableIDSyncs -> (ECID) disableIdSyncs
   1. (DIL) iframeAkamaiHTTPS -> (ECID) dSyncSSLUseAkamai
   1. (DIL) statementId -> (ECID) setCustomerIDs

1. Publication des modifications

>[!VIDEO](https://video.tv.adobe.com/v/23874/?quality=12)

## Mise à jour vers DIL 8.0 dans Adobe DTM {#updating-to-dil-in-adobe-dtm}

1. Mettez à jour votre outil AAM vers la version 8.0 ou ultérieure. Ce paramètre de version se trouve sous la section &quot;Général&quot; de l’outil AAM.
1. Pour les méthodes/éléments obsolètes (tels que &quot;disableIDSyncs&quot;) qui se trouvaient dans le code personnalisé de votre DIL de l’outil AAM version antérieure à 8.0, notez-les (afin que vous puissiez les ajouter à l’outil ECID), puis supprimez-les de la personnalisation [!DNL DIL code] de l’outil AAM.
1. Mettez à jour votre extension du service d’identification des Experience Cloud vers la version 3.3.0 ou ultérieure.
1. Ajoutez les options avancées à l&#39;outil ECID que vous avez supprimé du code personnalisé de l&#39;outil AAM.
1. Publication des modifications

## Mise à jour vers DIL 8.0 sans solution de gestion des balises d’Adobe {#additional-resources}

Si vous mettez à jour votre code directement sur la page, vous pouvez simplement remplacer les éléments plus anciens par des éléments plus récents, sauf quand vous devez déplacer les méthodes/éléments du DIL à l&#39;ECID, comme expliqué ci-dessus. Dans ce cas, vous remplacerez simplement l’ancienne méthode/élément de l’emplacement du DIL par la méthode/l’élément ECID de l’emplacement ECID.

Il en va de même pour les gestionnaires de balises non-Adobes. Où que vous disposiez des anciennes versions de cette solution de gestion des balises, remplacez-la par le nouveau code, comme décrit dans les étapes suivantes.

1. Mettez à jour votre bibliothèque de DIL vers la dernière version (8.0 ou ultérieure). Vous devrez obtenir le code de DIL le plus récent auprès du service d’assistance clientèle d’Adobes ou d’Adobes, car il n’est actuellement pas disponible dans un emplacement public. Ensuite, remplacez simplement l’ancien code de bibliothèque du DIL par le nouveau code de bibliothèque du DIL et passez à l’étape suivante (ne vous arrêtez pas maintenant ou vous rencontrerez des problèmes, ha).
1. Installez [!DNL ECID Service] ou mettez à jour votre version existante vers la version 3.3.0 ou ultérieure. Vous pouvez télécharger la dernière version du service d’identification des Experience Cloud [à partir de notre page](https://github.com/Adobe-Marketing-Cloud/id-service/releases)GitHub. Si vous avez besoin d&#39;aide pour cela, consultez la [documentation](https://marketing.adobe.com/resources/help/fr_FR/mcvid/) ou contactez un consultant en Adobe.

1. Vérifiez que les méthodes ou éléments déconseillés figurant dans votre code personnalisé pour le DIL sont déplacés vers les méthodes ECID :

   1. (DIL) disableDestinationPublishingIframe -> (ECID) disableIdSyncs

      [Documentation](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-disableidsync.html)

   1. (DIL) disableIDSyncs -> (ECID) disableIdSyncs

      [Documentation](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-disableidsync.html)

   1. (DIL) iframeAkamaiHTTPS -> (ECID) idSyncSSLUseAkamai

      [Documentation](https://marketing.adobe.com/resources/help/en_US/aam/r_dil_create.html)

   1. (DIL) statementId -> (ECID) setCustomerIDs

      [Documentation](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid_setcustomerids.html)