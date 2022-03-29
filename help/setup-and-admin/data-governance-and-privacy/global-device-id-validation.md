---
title: Validation de l’identifiant de périphérique global
description: Découvrez la validation des identifiants d’appareil envoyés aux sources de données globales pour une mise en forme correcte et les messages d’erreur lorsque les identifiants sont mal formatés.
feature: Data Governance & Privacy
topics: mobile
activity: implement
doc-type: article
team: Technical Marketing
kt: 2977
role: Developer, Data Engineer, Architect
level: Experienced
exl-id: 0ff3f123-efb3-4124-bdf9-deac523ef8c9
source-git-commit: 2094d3bcf658913171afa848e4228653c71c41de
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 1%

---

# Validation de l’identifiant de périphérique global {#global-device-id-validation}

Les identifiants de publicité de périphérique (c’est-à-dire iDFA, GAID, Roku ID) ont des normes de mise en forme qui doivent être respectées pour être utilisables dans l’écosystème de publicité numérique. Aujourd’hui, les clients et les partenaires peuvent charger des identifiants dans nos sources de données globales dans n’importe quel format sans être avertis si l’identifiant est correctement formaté. Cette fonctionnalité introduit la validation des identifiants d’appareil envoyés aux sources de données globales pour une mise en forme correcte et fournit des messages d’erreur lorsque les identifiants sont mal formatés. Nous prendrons en charge la validation pour [!DNL iDFA], [!DNL Google Advertising] et [!DNL Roku IDs] au lancement.

## Présentation des normes de format {#overview-of-format-standards}

Vous trouverez ci-dessous les pools d’identifiants de publicité de périphérique globaux actuellement reconnus et pris en charge par AAM. Ils sont implémentés comme partagés [!UICONTROL Data Sources] qui peuvent être utilisés par n’importe quel client ou partenaire de données qui travaille avec des données liées aux utilisateurs de ces plateformes.

<table>
  <tr>
   <td>Plateforme </td>
   <td>ID de source de données AAM </td>
   <td>Format d’ID </td>
   <td>AAM PID </td>
   <td>Remarques </td>
  </tr>
  <tr>
   <td>Google Android (GAID)</td>
   <td>20914</td>
   <td>32 nombres hexadécimaux, généralement présentés sous la forme 8-4-4-4-12<em>exemple : 97987bca-ae59-4c7d-94ba-ee4f19ab8c21<br/> </em> </td>
   <td>1352</td>
   <td>Cet identifiant doit être collecté dans une référence de formulaire brute/non hachée/non modifiée - <a href="https://play.google.com/about/monetization-ads/ads/ad-id/">https://play.google.com/about/monetization-ads/ads/ad-id/</a></td>
  </tr>
  <tr>
   <td>Apple iOS (IDFA)</td>
   <td>20915</td>
   <td>32 nombres hexadécimaux, généralement présentés sous la forme 8-4-4-4-12 <em>Exemple : 6D92078A-8246-4BA4-AE5B-76104861E7DC<br /> </em> </td>
   <td>3560</td>
   <td>Cet identifiant doit être collecté dans une référence de formulaire brute/non hachée/non modifiée - <a href="https://support.apple.com/en-us/HT205223">https://support.apple.com/en-us/HT205223</a></td>
  </tr>
  <tr>
   <td>Roku (RIDA)</td>
   <td>121963</td>
   <td>32 nombres hexadécimaux, généralement présentés sous la forme 8-4-4-4-12 <em>exemple,</em> <em>fcb2a29c-315a-5e6b-bcfd-d889ba19aada</em></td>
   <td>11536</td>
   <td>Cet identifiant doit être collecté dans une référence de formulaire brute/non hachée/non modifiée - <a href="https://sdkdocs.roku.com/display/sdkdoc/Roku+Advertising+Framework">https://sdkdocs.roku.com/display/sdkdoc/Roku+Advertising+Framework</a> </td>
  </tr>
  <tr>
   <td>Microsoft Advertising ID (MAID)</td>
   <td>389146</td>
   <td>Chaîne numérique Alpha</td>
   <td>14593</td>
   <td>Cet identifiant doit être collecté dans une référence de formulaire brute/non hachée/non modifiée - <a href="https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid">https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid</a><br/><a href="https://msdn.microsoft.com/en-us/library/windows/apps/windows.system.userprofile.advertisingmanager.advertisingid.aspx">https://msdn.microsoft.com/en-us/library/windows/apps/windows.system.userprofile.advertisingmanager.advertisingid.aspx</a></td>
  </tr>
  <tr>
   <td>Samsung DUID</td>
   <td>404660</td>
   <td>Exemple de chaîne numérique Alpha, 7XCBNROQJPYW</td>
   <td>15950</td>
   <td>Cet identifiant doit être collecté dans une référence de formulaire brute/non hachée/non modifiée - <a href="https://developer.samsung.com/tv/develop/api-references/samsung-product-api-references/productinfo-api">https://developer.samsung.com/tv/develop/api-references/samsung-product-api-references/productinfo-api</a> </td>
  </tr>
