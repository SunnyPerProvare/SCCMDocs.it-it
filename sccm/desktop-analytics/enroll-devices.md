---
title: Registrare i dispositivi in desktop Analytics
titleSuffix: Configuration Manager
description: Informazioni su come registrare i dispositivi in desktop Analytics.
ms.date: 10/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ab19d24e62f8454a2fc7f4366b8a4cf2fc510481
ms.sourcegitcommit: c25a91db838805eca5dbb421a3de401928968bf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/30/2019
ms.locfileid: "73142969"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>Come registrare i dispositivi in desktop Analytics

Quando ci si [connette Configuration Manager](/sccm/desktop-analytics/connect-configmgr) a desktop Analytics, si configurano le impostazioni per la registrazione dei dispositivi in analisi desktop. È possibile modificare queste impostazioni in qualsiasi momento. Assicurarsi inoltre che i dispositivi siano aggiornati.



## <a name="update-devices"></a>Aggiornare i dispositivi

Esistono due tipi di aggiornamenti che è necessario applicare per un'esperienza ottimale con l'analisi del desktop:

- [Aggiornamenti per la compatibilità](#bkmk_appraiser)  
- [Esperienza utente connessa e servizio di telemetria](#bkmk_diagtrack)


### <a name="bkmk_appraiser"></a>Aggiornamenti per la compatibilità

Il componente Compatibility (Estimator) esegue la diagnostica sul dispositivo Windows per valutarne lo stato di compatibilità con le versioni più recenti di Windows 10.

Microsoft incrementa regolarmente gli aggiornamenti per questo componente, ma il numero di KB associato non cambia. Assicurarsi di disporre sempre della versione più recente dell'aggiornamento.

Riavviare i dispositivi dopo aver installato gli aggiornamenti per la compatibilità per la prima volta.

> [!Tip]  
> Usare Configuration Manager per installare automaticamente la versione più recente di questi aggiornamenti. Per altre informazioni, vedere [Distribuire gli aggiornamenti software](/sccm/sum/deploy-use/deploy-software-updates).  

> [!Note]  
> È disponibile un aggiornamento facoltativo correlato, [KB 3150513](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=3150513). Questo aggiornamento fornisce la configurazione aggiornata e le definizioni per gli aggiornamenti di compatibilità precedenti. Per ulteriori informazioni, vedere l' [aggiornamento più recente per la definizione di compatibilità per Windows](https://support.microsoft.com/help/3150513).  

#### <a name="windows-10"></a>Windows 10

Windows 10 include il componente compatibilità. Per ottenere l'aggiornamento più recente per la compatibilità, installare l'aggiornamento cumulativo più recente di Windows 10.

#### <a name="windows-81"></a>Windows 8,1

Scaricare l'aggiornamento: [KB 2976978](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2976978) 

Esegue la diagnostica nei sistemi Windows 8.1 che partecipano al Analisi utilizzo software di Windows. Questi dati consentono di determinare se è possibile che si verifichino problemi di compatibilità durante l'aggiornamento a Windows 10.

Per ulteriori informazioni, vedere [aggiornamento della compatibilità per mantenere aggiornato Windows in Windows 8.1](https://support.microsoft.com/help/2976978).

#### <a name="windows-7-with-service-pack-1"></a>Windows 7 con Service Pack 1

Scaricare l'aggiornamento: [KB 2952664](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2952664) 

Esegue la diagnostica nei sistemi Windows 7 con Service Pack 1 (SP1) che partecipano al Analisi utilizzo software di Windows. Questi dati consentono di determinare se è possibile che si verifichino problemi di compatibilità durante l'aggiornamento a Windows 10.

Per ulteriori informazioni, vedere [aggiornamento della compatibilità per mantenere Windows aggiornato in Windows 7](https://support.microsoft.com/help/2952664).


### <a name="bkmk_diagtrack"></a>Esperienza utente connessa e servizio di telemetria

Con i dati di diagnostica di Windows abilitati, l'esperienza utente connessa e il servizio di telemetria (DiagTrack) raccolgono i dati del sistema, dell'applicazione e del driver. Microsoft analizza questi dati e li condivide nuovamente con l'utente tramite desktop Analytics.

Per un'esperienza ottimale, installare gli aggiornamenti seguenti a seconda della versione del sistema operativo.

> [!Note]  
> Quando si installano questi aggiornamenti, prevedere i comportamenti seguenti:
> 
> - I dispositivi registrati per desktop Analytics vengono visualizzati nel servizio in meno di un'ora  
> - I dispositivi segnalano rapidamente lo stato degli aggiornamenti di qualità e funzionalità di Windows  
>
> Senza questi aggiornamenti, questi processi possono richiedere più di 48 ore affinché un dispositivo segnali a desktop Analytics.  


#### <a name="windows-10"></a>Windows 10

Installare l'aggiornamento cumulativo più recente di Windows 10.

<!-- 
- Windows 10 1809: Included in RTM build
- Windows 10 1803: [KB4458469](https://support.microsoft.com/help/4458469) (OS Build 17134.319)
- Windows 10 1709: [KB4457136](https://support.microsoft.com/help/4457136) (OS Build 16299.697)
- Windows 10 1703: [KB4457141](https://support.microsoft.com/help/4457141) (OS Build 15063.1358)
- Windows 10 1607: [KB4457127](https://support.microsoft.com/help/4457127) (OS Build 14393.2517)
 -->

#### <a name="windows-81"></a>Windows 8,1

Installare il rollup mensile del 2018 ottobre, [KB4462926](https://support.microsoft.com/help/4462926)

#### <a name="windows-7"></a>Windows 7

Installare il rollup mensile del 2018 ottobre, [KB4462923](https://support.microsoft.com/help/4462923)



## <a name="device-enrollment"></a>Registrazione del dispositivo

Il servizio desktop Analytics non ha agenti da installare. Per la registrazione del dispositivo è necessario configurare le impostazioni nei dispositivi che si desidera monitorare. Queste impostazioni controllano l'istanza di desktop Analytics a cui il dispositivo deve inviare i dati e altre opzioni di configurazione.

> [!Note]  
> Se si sta già usando Windows Analytics, usare la stessa area di lavoro per l'analisi desktop. È necessario registrare nuovamente i dispositivi in desktop Analytics registrati in precedenza in Windows Analytics.
>
> È possibile avere solo un'area di lavoro di analisi desktop per ogni tenant Azure AD. I dispositivi possono inviare i dati di diagnostica solo a un'area di lavoro.  

Configuration Manager offre un'esperienza integrata per la gestione e la distribuzione di queste impostazioni ai client. Per un'esperienza ottimale, usare Configuration Manager.

Quando ci si connette Configuration Manager a desktop Analytics, si configurano le impostazioni per la registrazione dei dispositivi. Per altre informazioni, vedere [How to connect Configuration Manager with desktop Analytics](/sccm/desktop-analytics/connect-configmgr#bkmk_connect).

Per modificare queste impostazioni, attenersi alla procedura seguente:

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**. Selezionare la connessione a desktop Analytics e scegliere **Proprietà** nella barra multifunzione.

2. Nella pagina **dati di diagnostica** apportare le modifiche necessarie alle seguenti impostazioni:  

    - **ID commerciale**: questo valore deve essere popolato automaticamente con l'ID dell'organizzazione. In caso contrario, assicurarsi che il server proxy sia configurato per consentire tutti gli [endpoint](/sccm/desktop-analytics/enable-data-sharing#endpoints) necessari prima di continuare. In alternativa, recuperare manualmente l'ID commerciale dal [portale di analisi dei desktop](/sccm/desktop-analytics/monitor-connection-health#bkmk_ViewCommercialID).   

    - **Livello dati di diagnostica di Windows 10**: per altre informazioni, vedere [livelli di dati di diagnostica](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

    - **Consenti nome dispositivo nei dati di diagnostica**: per altre informazioni, vedere [nome dispositivo](#device-name).  

    Quando si apportano modifiche a questa pagina, nella pagina **funzionalità disponibili** viene visualizzata un'anteprima della funzionalità di analisi del desktop con le impostazioni dei dati di diagnostica selezionate.  

3. Nella pagina **connessione a desktop Analytics** apportare le modifiche necessarie alle seguenti impostazioni:

    - **Nome visualizzato**: il portale di analisi del desktop Visualizza questa connessione Configuration Manager usando questo nome.  

    - **Raccolta di destinazione**: questa raccolta include tutti i dispositivi che Configuration Manager configura con l'ID commerciale e le impostazioni dei dati di diagnostica. Si tratta del set completo di dispositivi che Configuration Manager si connette al servizio desktop Analytics.  

    - **I dispositivi nella raccolta di destinazione usano un proxy autenticato dall'utente per le comunicazioni in uscita**: per impostazione predefinita, questo valore è **No**. Se necessario nell'ambiente in uso, impostare su **Sì**. Per ulteriori informazioni, vedere [autenticazione del server proxy](/sccm/desktop-analytics/enable-data-sharing#proxy-server-authentication).  

    - **Selezionare raccolte specifiche da sincronizzare con analisi desktop**: selezionare **Aggiungi** per includere raccolte aggiuntive dalla gerarchia della **raccolta di destinazione** . Queste raccolte sono disponibili nel portale di analisi del desktop per il raggruppamento con i piani di distribuzione. Assicurarsi di includere le raccolte di esclusioni pilota e pilota.  <!-- 4097528 -->

        > [!Important] 
        > Queste raccolte continuano a essere sincronizzate in seguito alla modifica dell'appartenenza. Il piano di distribuzione, ad esempio, usa una raccolta con una regola di appartenenza di Windows 7. Quando i dispositivi eseguono l'aggiornamento a Windows 10 e Configuration Manager valuta l'appartenenza alla raccolta, tali dispositivi rilasciano il piano di raccolta e di distribuzione.  


### <a name="windows-settings"></a>Impostazioni di Windows

Configuration Manager imposta i criteri di Windows in una o in entrambe le chiavi del registro di sistema seguenti:

- **Criteri it**: `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

- Preferenza **utente** : `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`

| Criteri   | Percorso | Valore  | 
|----------|------|--------|
| **CommercialId** | utente | *Si applica a Windows 7, Windows 8.1 e Windows 10*: per consentire la visualizzazione di un dispositivo in analisi desktop, configurarlo con l'ID commerciale dell'organizzazione. | 
| **AllowTelemetry**  | Criteri IT | *Si applica a Windows 10*: impostare `1` per **Basic**, `2` per **Enhanced**o `3` per i dati di diagnostica **completi** . Per desktop Analytics sono necessari almeno i dati di diagnostica di base. Microsoft consiglia di usare il livello avanzato (limitato) con analisi desktop. Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization) (Configurare i dati di diagnostica di Windows nell'organizzazione). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | Criteri IT | *Si applica a Windows 10, versione 1803 e successive*: questa impostazione si applica solo quando l'impostazione AllowTelemetry è `2`. Limita gli eventi dati di diagnostica avanzati inviati a Microsoft solo agli eventi richiesti da desktop Analytics. Per ulteriori informazioni, vedere [gli eventi e i campi dei dati di diagnostica di Windows 10 raccolti tramite il limite dei criteri dati di diagnostica avanzati](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields).|
| **AllowDeviceNameInTelemetry** | Criteri IT | *Si applica a Windows 10, versione 1803 e successive*: è necessario un consenso esplicito per consentire ai dispositivi di continuare a inviare il nome del dispositivo.<br> <br>Nota: per impostazione predefinita, il nome del dispositivo non viene inviato a Microsoft. Se non si invia il nome del dispositivo, questo viene visualizzato in desktop Analytics come "sconosciuto". Questo comportamento può rendere difficile l'identificazione e la valutazione dei dispositivi. Per altre informazioni, vedere [nome dispositivo](#device-name). | 
| **E** | utente |*Si applica a Windows 7 e Windows 8.1*: è necessario un valore di `1` per analisi desktop. Per ulteriori informazioni, vedere la pagina relativa al [consenso esplicito ai dati commerciali in Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |
| **Commercialdataoptin** | Entrambi |*Si applica a tutte le versioni di Windows*: il valore `1` è necessario per il corretto funzionamento della raccolta dei dati di analisi del desktop. | 
| **DisableEnterpriseAuthProxy** | Criteri IT |*Si applica a tutte le versioni di Windows*: il valore `0` è necessario per il corretto funzionamento della raccolta dei dati di analisi del desktop. | 

> [!Important]  
> Nella maggior parte dei casi, usare solo Configuration Manager per configurare queste impostazioni. Non applicare anche queste impostazioni negli oggetti Criteri di gruppo del dominio. Per ulteriori informazioni, vedere [risoluzione dei conflitti](#conflict-resolution).<!-- SCCMDocs-pr 3120 -->

### <a name="device-name"></a>Nome dispositivo

A partire da Windows 10, versione 1803, il nome del dispositivo non viene più raccolto per impostazione predefinita. Per raccogliere il nome del dispositivo con i dati di diagnostica, è necessario un consenso esplicito. Senza il nome del dispositivo, è più difficile identificare i dispositivi che richiedono attenzione durante la valutazione di un aggiornamento a una nuova versione di Windows.

Se non si invia il nome del dispositivo, questo viene visualizzato in desktop Analytics come "sconosciuto".

![Elenco dei dispositivi di analisi desktop che mostra i nomi "sconosciuti"](media/unknown-device-name.png)

Per configurare questa opzione, è disponibile un'opzione nel Configuration Manager impostazioni per desktop Analytics: **Consenti nome dispositivo nei dati di diagnostica**. Questa impostazione Configuration Manager controlla l'impostazione dei criteri di Windows, AllowDeviceNameInTelemetry.
 

### <a name="conflict-resolution"></a>Risoluzione dei conflitti

In generale, usare le raccolte di Configuration Manager per individuare le impostazioni e la registrazione di desktop Analytics. Usare l'appartenenza diretta o le query per includere o escludere i dispositivi dalla raccolta. Per altre informazioni, vedere [Come creare le raccolte](/sccm/core/clients/manage/collections/create-collections).

Configuration Manager configura le impostazioni di Windows solo se un valore non esiste già. Se è necessario configurare impostazioni diverse per un gruppo univoco di dispositivi, è possibile utilizzare [criteri di gruppo](#windows-settings). 

Visualizzare queste impostazioni nell'Editor criteri di gruppo nel percorso seguente: **Configurazione Computer**  > **modelli amministrativi**  > **componenti di Windows**  > **compilazioni raccolta dati e anteprima**. Le impostazioni di destinazione di criteri di gruppo hanno la precedenza sulle impostazioni Configuration Manager.

Se si hanno come destinazione Configuration Manager client con le impostazioni di Windows Analytics e di analisi desktop, le impostazioni di desktop Analytics hanno la precedenza.

Quando si configura il livello dati di diagnostica, è necessario impostare il limite superiore per il dispositivo. Per impostazione predefinita, in Windows 10, versione 1803 e successive, gli utenti possono scegliere di impostare un livello inferiore. È possibile controllare questo comportamento usando l'impostazione di criteri di gruppo, **configurare l'impostazione del consenso esplicito per la telemetria dell'interfaccia utente**. Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management) (Configurare i dati di diagnostica di Windows nell'organizzazione).



## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per creare piani di distribuzione in desktop Analytics.
> [!div class="nextstepaction"]  
> [Creare piani di distribuzione](/sccm/desktop-analytics/create-deployment-plans)  
