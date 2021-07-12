---
title: Comment identifier votre identifiant de partenaire ou votre sous-domaine d’Audience Manager
description: Lors de la mise en oeuvre de certaines fonctionnalités Experience Cloud, vous devez connaître votre Audience Manager "Identifiant de partenaire" (également parfois appelé "identifiant client" ou "sous-domaine"). Dans cette vidéo, nous vous montrerons deux emplacements où vous pourrez obtenir cet identifiant dans l’interface utilisateur d’Audience Manager.
feature: Principes de mise en oeuvre
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2359
role: Developer, Data Engineer
level: Intermediate
exl-id: d3f4a12d-acc5-47b7-a38a-a6a14152bf3a
source-git-commit: 4b91696f840518312ec041abdbe5217178aee405
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# Comment identifier votre sous-domaine d’Audience Manager {#how-to-identify-your-audience-manager-partner-id-or-subdomain}

Lors de l’implémentation de certaines fonctionnalités Experience Cloud, vous devez connaître votre Audience Manager `Subdomain` (également appelée `client ID` ou `Partner ID`). Dans cette vidéo, nous vous montrerons deux endroits où vous pourrez obtenir ces informations dans l’interface utilisateur d’Audience Manager.

## En donnant la fin... {#giving-away-the-ending}

Si vous préférez sauter et le trouver sans regarder cette courte vidéo, vous pouvez trouver votre `Partner Subdomain` à deux endroits dans l’interface utilisateur :

1. Si vous avez déjà créé une [!UICONTROL rule-based] [!UICONTROL trait], cliquez sur **[!UICONTROL Get Trait URL]**
   [!UICONTROL Get Trait URL] est en regard de  [!UICONTROL trait] dans la liste de  [!UICONTROL traits] dans ce dossier et l’URL inclut votre sous-domaine dans l’URL.
1. Si vous accédez à l’interface **[!UICONTROL Tools]** > **[!UICONTROL Tags]** et cliquez sur **[!UICONTROL Get code]** pour votre conteneur, le sous-domaine se situe vers la fin de la ligne Akamai.

Si vous ne parvenez pas à le trouver rapidement avec ces références rapides, la vidéo est un engagement de courte durée. :)

>[!VIDEO](https://video.tv.adobe.com/v/25922/?quality=12)

>[!IMPORTANT]
>
>Un identifiant numérique est attribué à chaque client de Adobe Experience Cloud, ce qui est souvent appelé &quot;PID&quot; ou identifiant de partenaire. Ce n&#39;est pas l&#39;identifiant dont nous parlons dans cet article et cette vidéo. Au lieu de cela, le &quot;sous-domaine partenaire&quot;, parfois appelé ID de partenaire, est généralement une version du nom du client et est le sous-domaine du serveur auquel les données sont envoyées. Par exemple, si votre société est &quot;Bob&#39;s Knobs&quot; (tout ce qui concerne les poignées de porte, bien sûr, haha), il est probable que votre sous-domaine partenaire soit &quot;bobsKnobs&quot;, alors que le &quot;PID&quot; serait quelque chose comme &quot;12345&quot;. En règle générale, vous n’avez pas besoin de connaître votre PID, mais votre sous-domaine est important à connaître afin de pouvoir configurer l’implémentation de votre Audience Manager.

