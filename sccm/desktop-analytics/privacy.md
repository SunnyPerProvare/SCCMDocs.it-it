---
title: Privacy dei dati di analisi desktop
titleSuffix: Configuration Manager
description: L'analisi del desktop è vincolata alla privacy dei dati dei clienti
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: aef08fb2d4c404ea66ded3d1a49d30af68fe4a95
ms.sourcegitcommit: 9648ce8a8b5c82518e7c8b6a7668e0e9b076cae6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/05/2019
ms.locfileid: "70379747"
---
# <a name="desktop-analytics-data-privacy"></a>Privacy dei dati di analisi desktop

Desktop Analytics è pienamente impegnato nella privacy dei dati dei clienti, centrando su questi principi:

- **Trasparenza** Gli eventi di diagnostica di Windows sono documentati in modo completo. Esaminarli con i team di sicurezza e conformità dell'azienda. Il Visualizzatore dati di diagnostica Windows consente di visualizzare i dati di diagnostica inviati da un determinato dispositivo. Per altre informazioni, vedere [Cenni preliminari sul Visualizzatore dati di diagnostica](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview).  

- **Controllo** È possibile controllare il livello dei dati di diagnostica da condividere con Microsoft. Windows 10, versione 1709, aggiunge un nuovo criterio per limitare i dati di diagnostica avanzati al minimo richiesto da desktop Analytics.  

- **Sicurezza** Microsoft protegge i dati con sicurezza e crittografia complesse.  

- **Trust** Desktop Analytics supporta l' [informativa sulla privacy](https://privacy.microsoft.com/privacystatement) di Microsoft e le condizioni per i [servizi online](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).  



## <a name="diagnostic-data-flow"></a>Flusso di dati di diagnostica

La figura seguente mostra il flusso dei dati di diagnostica da singoli dispositivi tramite il servizio dati di diagnostica, l'archiviazione di Azure Log Analytics e l'area di lavoro Log Analytics:

![Diagramma che illustra il flusso dei dati di diagnostica dai dispositivi](media/da-data-flow.png)

1. Si accede al portale di Azure e si esegue l'onboarding in desktop Analytics. Si crea l'app Azure AD per connettersi con Configuration Manager. Quando si configura analisi desktop, si crea un'area di lavoro di Azure Log Analytics nel percorso desiderato.  

2. Connettersi Configuration Manager e registrare i dispositivi  

    1. Il servizio cloud di analisi dei desktop viene configurato in Configuration Manager con i dettagli dell'app Azure AD.  

    2. Entro 15 minuti Configuration Manager Sincronizza i piani di raccolte e distribuzioni dei dispositivi con analisi del desktop. Questa operazione viene ripetuta ogni ora.  

    3. Configuration Manager imposta l'ID commerciale, il livello dati di diagnostica e altre impostazioni per i dispositivi nella raccolta di destinazione. Questa configurazione specifica i dispositivi da visualizzare nell'area di lavoro di analisi del desktop.  

    4. Gli aggiornamenti della compatibilità vengono distribuiti in tutti i dispositivi di destinazione.  

3. I dispositivi inviano i dati di diagnostica al servizio Microsoft Diagnostic Gestione dati per Windows. Questo servizio è ospitato nel Stati Uniti.  

4. Ogni giorno, Microsoft produce uno snapshot delle informazioni approfondite incentrate sull'IT. Questo snapshot combina i dati di diagnostica di Windows con l'input per i dispositivi registrati. Questo processo si verifica nell'archiviazione temporanea, che viene usato solo da desktop Analytics. L'archiviazione temporanea è ospitata nei Data Center Microsoft nel Stati Uniti. Gli snapshot vengono isolati in base all'ID commerciale.  

5. Gli snapshot vengono quindi copiati nell'area di lavoro di Azure Log Analytics appropriata.  

6. Desktop Analytics archivia l'input in Azure Log Analytics archiviazione. Queste configurazioni includono i piani di distribuzione e le decisioni relative agli asset per l'aggiornamento e l'importanza.  



## <a name="other-resources"></a>Altre risorse

Per le domande frequenti relative alla privacy per analisi desktop, vedere [domande frequenti sulla privacy](/sccm/desktop-analytics/faq#privacy).

Per ulteriori informazioni sugli aspetti correlati alla privacy, vedere gli articoli seguenti:

- [Windows 10 e GDPR per i responsabili decisionali IT](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configurare i dati di diagnostica di Windows nell'organizzazione](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Eventi e campi di dati di diagnostica di Windows 7, Windows 8 e Windows 8.1 Estimator](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)  

- [Eventi e campi di diagnostica Windows 10, versione 1809 livello Basic](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [Eventi e campi di dati di diagnostica avanzati di Windows 10, versione 1709 usati da desktop Analytics](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [Panoramica del Visualizzatore dati di diagnostica](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [Condizioni di licenza e documentazione](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  

- [Sicurezza e privacy in Microsoft Azure Data Center](https://azure.microsoft.com/global-infrastructure/)  

- [Fiducia nel cloud attendibile](https://azure.microsoft.com/overview/trusted-cloud/)  

- [Centro protezione](https://www.microsoft.com/trustcenter)  
