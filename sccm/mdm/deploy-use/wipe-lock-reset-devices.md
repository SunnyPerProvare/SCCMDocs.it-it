---
title: Proteggere i dati con cancellazione remota, blocco remoto o reimpostazione passcode
titleSuffix: Configuration Manager
description: Proteggere i dati del dispositivo con cancellazione completa, cancellazione selettiva, blocco remoto o reimpostazione passcode usando System Center Configuration Manager.
ms.date: 10/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 670667c21e85d7e5c174c051b6adbdca3eba55a8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32353002"
---
# <a name="protect-data-with-remote-wipe-lock-or-passcode-reset-by-using-system-center-configuration-manager"></a>Proteggere i dati con cancellazione remota, blocco remoto o reimpostazione passcode usando System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager include funzionalità per la cancellazione selettiva, la cancellazione completa, il blocco remoto e la reimpostazione del passcode. I dispositivi mobili possono memorizzare i dati aziendali riservati e consentire l'accesso a numerose risorse aziendali. Per aiutare a proteggere i dispositivi è possibile eseguire:  

- Una cancellazione completa per ripristinare le impostazioni di fabbrica del dispositivo.  

- Una cancellazione selettiva per rimuovere solo i dati aziendali.  

- Un blocco remoto per proteggere un dispositivo che potrebbe andare perso.  

- Una reimpostazione del passcode del dispositivo.  

## <a name="full-wipe"></a>Cancellazione completa  
È possibile eseguire un comando di cancellazione del dispositivo se è necessario proteggere un dispositivo perso o se si ritira un dispositivo.  

Impartire un comando di **cancellazione completa** di un dispositivo per ripristinarne le impostazioni di fabbrica. Questo comando rimuove i dati e le impostazioni aziendali e dell'utente. È possibile eseguire una cancellazione completa nei dispositivi Windows Phone, iOS, Android e Windows 10.  

> [!NOTE]
> Nei dispositivi di proprietà dell'azienda è possibile eseguire solo una cancellazione completa.