</table>

## Définition d’un identifiant de publicité dans l’application {#setting-an-advertising-identifier-in-the-app}

La définition de l’ID d’annonceur dans l’application est un processus en deux étapes, d’abord la récupération de l’ID d’annonceur, puis son envoi à l’Experience Cloud. Vous trouverez ci-dessous des liens pour effectuer ces étapes.

1. Récupération de l’ID
   1. [!DNL Apple] informations relatives à [!DNL advertising ID] est disponible [ICI](https://developer.apple.com/documentation/adsupport/asidentifiermanager).
   1. Quelques informations sur la définition de la variable [!DNL advertiser ID] pour [!DNL Android] les développeurs sont disponibles [ICI](http://android.cn-mirrors.com/google/play-services/id.html).
1. Envoyez-le à l’Experience Cloud à l’aide du [!DNL setAdvertisingIdentifier] dans le SDK
   1. Informations relatives à l’utilisation de `setAdvertisingIdentifier` se trouve dans la variable [documentation](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#set-an-advertising-identifier) pour les deux [!DNL iOS] et [!DNL Android].

`// iOS (Swift) example for using setAdvertisingIdentifier:`
`ACPCore.setAdvertisingIdentifier([AdvertisingId]) // ...where [AdvertisingId] is replaced by the actual advertising ID`

## Messagerie d’erreur DCS pour les ID incorrects  {#dcs-error-messaging-for-incorrect-ids}

Lorsqu’un identifiant de périphérique global incorrect (IDFA, GAID, etc.) est envoyé en temps réel à l’Audience Manager, un code d’erreur est renvoyé lors de l’accès. Voici un exemple d’erreur renvoyée, car l’ID est envoyé en tant que [!DNL Apple IDFA], qui ne doit contenir que des majuscules, et pourtant il existe un &quot;x&quot; minuscule dans l’identifiant.

![image d&#39;erreur](assets/image_4_.png)

Veuillez consulter la [documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-error-codes.html?lang=en#api-and-sdk-code) pour la liste des codes d’erreur.

## Intégration des identifiants de périphérique globaux {#onboarding-global-device-ids}

Outre l’envoi en temps réel des identifiants d’appareils globaux, vous pouvez également &quot;[!DNL onboard]&quot; (transférez) également des données par rapport aux identifiants. Ce processus est le même que lorsque vous intégrez des données par rapport à vos ID de client (généralement via des paires clé/valeur), mais vous utiliserez simplement les ID de source de données appropriés, de sorte que les données soient affectées à l’ID d’appareil global. Vous trouverez de la documentation sur le processus d’intégration dans la section [documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/sending-audience-data/batch-data-transfer-process/batch-data-transfer-overview.html?lang=en#implementation-integration-guides). N’oubliez pas d’utiliser l’ID de source de données globale, en fonction de la plateforme que vous utilisez.

Si des identifiants d’appareil global incorrects sont envoyés par le biais du processus d’intégration, les erreurs s’affichent dans la variable [[!DNL Onboarding Status Report]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reporting/onboarding-status-report.html?lang=en#reporting).

Voici un exemple d’erreur qui résulterait de ce rapport :

![image d&#39;erreur](assets/image_5_.png)
