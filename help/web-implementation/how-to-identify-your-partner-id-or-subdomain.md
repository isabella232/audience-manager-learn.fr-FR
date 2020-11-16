---
title: Comment identifier votre ID de partenaire d'Audience Manager ou votre sous-domaine
description: Lors de la mise en oeuvre de certaines fonctions d’Experience Cloud, vous devez connaître l’Audience Manager "ID de partenaire" (également parfois appelée "ID de client" ou "sous-domaine"). Dans cette vidéo, nous allons vous montrer deux endroits où vous pouvez obtenir cet identifiant dans l’interface utilisateur de l’Audience Manager.
feature: implementation basics
topics: null
audience: implementer
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2359
translation-type: tm+mt
source-git-commit: a108c51fdad66f4e7974eb96609b6d8f058cb6ff
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---


# Comment identifier votre sous-domaine d&#39;Audience Manager {#how-to-identify-your-audience-manager-partner-id-or-subdomain}

Lors de la mise en oeuvre de certaines fonctionnalités Experience Cloud, vous devez connaître votre Audience Manager `Subdomain` (parfois appelée votre `client ID` ou `Partner ID`). Dans cette vidéo, nous allons vous montrer deux endroits où vous pouvez obtenir ces informations dans l&#39;interface utilisateur de l&#39;Audience Manager.

## Donner la fin... {#giving-away-the-ending}

Au cas où vous préféreriez simplement sauter et le trouver sans regarder cette courte vidéo, vous pouvez trouver votre `Partner Subdomain` place à deux endroits dans l&#39;interface utilisateur :

1. Si vous avez déjà créé une [!UICONTROL rule-based][!UICONTROL trait], cliquez sur **[!UICONTROL Get Trait URL]**
   [!UICONTROL Get Trait URL] est située en regard de la [!UICONTROL trait] liste de [!UICONTROL traits] ce dossier et l’URL inclut votre sous-domaine dans l’URL.
1. Si vous accédez à l’interface **[!UICONTROL Tools]** > **[!UICONTROL Tags]** et cliquez sur **[!UICONTROL Get code]** pour votre conteneur, le sous-domaine se trouve à la fin de la ligne Akamai.

Si vous ne parvenez pas à le trouver rapidement avec ces références rapides, la vidéo est un engagement de courte durée. :)

>[!VIDEO](https://video.tv.adobe.com/v/25922/?quality=12)

>[!IMPORTANT]
>
>Un ID numérique est attribué à chaque client de la Adobe Experience Cloud, et il est souvent appelé &quot;PID&quot;, ou ID de partenaire. Ce n&#39;est pas l&#39;identifiant dont nous parlons dans cet article et cette vidéo. Au lieu de cela, le &quot;sous-domaine partenaire&quot;, parfois appelé ID de partenaire, est généralement une version du nom du client et est le sous-domaine du serveur auquel les données sont envoyées. Par exemple, si votre société est &quot;Bob&#39;s Knobs&quot; (toutes choses que les poignées de porte, bien sûr, haha), il est probable que votre sous-domaine partenaire soit &quot;bobsknobs&quot;, alors que le &quot;PID&quot; serait quelque chose comme &quot;12345&quot;. En règle générale, vous n’avez pas besoin de connaître votre PID, mais votre sous-domaine est important à connaître, de sorte que vous puissiez configurer votre mise en oeuvre d’Audiences Manager.