> [!NOTE]
> La cancellazione nei dispositivi Windows 10 con versioni precedenti alla versione 1511 di meno di 4 GB di RAM potrebbe determinare la mancata risposta del dispositivo. [Altre informazioni](https://technet.microsoft.com/library/mt592024.aspx#full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram).

#### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>Per avviare una cancellazione remota dalla console di Configuration Manager  

1. Nella console di Configuration Manager selezionare **Asset e conformità** e scegliere **Dispositivi**. In alternativa, è possibile scegliere **Raccolte dispositivi** e selezionare una raccolta.  

2. Selezionare il dispositivo che si desidera ritirare/cancellare.  

3. Scegliere **Azioni dispositivo remoto** in **Gruppo di dispositivi** e quindi scegliere **Disattiva/Cancella**.  

## <a name="selective-wipe"></a>Cancellazione selettiva  
Eseguire una **cancellazione selettiva** per rimuovere solo i dati aziendali presenti sul dispositivo. La tabella seguente descrive i dati che vengono rimossi in base al tipo di piattaforma e l'effetto sui dati che rimangono sul dispositivo dopo la cancellazione selettiva.  

**iOS**  

|Contenuti rimossi quando si disattiva un dispositivo|iOS|  
|--------------------------------------------|---------|  
|App aziendali e dati associati installati usando Configuration Manager e Intune|Le app vengono disinstallate e vengono rimossi i dati dell'app aziendale.|  
|Profili VPN e Wi-Fi|Rimosso.|  
|Certificati|Rimossi e revocati.|  
|Impostazioni|Rimosse, tranne per: **Consenti chiamate in roaming**, **Consenti roaming dei dati** e **Consenti la sincronizzazione automatica durante il roaming**.|  
|Agente di gestione|Il profilo di gestione viene rimosso.|  
|Profili di posta elettronica|Per i profili di posta elettronica configurati da Intune, vengono rimossi l'account e l'indirizzo di posta elettronica.|  

**Android e Android Samsung KNOX Standard**  

|Contenuti rimossi quando si disattiva un dispositivo|Android|Samsung KNOX Standard|  
|--------------------------------------------|-------------|------------------|  
|App aziendali e dati associati installati usando Configuration Manager e Intune|Le app e i dati rimangono installati.|Le app vengono disinstallate|  
|Profili VPN e Wi-Fi|Rimosso.|Rimosso.|  
|Certificati|Revocati.|Revocati.|  
|Impostazioni|I requisiti vengono rimossi.|I requisiti vengono rimossi.|  
|Agente di gestione|Il privilegio di amministratore del dispositivo viene revocato.|Il privilegio di amministratore del dispositivo viene revocato.|  
|Profili di posta elettronica|Non applicabile.|Per i profili di posta elettronica configurati da Intune, vengono rimossi l'account e l'indirizzo di posta elettronica.|  

**Android for Work**

Quando si esegue la cancellazione selettiva in un dispositivo Android for Work, viene rimosso il profilo di lavoro insieme a tutti i dati, le app e le impostazioni presenti nel profilo di lavoro stesso sul dispositivo in questione. Questo impedisce la gestione del dispositivo con Configuration Manager e Intune. La cancellazione completa non è supportata per Android for Work.

 **Windows 10, Windows 8.1, Windows RT 8.1 e Windows RT**  

|Contenuti rimossi quando si disattiva un dispositivo|Windows 10, Windows 8.1 e Windows RT 8.1|  
|---------------------------------|-------------|
|App aziendali e dati associati installati usando Configuration Manager e Intune|Le app vengono disinstallate e le chiavi di trasferimento locale vengono rimosse. Alle app che usano la cancellazione selettiva di Windows verrà revocata la chiave di crittografia e i dati non saranno più accessibili.|  
|Profili VPN e Wi-Fi|Rimosso.|  
|Certificati|Rimossi e revocati.|  
|Impostazioni|I requisiti vengono rimossi.|
|Agente di gestione|Non applicabile. L'agente di gestione è incorporato.|  
|Profili di posta elettronica|Vengono rimosse le applicazioni di posta elettronica abilitate per EFS, tra cui i messaggi e gli allegati dell'applicazione Windows Mail.|  

 **Windows 10 Mobile, Windows Phone 8.0 e Windows Phone 8.1**

|Contenuti rimossi quando si disattiva un dispositivo|Windows 10 Mobile, Windows Phone 8 e Windows Phone 8.1|  
|-|-|
|App aziendali e dati associati installati usando Configuration Manager e Intune|Le app vengono disinstallate e vengono rimossi i dati dell'app aziendale.|  
|Profili VPN e Wi-Fi|Rimossi per Windows 10 Mobile e Windows Phone 8.1.|  
|Certificati|Rimosso per Windows Phone 8.1.|  
|Agente di gestione|Non applicabile. L'agente di gestione è incorporato.|  
|Profili di posta elettronica|Rimossi (ad eccezione di Windows Phone 8.0).|  

Le seguenti impostazioni vengono inoltre rimosse dai dispositivi Windows 10 Mobile e Windows Phone 8.1:  

- **Richiedi una password per sbloccare i dispositivi mobili**  
- **Consenti password semplici**  
- **Lunghezza minima password**  
- **Tipo di password richiesto**
- **Scadenza password (giorni)**  
- **Ricorda cronologia password**  
- **Numero di errori di accesso ripetuti consentiti prima della cancellazione del dispositivo**  
- **Minuti di inattività prima che venga richiesta la password**  
- **Tipo di password richiesto - numero minimo di set di caratteri**  
- **Consenti dispositivo foto/video**
- **Richiedi crittografia sui dispositivi mobili**  
- **Consenti archivi rimovibili**  
- **Consenti browser Web**  
- **Consenti archivio applicazioni**  
- **Consenti acquisizione schermo**  
- **Consenti georilevazione**  
- **Consenti account Microsoft**  
- **Consenti copia e incolla**  
- **Consenti tethering Wi-Fi**  
- **Consenti connessione automatica agli hotspot Wi-Fi gratuiti**  
- **Consenti creazione report degli hotspot Wi-Fi**  
- **Consenti ripristino impostazioni predefinite**
- **Consenti Bluetooth**  
- **Consenti NFC**
- **Consenti Wi-Fi**

#### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>Per avviare una cancellazione remota dalla console di Configuration Manager  

1. Nella console di Configuration Manager selezionare **Asset e conformità** e scegliere **Dispositivi**. In alternativa, è possibile scegliere **Raccolte dispositivi** e selezionare una raccolta.  

2. Selezionare il dispositivo che si desidera ritirare/cancellare.  

3. Scegliere **Azioni dispositivo remoto** in **Gruppo di dispositivi** e quindi scegliere **Disattiva/Cancella**.  

## <a name="wiping-efs-enabled-content"></a>Cancellazione dei contenuti abilitati EFS  
Windows 8.1 e Windows RT 8.1 supportano la cancellazione selettiva dei contenuti crittografati con EFS. Quanto descritto di seguito si applica alla cancellazione selettiva di contenuti abilitati EFS:  

- Solo le app e i dati protetti da EFS attraverso lo stesso dominio Internet come account Intune vengono cancellati in modo selettivo. Per altre informazioni, vedere [Cancellazione selettiva di Windows per la gestione di dati del dispositivo](http://technet.microsoft.com/library/dn486874.aspx).  

- In caso di modifiche al dominio associato con EFS, potranno essere necessarie fino a 48 ore prima che le app e i dati che usano il nuovo dominio siano cancellati in modo selettivo.  

- Ogni dominio registrato con Intune corrisponde al dominio che verrà cancellato.  

I dati e le app attualmente supportati dalla cancellazione selettiva EFS sono:  

- App di posta elettronica per Windows.  

- Cartelle di lavoro.

- File e cartelle crittografate con EFS. Per altre informazioni, vedere [Procedure ottimali per la crittografia del file system](http://support.microsoft.com/kb/223316).  

### <a name="best-practices-for-selective-wipe"></a>Procedure consigliate per la cancellazione selettiva  

- Per cancellare correttamente i messaggi di posta elettronica, configurare profili di posta elettronica nei dispositivi iOS e Windows Phone 8.1.  

- Per cancellare correttamente le app, assicurarsi che le app vengano distribuite con la gestione delle app per dispositivi mobili.  

- Per iOS, configurare l'impostazione **Consenti backup in iCloud** su **Non consentire** in modo che gli utenti non possano ripristinare il contenuto con iCloud.  

- Se un account è stato disattivato, dopo un anno Intune ritirerà l'account e verrà eseguita una cancellazione selettiva.  

##  <a name="passcode-reset"></a>Reimpostazione del passcode  
Se un utente dimentica il passcode, è possibile aiutarlo rimuovendo il passcode da un dispositivo oppure forzando l'uso di un nuovo passcode temporaneo su un dispositivo. La tabella seguente illustra il funzionamento della reimpostazione del passcode su diverse piattaforme per dispositivi mobili.  

| Piattaforma                              | Reimpostazione del passcode                                                                               |
|---------------------------------------|----------------------------------------------------------------------------------------------|
| iOS                                   | Funzionalità supportata per cancellare il passcode da un dispositivo. Non implica la creazione di un nuovo passcode temporaneo. |
| macOS                                 | Non supportata.                                                                               |
| Android                               | Supportata nelle versioni precedenti ad Android 7.0. Crea un passcode temporaneo.                |
| Android for Work                      | Non supportata.                                                                               |
| PC con Windows 10                        | Non supportata.                                                                               |
| Windows 10 Mobile                     | Funzionalità supportata; esclude i dispositivo aggiunti ad Azure AD.  |
| Windows Phone 8 e Windows Phone 8.1 | Supportata.                                                                                   |
| Windows RT 8.1                        | Non supportata.                                                                               |
| PC con Windows 8.1                       | Non supportata.                                                                               |

> [!Note]    
> È necessario eseguire l'operazione di reimpostazione del passcode dal sito di livello superiore nell'ambiente in uso. Ad esempio, se si usa un sito di amministrazione centrale è possibile eseguire l'azione solo in tale sito. Se si usa un sito primario autonomo è possibile eseguire l'azione solo in tale sito.

#### <a name="to-reset-the-passcode-on-a-mobile-device-remotely-in-configuration-manager"></a>Per reimpostare il passcode su un dispositivo mobile in modalità remota in Configuration Manager  

1. Nella console di Configuration Manager selezionare **Asset e conformità** e scegliere **Dispositivi**. In alternativa, è possibile scegliere **Raccolte dispositivi** e selezionare una raccolta.  

2. Selezionare il dispositivo o i dispositivi per cui si desidera reimpostare il passcode.  

3. Scegliere **Azioni dispositivo remoto** in **Gruppo di dispositivi** e quindi scegliere **Reimpostazione del passcode**.  

#### <a name="to-show-the-state-of-the-passcode-reset"></a>Per mostrare lo stato della reimpostazione del passcode  

1. Nella console di Configuration Manager selezionare **Asset e conformità** e scegliere **Dispositivi**. In alternativa, è possibile scegliere **Raccolte dispositivi** e selezionare una raccolta.  

2. Selezionare il dispositivo o i dispositivi per cui si desidera mostrare lo stato della reimpostazione del passcode.  

3. Scegliere **Azioni dispositivo remoto** in **Gruppo di dispositivi** e quindi scegliere **Mostra stato passcode**.  

## <a name="remote-lock"></a>Blocco remoto  
Se un utente perde il dispositivo, è possibile bloccare il dispositivo in modalità remota. Nella tabella seguente è illustrato il funzionamento del blocco remoto su diverse piattaforme per dispositivi mobili.  

|Piattaforma|Blocco remoto|  
|--------------|-----------------|  
|iOS|Supportata.|  
|Android|Supportata.|  
|Windows 10|Non supportato al momento.|  
|Windows Phone 8 e Windows Phone 8.1|Supportata.|  
|Windows RT 8.1 |Funzionalità supportata se l'utente corrente del dispositivo è lo stesso utente che ha registrato il dispositivo.|  
|Windows 8.1|Funzionalità supportata se l'utente corrente del dispositivo è lo stesso utente che ha registrato il dispositivo.|  

> [!Note]    
> È necessario eseguire l'operazione di blocco remoto dal sito di livello superiore nell'ambiente in uso. Ad esempio, se si usa un sito di amministrazione centrale è possibile eseguire l'azione solo in tale sito. Se si usa un sito primario autonomo è possibile eseguire l'azione solo in tale sito.

#### <a name="to-lock-a-mobile-device-remotely-through-the-configuration-manager-console"></a>Per bloccare un dispositivo mobile in modalità remota tramite la console di Configuration Manager  

1. Nella console di Configuration Manager selezionare **Asset e conformità** e scegliere **Dispositivi**. In alternativa, è possibile scegliere **Raccolte dispositivi** e selezionare una raccolta.  

2. Selezionare il dispositivo o i dispositivi da bloccare.  

3. Scegliere **Azioni dispositivo remoto** in **Gruppo di dispositivi** e quindi scegliere **Blocco remoto**.  

#### <a name="to-show-the-state-of-the-remote-lock"></a>Per mostrare lo stato del blocco remoto  

1. Nella console di Configuration Manager selezionare **Asset e conformità** e scegliere **Dispositivi**. In alternativa, è possibile scegliere **Raccolte dispositivi** e selezionare una raccolta.  

2. Selezionare il dispositivo per cui si desidera mostrare lo stato del blocco remoto.  

3. Scegliere **Azioni dispositivo remoto** in **Gruppo di dispositivi** e quindi scegliere **Mostra stato blocco remoto**.  

### <a name="see-also"></a>Vedere anche  
[Cancellazione selettiva di Windows per la gestione di dati del dispositivo](http://technet.microsoft.com/library/dn486874.aspx)   
