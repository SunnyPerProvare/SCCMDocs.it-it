---
title: Endpoint Protection | System Center Configuration Manager
description: Informazioni su come gestire i criteri antimalware e la sicurezza di Windows Firewall per i computer client nella gerarchia di Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
caps.latest.revision: 11
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: 30ac6f2ec03a4c0d50de700f9ce77f9e50eaf1e0


---
# <a name="endpoint-protection-in-system-center-configuration-manager"></a>Endpoint Protection in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Endpoint Protection in System Center Configuration Manager consente di gestire i criteri antimalware e la sicurezza di Windows Firewall per i computer client nella gerarchia di Configuration Manager.  

> [!IMPORTANT]  
>  Per gestire i client nella gerarchia di Configuration Manager è necessario avere la licenza per l'uso di Endpoint Protection.  

 L'uso di Endpoint Protection con Configuration Manager offre i vantaggi seguenti:  

-   Configurare criteri antimalware e impostazioni di Windows Firewall e gestire Windows Defender Advanced Threat Protection per gruppi di computer selezionati  

-   Usare gli aggiornamenti software di Configuration Manager per scaricare i file definizioni antimalware più recenti e mantenere aggiornati i computer client  

-   Inviare notifiche di posta elettronica, usare il monitoraggio integrato nella console e visualizzare report per mantenere gli utenti amministratori informati quando viene rilevato malware nei computer client  

I computer Windows 10 non richiedono client aggiuntivi per la gestione di Endpoint Protection. In computer con Windows 8.1 e versioni precedenti, viene installato il client di Endpoint Protection oltre al client di Configuration Manager. Endpoint Protection può gestire. Il client di Endpoint Protection ha le funzionalità seguenti:  

-   Rilevamento e correzione di spyware e malware  

-   Rilevamento e correzione di rootkit  

-   Valutazione delle vulnerabilità critiche e aggiornamenti automatici del motore e delle definizioni  

-   Rilevamento delle vulnerabilità di rete con Network Inspection System  

-   Integrazione con Cloud Protection Service per segnalare malware a Microsoft. Se si partecipa a questo servizio, il client di Endpoint Protection o Windows Defender può scaricare le definizioni più recenti da Malware Protection Center quando in un computer viene rilevato malware non identificato.  

> [!NOTE]  
>  Il client di Endpoint Protection può essere installato in un server che esegue Hyper-V e nelle macchine virtuali guest con sistemi operativi supportati. Per evitare un uso eccessivo della CPU, le azioni di Endpoint Protection hanno un ritardo casuale predefinito che impedisce l'esecuzione contemporanea dei servizi.  

 Endpoint Protection in Configuration Manager consente anche di gestire le impostazioni di Windows Firewall nella console di Configuration Manager.  

 [Example scenario: Using System Center Endpoint Protection to protect computers from malware in System Center Configuration Manager](scenarios-endpoint-protection.md) (Scenario di esempio: uso di Endpoint Protection in System Center per proteggere i computer da malware in System Center Configuration Manager) Endpoint Protection e Windows Firewall.  


## <a name="managing-malware-with-endpoint-protection"></a>Gestione del malware con Endpoint Protection  
 Endpoint Protection in Configuration Manager consente di creare criteri antimalware che contengono impostazioni per le configurazioni del client di Endpoint Protection. È quindi possibile distribuire tali criteri antimalware nei computer client e monitorarli nel nodo **Stato di Endpoint Protection ** dell'area di lavoro **Monitoraggio** oppure usando i report di Configuration Manager.  

 Altre informazioni:  

-   [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md) (Creare e distribuire criteri antimalware per Endpoint Protection in System Center Configuration Manager): creare, distribuire e monitorare criteri antimalware con un elenco di impostazioni da configurare  

-   [How to monitor Endpoint Protection in System Center Configuration Manager](monitor-endpoint-protection.md) (Monitorare Endpoint Protection in System Center Configuration Manager): monitoraggio dei report sull'attività, dei computer client infetti e altro.  

-   [How to manage antimalware policies and firewall settings for Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-firewall.md) (Come gestire i criteri antimalware e le impostazioni del firewall per Endpoint Protection in System Center Configuration Manager)  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>Gestione di Windows Firewall con Endpoint Protection  
 Endpoint Protection in Configuration Manager offre funzionalità di gestione di base per Windows Firewall nei computer client. Per ogni profilo di rete è possibile configurare le impostazioni seguenti:  

-   Abilitare o disabilitare Windows Firewall.  

-   Bloccare le connessioni in ingresso, comprese quelle nell'elenco dei programmi consentiti.  

-   Notificare all'utente quando Windows Firewall blocca un nuovo programma.  

> [!NOTE]  
>  Endpoint Protection supporta solo la gestione di Windows Firewall.  


 Per altre informazioni su come creare e distribuire i criteri di Windows Firewall per Endpoint Protection, vedere [Come creare e distribuire criteri di Windows Firewall per Endpoint Protection in System Center Configuration Manager](create-windows-firewall-policies.md).  


## <a name="windows-defender-advanced-threat-protection"></a>Windows Defender Advanced Threat Protection

A partire dalla versione 1606 di Configuration Manager (Current Branch), Endpoint Protection consente di gestire e monitorare Windows Defender Advanced Threat Protection (ATP). Windows Defender ATP è un nuovo servizio che consente alle aziende di rilevare, analizzare e rispondere agli attacchi avanzati sulle reti. Vedere [Windows Defender Advanced Threat Protection](windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Flusso di lavoro di Endpoint Protection  
 Vedere il diagramma seguente per capire il flusso di lavoro per l'implementazione di Endpoint Protection nella gerarchia di Configuration Manager.  

 ![Flusso di lavoro di Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)  

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Client di Endpoint Protection per computer Mac e server Linux  
 System Center Endpoint Protection include un client di Endpoint Protection per Linux e per i computer Mac. Questi client non vengono installati con Configuration Manager. È necessario invece scaricare i prodotti seguenti da [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

-   System Center 2012 Endpoint Protection per Mac  

-   System Center 2012 Endpoint Protection per Linux  


> [!IMPORTANT]  
>  Per scaricare i file di installazione di Endpoint Protection per Linux e Mac occorre essere titolari di un contratto multilicenza Microsoft.  

 Questi prodotti non possono essere gestiti dalla console di Configuration Manager. Con i file di installazione, tuttavia, viene fornito un Management Pack di System Center Operations Manager, che consente di gestire il client per Linux usando Operations Manager.  

 Per altre informazioni su come installare e gestire i client di Endpoint Protection per i computer Mac e Linux, usare la documentazione di accompagnamento di questi prodotti, disponibile nella cartella **Documentazione** .



<!--HONumber=Nov16_HO1-->

