---
title: Creare elementi di configurazione per Windows 10 gestito da client - Configuration Manager | Microsoft Docs
description: Usare l'elemento di configurazione Windows 10 in System Center Configuration Manager per gestire le impostazioni dei computer Windows 10 gestiti dal client di Configuration Manager.
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 14226fbe-dd07-4432-910b-130790624a4e
caps.latest.revision: "17"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: e0a42a1d4706ab29617f3b6f8960ece27672908b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-configuration-items-for-windows-10-devices-managed-with-the-system-center-configuration-manager-client"></a>Come creare elementi di configurazione per dispositivi Windows 10 gestiti con il client di System Center Configuration Manager
Usare l'elemento di configurazione **Windows 10** in System Center Configuration Manager per gestire le impostazioni dei computer che eseguono Windows 10 gestiti dal client di Configuration Manager.  
  
> [!IMPORTANT]  
>  In questa versione, se all'interno di un elemento di configurazione di tipo **Windows 10** (per un dispositivo gestito con il client di Configuration Manager) è stata creata un'impostazione **Password** che non esiste ancora o non è stata configurata nel dispositivo Windows 10, viene erroneamente valutata come conforme.  
>   
>  Come soluzione alternativa, quando si crea un'impostazione per questi dispositivi assicurarsi che sia selezionata l'opzione **Monitora e aggiorna impostazioni non conformi** nelle pagine delle impostazioni della Creazione guidata dell'elemento di configurazione. Inoltre, quando si distribuisce una linea di base di configurazione contenente un elemento di configurazione di Windows 10 con impostazioni di password al suo interno, selezionare **Monitora e aggiorna le regole non conformi, se supportato** nella finestra di dialogo Distribuisci linee di base di configurazione. L'uso di questa soluzione alternativa consente di monitorare l'impostazione e di correggerla se risulta non conforme. Dopo la correzione, l'impostazione verrà correttamente segnalata come **Conforme** , a meno che non venga rilevato un problema, nel qual caso verrà segnalata con **Errore**.  
  
### <a name="to-create-a-windows-10-configuration-item"></a>Per creare un elemento di configurazione Windows 10  
  
1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  
  
2.  Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità**e quindi fare clic su **Elementi di configurazione**.  
  
3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea elemento di configurazione**.  
  
4.  Nella pagina **Generale** della **Creazione guidata dell'elemento di configurazione**specificare un nome e una descrizione facoltativa per l'elemento di configurazione.  
  
5.  In **Specificare il tipo di elemento di configurazione da creare**selezionare **Windows 10**.  
  
6.  Fare clic su **Categorie** se si vogliono creare e assegnare categorie per facilitare la ricerca e il filtraggio degli elementi di configurazione nella console di Configuration Manager.  
  
7.  Nella pagina **Piattaforme supportate** della procedura guidata selezionare le piattaforme Windows 10 specifiche che valuteranno l'elemento di configurazione.  
  
