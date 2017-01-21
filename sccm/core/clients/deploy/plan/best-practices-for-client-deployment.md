---
title: Procedure consigliate per la distribuzione client | Microsoft Docs
description: Apprendere le procedure consigliate per la distribuzione client in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
caps.latest.revision: 11
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 49b2520a82614bedc7bcc077604e0b89885119c2


---
# <a name="best-practices-for-client-deployment-in-system-center-configuration-manager"></a>Procedure consigliate per la distribuzione di client in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Per la distribuzione client su computer in System Center Configuration Manager usare le seguenti procedure consigliate.  

## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>Utilizzare l'installazione client basata su aggiornamento software per i computer Active Directory  
 Questo metodo di distribuzione client ha il vantaggio di usare tecnologie Windows esistenti, si integra con l'infrastruttura di Active Directory, richiede la minima configurazione in Configuration Manager, è il più semplice da configurare per i firewall ed è il più sicuro. L'uso di gruppi di protezione e di filtri WMI per la configurazione dei criteri di gruppo consente di controllare in modo flessibile su quali computer installare il client di Configuration Manager.  

 Per altre informazioni, vedere [How to Install Configuration Manager Clients by Using Software Update-Based Installation](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>Estendere lo schema di Active Directory e pubblicare il sito in modo che sia possibile eseguire CCMSetup senza opzioni di riga di comando  
 Quando si estende lo schema di Active Directory per Configuration Manager e il sito viene pubblicato su Servizi di dominio Active Directory, molte proprietà di installazione client vengono pubblicate in Servizi di dominio Active Directory. Se un computer è in grado di rilevare le proprietà di installazione del client, può usarle durante la distribuzione del client di Configuration Manager. Poiché queste informazioni vengono generate automaticamente, viene eliminato il rischio di errori umani associato all'immissione manuale delle proprietà di installazione.  

 Per altre informazioni, vedere [Informazioni sulle proprietà di installazione client pubblicate in Servizi di dominio Active Directory in System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

## <a name="when-you-have-many-clients-to-deploy-plan-a-phased-rollout-outside-business-hours"></a>Se si dispone di molti client da distribuire, pianificare un'implementazione graduale fuori dall'orario di ufficio  
 Per ridurre al minimo l'impatto dei requisiti di elaborazione della CPU sul server del sito, pianificare un'implementazione graduale dei client per un periodo di tempo. Distribuire i client fuori dall'orario di ufficio in modo da garantire una maggiore larghezza di banda per i servizi aziendali critici durante il giorno ed evitare che i computer siano rallentati o che sia necessario un riavvio per completare l'installazione.  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>Attivare l'aggiornamento automatico al termine della distribuzione del client principale  
 Gli aggiornamenti client automatici sono utili quando si desidera aggiornare un numero ridotto di computer client che potrebbero essere stati esclusi dal metodo di installazione client principale. Ad esempio, è stato completato un aggiornamento client iniziale, ma alcuni client erano offline durante la distribuzione dell'aggiornamento. È possibile quindi usare questo metodo per aggiornare il client su questi computer alla successiva attivazione.  

> [!NOTE]  
>  Grazie alle prestazioni migliorate di Configuration Manager, è possibile usare gli aggiornamenti automatici come metodo principale di aggiornamento dei client. Tuttavia, le prestazioni variano in base all'infrastruttura della gerarchia, come ad esempio il numero di client.  

 Per altre informazioni sul metodo di aggiornamento automatico dei client, vedere [Come aggiornare i client per i computer Windows in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>Se si installa il client con proprietà client.msi utilizzare SMSMP e FSP  
 La proprietà SMSMP specifica il punto di gestione iniziale per la comunicazione del client ed elimina la dipendenza da soluzioni di posizionamento dei servizi come Servizi di dominio Active Directory, DNS e WINS.  

 Utilizzare la proprietà FSP e installare un punto di stato di fallback in modo da poter controllare l'installazione e l'assegnazione di client e identificare eventuali problemi di comunicazione.  

 Per altre informazioni su queste opzioni, vedere [Informazioni sulle proprietà di installazione del client in System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

## <a name="if-you-want-to-use-client-languages-other-than-english-install-the-client-language-packs-before-you-install-the-clients"></a>Se si desidera utilizzare delle lingue client diverse dall'inglese, installare i Language Pack client prima di installare i client  
 Se si installano i Language Pack client su un sito dopo aver installato i client, è necessario reinstallare i client per consentire l'utilizzo delle lingue aggiuntive. Per i client di dispositivi mobili, è necessario cancellare il dispositivo e registrarlo nuovamente.  

 Per altre informazioni su come aggiungere il supporto di altre lingue client, vedere [Language Pack in System Center Configuration Manager](../../../../core/servers/deploy/install/language-packs.md).  

## <a name="plan-and-prepare-any-required-pki-certificates-in-advance"></a>Pianificare e preparare in anticipo i certificati PKI richiesti  
 Per gestire dei dispositivi su Internet, dispositivi mobili registrati e computer Mac è necessario disporre di certificati PKI sui sistemi del sito (punti di gestione e punti di distribuzione) e sui dispositivi client. Per molti clienti sono necessarie una pianificazione e una preparazione avanzate, soprattutto se si dispone di un team separato che gestisce l'infrastruttura PKI. Sulle reti di produzione potrebbe essere richiesta l'approvazione della gestione delle modifiche per utilizzare i nuovi certificati, il riavvio dei server di sistema del sito oppure la disconnessione e l'accesso per una nuova appartenenza al gruppo. Inoltre, potrebbe essere necessario attendere un tempo sufficiente per la replica delle autorizzazioni di protezione e per i nuovi modelli di certificato.  

 Per altre informazioni sui certificati PKI richiesti, vedere [PKI certificate requirements for System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md) (Requisiti dei certificati PKI per System Center Configuration Manager).  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>Prima di installare i client, configurare le impostazioni client richieste e le finestre di manutenzione  
 Sebbene sia possibile configurare le impostazioni client e le finestre di manutenzione prima o dopo aver installato i client, configurare tutte le impostazioni richieste prima di installare i client in modo che le impostazioni vengano usate al momento dell'installazione. Per altre informazioni, vedere [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md)  

 Configurare le finestre di manutenzione per i server e per i dispositivi con Windows Embedded per garantire la continuità aziendale per questi computer, spesso di rilevanza critica per l'azienda. Ad esempio, le finestre di manutenzione garantiscono che gli aggiornamenti software richiesti e il software antimalware non determinino il riavvio del computer durante l'orario di lavoro.  

> [!IMPORTANT]  
>  Per i computer Windows 10 che si prevede di proteggere con il Filtro di scrittura unificato (UWF), è necessario configurare il dispositivo per UWF prima di installare il client. In questo modo Configuration Manager installa il client con un provider di credenziali personalizzato che blocca l'accesso degli utenti con diritti limitati al dispositivo in modalità di manutenzione.  

## <a name="for-mac-computers-and-mobile-devices-that-are-enrolled-by-configuration-manager-plan-your-user-enrollment-experience"></a>Per i computer Mac e i dispositivi mobili che vengono registrati da Configuration Manager, pianificare l'esperienza di registrazione utente  
 Se gli utenti registrano il computer Mac e i dispositivi mobili tramite Configuration Manager, pianificare e preparare l'esperienza utente. Ad esempio, è possibile eseguire lo script dell'installazione e del processo di registrazione utilizzando una pagina Web in modo che gli utenti possano inserire una minima quantità di informazioni richieste e ricevano le istruzioni con un collegamento tramite posta elettronica.  

## <a name="when-you-manage-windows-embedded-devices-use-file-based-write-filters-fbwf-rather-than-enhanced-write-filters-ewf-for-higher-scalability"></a>Quando si gestiscono i dispositivi con Windows Embedded, usare i filtri di scrittura basati su file (FBWF) piuttosto che i filtri di scrittura avanzati (EWF) per una maggiore scalabilità  
 I dispositivi incorporati che utilizzano i filtri di scrittura avanzati (EWF) sono soggetti alle risincronizzazioni dei messaggi di stato. Se si dispone solo di pochi dispositivi incorporati che utilizzano filtri di scrittura avanzati, tale evento potrebbe passare inosservato. Tuttavia, in caso di risincronizzazione delle informazioni di numerosi dispositivi integrati, come l'invio dell'inventario completo piuttosto che l'inventario differenziale, potrebbe verificarsi un significativo aumento dei pacchetti di rete e un maggiore carico di elaborazione della CPU sul server del sito.  

 Se è possibile scegliere il tipo di filtro di scrittura da abilitare, scegliere i filtri di scrittura basati su file. Configurare quindi le eccezioni per il mantenimento dello stato del client e dei dati di inventario tra riavvii dei dispositivi per la massima efficienza della rete e della CPU nel client di Configuration Manager. Per altre informazioni sui filtri di scrittura, vedere   [Planning for client deployment to Windows Embedded devices in System Center Configuration Manager](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

 Per altre informazioni sul numero massimo di client con Windows Embedded supportati da un sito primario, vedere [Supported operating sysetms for clients and devices](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) (Sistemi operativi supportati per client e dispositivi).  



<!--HONumber=Dec16_HO3-->


