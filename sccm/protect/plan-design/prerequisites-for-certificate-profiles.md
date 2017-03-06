---
title: Prerequisiti per i profili certificato | Microsoft Docs
description: Informazioni sui profili certificato in System Center Configuration Manager e sulle dipendenze esterne e dipendenze nel prodotto.
ms.custom: na
ms.date: 11/27/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0317fd02-3721-4634-b18b-7c976a4e92bf
caps.latest.revision: 9
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 593fbd0587d54490246f48ae54f666bac6b7830d
ms.openlocfilehash: 08fb30da2060728142648f13846be737f98f2276
ms.lasthandoff: 12/16/2016


---
# <a name="prerequisites-for-certificate-profiles-in-system-center-configuration-manager"></a>Prerequisiti per i profili certificato in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


I profili certificato in System Center Configuration Manager (noto anche come ConfigMgr o SCCM) hanno dipendenze esterne e dipendenze nel prodotto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dipendenze esterne a Configuration Manager  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|Un'autorità di certificazione emittente globale (enterprise) che esegue Servizi certificati Active Directory (AD CS).<br /><br /> Per revocare i certificati, per l'account computer del server del sito al livello superiore della gerarchia sono necessari i diritti *Rilascio e gestione certificati* per ogni modello di certificato usato da un profilo certificato in Configuration Manager. In alternativa, concedere le autorizzazioni di gestore di certificati per concedere le autorizzazioni per tutti i modelli di certificato usati da tale autorità di certificazione.<br /><br /> È supportata l'approvazione manager per richieste certificato. I modelli di certificato usati per emettere certificati devono essere tuttavia configurati per **Inserisci nella richiesta** per l'oggetto del certificato in modo che System Center Configuration Manager sia in grado di inserire automaticamente questo valore.|Per altre informazioni su Servizi certificati Active Directory, vedere la documentazione di Windows Server.<br /><br /> Per Windows Server 2012: [Panoramica su Servizi certificati Active Directory](http://go.microsoft.com/fwlink/p/?LinkId=286744)<br /><br /> Per Windows Server 2008: [Panoramica su Servizi certificati Active Directory in Windows Server 2008](http://go.microsoft.com/fwlink/p/?LinkId=115018)|  
|Il servizio del ruolo del servizio Registrazione dispositivi di rete per Servizi certificati Active Directory, in esecuzione su Windows Server 2012 R2.<br /><br /> Inoltre:<br /><br /> Numeri di porta diversi da TCP 443 (per HTTPS) o TCP 80 (HTTP) non sono supportati per la comunicazione tra il client e il servizio Registrazione dispositivi di rete.<br /><br /> Il server che esegue il servizio Registrazione dispositivi di rete deve essere in un server diverso dalla CA emittente.|System Center Configuration Manager comunica con il servizio Registrazione dispositivi di rete in Windows Server 2012 R2 per generare e verificare richieste Simple Certificate Enrollment Protocol (SCEP).<br /><br /> Se vengono emessi certificati a utenti o dispositivi che si collegano da Internet, ad esempio dispositivi mobili gestiti da Microsoft Intune, questi dispositivi devono essere in grado di accedere al server che esegue il servizio Registrazione dispositivi di rete da Internet. Ad esempio, installare il server in una rete perimetrale (nota anche come subnet schermata).<br /><br /> Se tra il server che esegue il servizio Registrazione dispositivi di rete e la CA emittente è presente un firewall, configurarlo per consentire il traffico di comunicazione (DCOM) tra i due server. Questo requisito firewall si applica anche al server che esegue il sito del server di System Center Configuration Manager e la CA emittente, in modo che System Center Configuration Manager possa revocare i certificati.<br /><br /> Se il servizio Registrazione dispositivi di rete è configurato per richiedere SSL (una procedura consigliata per la sicurezza) accertarsi che i dispositivi di connessione siano in grado di accedere all'elenco di revoche di certificati (CRL) per convalidare il certificato del server.<br /><br /> Per altre informazioni sul servizio Registrazione dispositivi di rete in Windows Server 2012 R2, vedere [Utilizzo di un Modulo criteri con il servizio Registrazione dispositivi di rete](http://go.microsoft.com/fwlink/p/?LinkId=328657).|  
|Se la CA emittente esegue Windows Server 2008 R2, questo server richiede un hotfix per le richieste di rinnovo SCEP.|Se l'hotfix non è già installato sul computer della CA emittente, installarlo. Per altre informazioni, vedere l'articolo [2483564: Impossibile rinnovare richiesta per un certificato SCEP in Windows Server 2008 R2 se il certificato viene gestito usando NDES](http://go.microsoft.com/fwlink/?LinkId=311945) nella Microsoft Knowledge Base.|  
|Un certificato di autenticazione client PKI e un certificato CA radice esportato.|Questo certificato autentica il server che esegue il servizio Registrazione dispositivi di rete in System Center Configuration Manager.<br /><br /> Per altre informazioni, vedere [Requisiti dei certificati PKI per System Center Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md).|  
|Sistemi operativi per i dispositivi supportati.|È possibile distribuire i profili certificato in dispositivi che eseguono sistemi operativi iOS, Windows 8.1, Windows RT 8.1, Windows 10 e Android.|  

## <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|Ruolo del sistema del sito punto di registrazione certificati|Prima di usare profili certificato, è necessario installare il ruolo del sistema del sito del punto di registrazione certificati. Questo ruolo comunica con il database, il server del sito e il modulo criteri di System Center Configuration Manager.<br /><br /> Per altre informazioni sui requisiti di sistema per questo ruolo del sistema del sito e sul relativo percorso di installazione nella gerarchia, vedere la sezione **Requisiti di sistema del sito** dell'argomento [Configurazioni supportate per System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md).<br /><br /> Si noti che il punto di registrazione certificati non deve essere installato sullo stesso server che esegue il servizio Registrazione dispositivi di rete.|  
|Modulo criteri di System Center Configuration Manager installato nel server che esegue il servizio del ruolo del servizio Registrazione dispositivi di rete per servizi certificati Active Directory|Per distribuire i profili certificato, è necessario installare il modulo criteri di System Center Configuration Manager. È possibile trovare questo modulo criteri nel supporto di installazione di System Center Configuration Manager.|  
|Dati di individuazione|I valori per l'oggetto del certificato e il nome alternativo dell'oggetto vengono specificati da System Center Configuration Manager e recuperati dalle informazioni raccolte dall'individuazione:<br /><br /> Per i certificati utente: individuazione utente Active Directory<br /><br /> Per i certificati computer: individuazione sistema e individuazione della rete Active Directory|  
|Autorizzazioni di protezione specifiche per la gestione dei profili certificato|L'utente deve disporre delle seguenti autorizzazioni di sicurezza per gestire le impostazioni di accesso alle risorse aziendali, ad esempio profili certificati, profili VPN e profili Wi-Fi:<br /><br /> Per visualizzare e gestire avvisi e report per i profili certificato: **Crea**, **Elimina**, **Modifica**, **Modifica report**, **Lettura**ed **Esegui report** per l'oggetto **Avvisi** .<br /><br /> Per creare e gestire profili certificato: **Criteri autore**, **Modifica report**, **Lettura** ed **Esegui report** per l'oggetto **Profilo certificato** .<br /><br /> Per gestire le distribuzioni di profili Wi-Fi, certificato e VPN: **Distribuisci criteri di configurazione**, **Modifica avviso stato client**, **Lettura**e **Leggi risorsa** per l'oggetto **Raccolta** .<br /><br /> Per gestire tutti i criteri di configurazione: **Crea**, **Elimina**, **Modifica**, **Lettura** e **Imposta ambito di protezione** per l'oggetto **Criteri di configurazione** .<br /><br /> Per eseguire query correlate ai profili certificato: autorizzazione **Lettura** per l'oggetto **Query** .<br /><br /> Per visualizzare le informazioni sui profili certificato nella console di System Center Configuration Manager: autorizzazione **Lettura** per l'oggetto **Sito**.<br /><br /> Per visualizzare i messaggi di stato per i profili certificato: autorizzazione **Lettura** per l'oggetto **Messaggi di stato** .<br /><br /> Per creare e modificare il profilo del certificato CA attendibile: **Criteri autore**, **Modifica report**, **Lettura** ed **Esegui report** per l'oggetto **Profilo certificato CA attendibile** .<br /><br /> Per creare e gestire profili VPN: **Criteri autore**, **Modifica report**, **Lettura** ed **Esegui report** per l'oggetto **Profilo VPN** .<br /><br /> Per creare e gestire profili Wi-Fi: **Criteri autore**, **Modifica report**, **Lettura** ed **Esegui report** per l'oggetto **Profilo Wi-Fi** .<br /><br /> Il ruolo di sicurezza **Gestione accesso risorse aziendali** include queste autorizzazioni necessarie per gestire i profili certificato in System Center Configuration Manager. Per ulteriori informazioni, vedere la sezione **Configure role-based administration** nell'argomento [Configure security in System Center Configuration Manager](../../core/plan-design/security/configure-security.md) .|  