8.  Nella pagina **Impostazioni dispositivo** della creazione guidata selezionare il gruppo di impostazioni da configurare. Per dettagli, vedere [Windows 10 configuration item settings reference](#BKMK_Ref) in questo argomento e quindi fare clic su **Avanti**.  
  
    > [!TIP]  
    >  Se l'impostazione da modificare non è inclusa nell'elenco, selezionare la casella di controllo **Configura impostazioni aggiuntive non presenti nei gruppi di impostazioni predefinite**.  
  
9. In ogni pagina di impostazioni configurare le impostazioni necessarie e specificare se si vuole monitorarle e aggiornarle nel caso non siano conformi nei dispositivi (se questa funzionalità è supportata).  
  
10. Per ogni gruppo di impostazioni, è anche possibile configurare il livello di gravità che verrà segnalato quando viene trovato un elemento di configurazione non conforme, selezionando uno dei livelli seguenti:  
  
    -   **Nessuno**: i dispositivi che non soddisfano questa regola di conformità non segnalano una gravità dell'errore per i report di Configuration Manager.  
  
    -   **Informazioni**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Informazioni** per i report di Configuration Manager.  
  
    -   **Avviso**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Avviso** per i report di Configuration Manager.  
  
    -   **Errore critico**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Errore critico** per i report di Configuration Manager.  
  
    -   **Errore critico con evento**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Errore critico** per i report di Configuration Manager. Il livello di gravità viene anche registrato come un evento Windows nel log eventi dell'applicazione.  
  
11. Nella pagina **Applicabilità piattaforma** della creazione guidata, verificare le eventuali impostazioni non compatibili con le piattaforme supportate selezionate in precedenza. È possibile tornare indietro e rimuovere queste impostazioni oppure continuare.  
  
    > [!TIP]  
    >  Non viene valutata la conformità delle impostazioni non supportate.  
  
12. Completare la procedura guidata.  
  
 È possibile visualizzare il nuovo elemento di configurazione nel nodo **Elementi di configurazione** dell'area di lavoro **Asset e conformità** .  
  
##  <a name="windows-10-configuration-item-settings-reference"></a>Informazioni di riferimento sulle impostazioni degli elementi di configurazione di Windows 10  
  
### <a name="password"></a>Windows 10  
  
|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Richiedi impostazioni password nei dispositivi mobili**|Richiede una password nei dispositivi supportati.|  
|**Lunghezza minima password (caratteri)**|Lunghezza minima della password.|  
|**Scadenza password in giorni**|Numero di giorni prima che sia necessario modificare la password.|  
|**Numero di password memorizzate**|Impedisce il riutilizzo delle password precedenti.|  
|**Numero di tentativi di accesso non riusciti prima della cancellazione dei dati da un dispositivo**|Cancella il dispositivo se l'accesso non riesce per il numero di volte indicato.|  
|**Tempo di inattività prima del blocco del dispositivo**|Specifica quanti minuti il dispositivo deve restare inattivo prima che venga bloccato automaticamente.|  
|**Complessità password**|Scegliere se è possibile specificare un PIN, ad esempio "1234", o se è necessario fornire una password complessa.|
|**Numero di set di caratteri complessi richiesti nella password**|Se è stata scelta una password **complessa**, usare questa impostazione per configurare il numero di set di caratteri complessi necessari. Per ottenere una password complessa, il valore deve essere impostato almeno su **3**, ovvero sono necessari lettere e numeri. Selezionare **4** per imporre una password che richiede anche caratteri speciali, ad esempio **(% $**.<br>(solo Windows 10)  |
  
###  <a name="device"></a>Dispositivo  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Bluetooth**|Consente l'uso della funzionalità Bluetooth nel dispositivo.|  
  
### <a name="cloud"></a>Cloud  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Sincronizzazione impostazioni**|Consente la sincronizzazione delle impostazioni tra i dispositivi.|  
|**Sincronizzazione credenziali**|Consente la sincronizzazione delle credenziali tra i dispositivi.|  
|**Sincronizzazione delle impostazioni con connessione a consumo**|Consente la sincronizzazione delle impostazioni quando la connessione a Internet è a consumo.|  
  
### <a name="roaming"></a>Roaming  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Roaming dati**|Consente il roaming tra reti quando si accede a dati.|  
  
### <a name="encryption"></a>Crittografia  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Crittografia file nel dispositivo mobile**|Richiede la crittografia dei file nel dispositivo.|  
  
### <a name="system-security"></a>Protezione del sistema  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Controllo dell'account utente**|Configura la modalità di funzionamento del controllo account utente di Windows nel dispositivo.<br />Ad esempio, è possibile disabilitare questa funzione o impostare il livello in corrispondenza del quale l'utente riceve una notifica.|  
|**Firewall di rete**|Attiva o disattiva Windows Firewall.|  
|**SmartScreen**|Abilita o disabilita Windows SmartScreen.|  
|**Protezione da virus**|Richiede che sia installato e configurato software antivirus.|  
|**Le firme per la protezione da virus sono aggiornate**|Richiede che i file di firma per il software antivirus nel dispositivo siano aggiornati.|  
  
### <a name="windows-information-protection-wip"></a>Windows Information Protection (WIP)

Con l'aumento dei dispositivi personali nell'organizzazione, aumenta anche il rischio di perdita accidentale dei dati tramite app e servizi, ad esempio posta elettronica, social media e cloud pubblico, non controllati dall'organizzazione. È il caso, ad esempio, di un dipendente che invia le immagini di progettazione più recenti dall'account di posta elettronica personale, copia e incolla le informazioni su un prodotto in un tweet o salva il report di una vendita in corso nell'area di archiviazione nel cloud pubblico.

Windows Information Protection, in precedenza denominato Protezione dei dati aziendali, offre protezione da questa potenziale perdita di dati senza interferire con l'esperienza del dipendente. Consente anche di proteggere le app e i dati aziendali da perdite di dati accidentali su dispositivi di proprietà dell'azienda e dispositivi personali che i dipendenti portano al lavoro senza richiedere modifiche all'ambiente o ad altre app.

 In Configuration Manager gli elementi di configurazione di Windows Information Protection gestiscono l'elenco di app protette da WIP, i percorsi di rete aziendali, il livello di protezione e le impostazioni di crittografia.
  

Per informazioni su come configurare Windows Information Protection con Configuration Manager, vedere [Proteggere i dati aziendali con Windows Information Protection (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip).
  
## <a name="see-also"></a>Vedere anche  
 [Elementi di configurazione per dispositivi gestiti con il client di System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md)
