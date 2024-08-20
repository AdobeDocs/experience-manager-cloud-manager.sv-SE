---
title: Miljöprovisionering
description: Läs om hur era miljöer etableras som en del av Cloud Manager introduktionsprocess.
exl-id: eade4255-89b5-4c65-a498-1c6d4e8c73ff
source-git-commit: 4c977cdfbef438fdabd90ee104d98887f2467b49
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# Miljöetablering {#environments-provisioning}

Läs om hur era miljöer etableras som en del av Cloud Manager introduktionsprocess.

## Provisionering {#provisioning}

Under introduktionsprocessen etablerar Adobe automatiskt alla AEM molnmiljöer som du har köpt och länkar dem till ditt program i [!UICONTROL Cloud Manager]. Varje Adobe Managed Services-prenumeration innehåller AEM molnmiljöer. De omfattar vanligtvis minst en produktionsmiljö och en staging-miljö. De kan även innehålla en eller flera utvecklings- eller testmiljöer.

## Välkomstmeddelande {#welcome-email}

När miljöprovisioneringsprocessen har slutförts får den utsedda kundadministratören ett välkomstmeddelande med en bekräftelse på att de har beviljats åtkomst till Adobe [!UICONTROL Experience Cloud]. Välkomstmeddelandet innehåller detaljerad information om hur du kommer igång med [!UICONTROL Experience Cloud]-tjänster, [!UICONTROL AEM Managed Services] molnmiljöer och [!UICONTROL Cloud Manager] självbetjäningsportal. Dessutom innehåller e-postmeddelandet viktig information, t.ex. kontaktinformation till kundens Success Engineer (CSE), var finns supportresurser, forum, frågor och svar och mycket annat. I listan över resurser i e-postmeddelandet finns även information om hur du får åtkomst till [!UICONTROL Cloud Manager] för dina AEM molnmiljöer.

## Nästa steg {#next-steps}

När du har fått välkomstmeddelandet kan du logga in på [!UICONTROL Cloud Manager] som systemadministratör med dina Adobe IMS-autentiseringsuppgifter. När du har loggat in kan du kontrollera att din AEM molnproduktion och icke-produktionsmiljöer är tillgängliga och fungerar smidigt.

[!UICONTROL Cloud Manager] använder dessa AEM molnmiljöer för att köra CI/CD-pipeline. Den distribuerar kod från sin Git-databas till staging-miljön. Sedan distribueras koden till AEM produktionsmiljö. Du kan även komma åt dina AEM molnmiljöer direkt från [!UICONTROL Cloud Manager] när du är redo att börja skapa digitala upplevelser för dina webbegenskaper.
