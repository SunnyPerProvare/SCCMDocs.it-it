---
title: Come creare elementi di configurazione per dispositivi Android for Work gestiti con Intune
titleSuffix: Configuration Manager
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ab6784fd-8c57-4be9-858f-50fe39f2ff5f
author: aczechowski
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1ebae22b8536c67fc5c912009b836185be3b17b6
ms.sourcegitcommit: 7dd42b5a280e64feb69a947dae082fdaf1571272
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66716248"
---
# <a name="how-to-create-configuration-items-for-android-for-work-devices-managed-with-intune"></a>Come creare elementi di configurazione per dispositivi Android for Work gestiti con Intune

 Usare l'elemento di configurazione **Android for Work** di System Center Configuration Manager per gestire le impostazioni dei dispositivi Android for Work registrati in Microsoft Intune o gestiti in locale da Configuration Manager.  

## <a name="create-an-android-for-work-configuration-item"></a>Creare un Android per un elemento di configurazione  

1. Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2. Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità**e quindi fare clic su **Elementi di configurazione**.  

3. Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea elemento di configurazione**.  

4. Nella pagina **Generale** della **Creazione guidata dell'elemento di configurazione**specificare un nome e una descrizione facoltativa per l'elemento di configurazione.  

5. In **Specificare il tipo di elemento di configurazione da creare** selezionare **Android for Work**.  

6. Scegliere **Categorie** se si vogliono creare e assegnare categorie per facilitare la ricerca e il filtraggio degli elementi di configurazione nella console di Configuration Manager.  

   Fare clic su **Avanti**.

7. Nella pagina **Impostazioni dispositivo** della procedura guidata selezionare i gruppi di impostazioni da configurare. Per informazioni dettagliate, vedere [Impostazioni degli elementi di configurazione di Android for Work](#android-for-work-configuration-item-settings-reference) e quindi fare clic su **Avanti**.  

   > [!TIP]  
   >  Se l'impostazione da modificare non è inclusa nell'elenco, selezionare la casella di controllo **Configura impostazioni aggiuntive non presenti nei gruppi di impostazioni predefinite**.  

8. In ogni pagina di impostazioni configurare le impostazioni necessarie e specificare se si vuole monitorarle e aggiornarle nel caso non siano conformi nei dispositivi (se questa funzionalità è supportata).  

9. Per ogni gruppo di impostazioni, è anche possibile configurare il livello di gravità che verrà segnalato quando viene trovato un elemento di configurazione non conforme, selezionando uno dei livelli seguenti:  

   -   **Nessuno**: i dispositivi che non soddisfano questa regola di conformità non segnalano una gravità dell'errore per i report di Configuration Manager.  

   -   **Informazioni**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Informazioni** per i report di Configuration Manager.  

   -   **Avviso**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Avviso** per i report di Configuration Manager.  

   -   **Errore critico**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Errore critico** per i report di Configuration Manager.  

   -   **Errore critico con evento**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Errore critico** per i report di Configuration Manager. Il livello di gravità viene anche registrato come un evento Windows nel log eventi dell'applicazione.  

10. Nella pagina **Applicabilità piattaforma** della creazione guidata, verificare le eventuali impostazioni non compatibili con le piattaforme supportate selezionate in precedenza. È possibile tornare indietro e rimuovere queste impostazioni oppure continuare.  

    > [!TIP]  
    >  Non viene valutata la conformità delle impostazioni non supportate.  

11. Completare la procedura guidata.  

    È possibile visualizzare il nuovo elemento di configurazione nel nodo **Elementi di configurazione** dell'area di lavoro **Asset e conformità** .  

##  <a name="android-for-work-configuration-item-settings-reference"></a>Informazioni di riferimento sulle impostazioni degli elementi di configurazione di Android for Work  

### <a name="password"></a>Password  

|Impostazione|Dettagli|  
|-------------|-------------|  
|**Richiedi impostazioni password nei dispositivi mobili**|Richiede una password nei dispositivi supportati.|  
|**Lunghezza minima password (caratteri)**|La lunghezza minima della password.|  
|**Scadenza password in giorni**|Il numero di giorni prima che sia necessario modificare una password.|  
|**Numero di password memorizzate**|Impedisce di usare di nuovo le password usate di recente.|  
|**Numero di tentativi di accesso non riusciti prima della cancellazione dei dati dal dispositivo**|Cancella il dispositivo se questo numero di tentativi di accesso ha esito negativo.|  
|**Tempo di inattività prima del blocco del dispositivo**|Selezionare il periodo di tempo in cui il dispositivo rimane inutilizzato prima che venga bloccato.|
|**Qualità password**|Selezionare il livello di complessità delle password necessario e indicare se possono essere usati anche dispositivi biometrici.|  
|**Consenti Smart Lock e altri agenti di attendibilità**|Consente di controllare la funzionalità Smart Lock su dispositivi compatibili con Android. Questa funzionalità del telefono, talvolta nota anche come agenti di attendibilità, consente di disabilitare o ignorare la password della schermata di blocco del dispositivo se il dispositivo si trova in una posizione attendibile, ad esempio quando è connesso a un dispositivo Bluetooth specifico oppure quando è nelle vicinanze di un tag NFC. È possibile usare questa impostazione per impedire agli utenti finali di configurare Smart Lock.|
|**Sblocco mediante impronta digitale**|&nbsp;|

###  <a name="work-profile"></a>Profilo di lavoro  
 Queste impostazioni si applicano solo ai dispositivi Samsung KNOX.  

|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Consenti la condivisione dei dati tra i profili di lavoro e personali**|È possibile scegliere tra:<br>- **Non configurato**<br>- **Restrizioni di condivisione predefinite**<br>- **Le app nel profilo di lavoro possono gestire una richiesta di condivisione dal profilo personale**<br>- **Le app nel profilo personale possono gestire una richiesta di condivisione dal profilo di lavoro**<br><br>Vedere anche l'uso di URI personalizzati per le [impostazioni di copia e incolla](#copy-paste-configuration-item-settings)|  
|**Nascondi le notifiche del profilo di lavoro quando il dispositivo è bloccato (Android 6.0+)**||
|**Imposta i criteri di autorizzazione predefiniti delle app (Android 6.0+)**|È possibile scegliere tra:<br>- **Non configurato**<br>- **Chiedi sempre conferma**<br>- **Concedi automaticamente**<br>- **Nega automaticamente**|

### <a name="copy-paste-configuration-item-settings"></a>Impostazioni degli elementi di configurazione di copia e incolla
Nessuna delle opzioni di **Consenti la condivisione dei dati tra i profili di lavoro e personali** impedisce il comportamento di copia e incolla. Usare un'impostazione personalizzata che può essere configurata per impedire le operazioni di copia e incolla. L'impostazione è configurabile tramite un URI personalizzato.

- URI OMA: ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
- Tipo valore: Boolean

Impostando DisallowCrossProfileCopyPaste su true si impedisce il comportamento di copia e incolla tra Android for Work personale e i profili di lavoro.

## <a name="see-also"></a>Vedere anche  
 [Elementi di configurazione per dispositivi gestiti senza il client di System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
