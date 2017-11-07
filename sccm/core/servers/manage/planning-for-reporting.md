---
title: Pianificazione per la creazione di report
titleSuffix: Configuration Manager
description: "È importante pianificare la creazione di report in Configuration Manager a partire dalla installazione fino alla sicurezza e alla larghezza di banda di rete."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ff920c84-d5c8-458c-b67f-bc7219b05690
caps.latest.revision: "6"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 9d7c8de64c412b19fff4fa8c4193a020de680407
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="planning-for-reporting-in-system-center-configuration-manager"></a>Pianificazione per la creazione di report in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La creazione di report in System Center Configuration Manager offre un set di strumenti e risorse che consentono di usare le stesse funzionalità avanzate di SQL Server Reporting Services. Usare le sezioni seguenti per la pianificazione della creazione di report in Configuration Manager.  

##  <a name="BKMK_InstallReportingServicesPoint"></a> Determinare il percorso di installazione del punto di Reporting Services  
 Quando si eseguono i report di Configuration Manager in un sito, questi hanno accesso alle informazioni incluse nel database del sito a cui si connettono. Utilizzare le seguenti sezioni per determinare il percorso di installazione del punto di Reporting Services e l'origine dati da utilizzare.  

> [!NOTE]  
>  Per altre informazioni sulla pianificazione dei sistemi del sito in Configuration Manager, vedere [Aggiungere ruoli di sistema del sito](../deploy/configure/add-site-system-roles.md).  

###  <a name="BKMK_SupportedSiteServers"></a> Server di sistema del sito supportati  
 È possibile installare il punto di Reporting Services in un sito di amministrazione centrale e in siti primari, oltre che in più sistemi di sito in un sito e in altri siti presenti nella gerarchia. Il punto di Reporting Services non è supportato nei siti secondari. Il primo punto di Reporting Services in un sito viene configurato come server di report predefinito. Anche se è possibile aggiungere più punti di Reporting Services in un sito, viene usato attivamente il server di report predefinito in ogni sito per i report di Configuration Manager. È possibile installare il punto di Reporting Services nel server del sito o in un sistema del sito remoto. Tuttavia, per motivi di prestazioni è consigliabile utilizzare Reporting Services in un server di sistema del sito remoto.  

###  <a name="BKMK_DataReplication"></a> Considerazioni sulla replica dei dati  
 Configuration Manager classifica i dati che replica come dati globali o come dati del sito. I dati globali si riferiscono a oggetti creati dagli utenti amministratori e che vengono replicati in tutti i siti della gerarchia, mentre i siti secondari ricevono solo un sottoinsieme di dati globali. Esempi di dati globali includono distribuzioni e aggiornamenti software, raccolte e ambiti di protezione amministrazione basata sui ruoli. I dati del sito fanno riferimento a informazioni operative create dai siti primari di Configuration Manager e dai client connessi ai siti primari. I dati del sito vengono replicati nel sito di amministrazione centrale, ma non in altri siti primari. Esempi di dati del sito includono dati dell'inventario hardware, messaggi di stato, avvisi e i risultati delle raccolte basate su query. I dati del sito possono essere visualizzati solo nel sito di amministrazione centrale e nel sito primario da cui provengono i dati.  

 Tenere presenti i seguenti fattori per determinare dove installare i punti di Reporting Services:  

-   Un punto di Reporting Services con il database del sito di amministrazione centrale come origine dati per i report ha accesso a tutti i dati globali e del sito presenti nella gerarchia di Configuration Manager. Se sono necessari report che contengano dati del sito per più siti in una gerarchia, prendere in considerazione l'installazione del punto di Reporting Services in un sistema del sito nel sito di amministrazione centrale e usare il database del sito di amministrazione centrale come origine dati per i report.  

-   Un punto di Reporting Services con il database del sito primario figlio come origine dei dati per i report ha accesso ai dati globali e ai dati del sito solo per il sito primario locale e per qualsiasi sito secondario figlio. I dati di sito per altri siti primari nella gerarchia di Configuration Manager non vengono replicati nel sito primario. Reporting Services non può pertanto accedere a tali dati. Se sono necessari report che contengano dati del sito per un sito primario specifico o per dati globali ma non si vuole che l'utente del report abbia accesso ai dati del sito da altri siti primari, installare un punto di Reporting Services in un sistema del sito nel sito primario e usare il database del sito primario come origine dati per i report.  

###  <a name="BKMK_NetworkBandwidth"></a> Considerazioni sulla larghezza di banda di rete  
 I server del sistema del sito all'interno dello stesso sito comunicano con tutti gli altri utilizzando SMB (Server Message Block), HTTP o HTTPS a seconda della configurazione del sito. Poiché queste comunicazioni non vengono gestite e si possono verificare in qualsiasi momento senza il controllo della larghezza di banda di rete, esaminare la larghezza di banda di rete disponibile prima di installare il ruolo del punto di Reporting Services in un sistema del sito.  

> [!NOTE]  
>  Per altre informazioni sulla pianificazione dei sistemi del sito, vedere [Aggiungere ruoli di sistema del sito](../deploy/configure/add-site-system-roles.md).  

##  <a name="BKMK_RoleBaseAdministration"></a> Pianificazione dell'amministrazione basata su ruoli per i report  
 La sicurezza dei report è simile alla sicurezza di altri oggetti in Configuration Manager, in cui è possibile assegnare autorizzazioni e ruoli di sicurezza agli utenti amministratori. Gli utenti amministratori possono solo eseguire e modificare i report per cui dispongono dei privilegi di protezione appropriati. Per eseguire report nella console di Configuration Manager, è necessario avere il diritto di **Lettura** per l'autorizzazione **Sito** e le autorizzazioni configurate per oggetti specifici.  

 A differenza di altri oggetti in Configuration Manager, i privilegi di sicurezza impostati per gli utenti amministratori nella console di Configuration Manager devono essere tuttavia configurati in Reporting Services. Quando si configurano i privilegi di sicurezza nella console di Configuration Manager, il punto di Reporting Services si connette a Reporting Services e imposta le autorizzazioni appropriate per i report. Ad esempio, il ruolo di sicurezza **Amministratore aggiornamento software** dispone delle autorizzazioni **Esegui report** e **Modifica report** ad esso associati. Gli utenti amministratori a cui viene assegnato solo il ruolo **Amministratore aggiornamento software** possono solo eseguire e modificare i report per gli aggiornamenti software. I report per gli altri oggetti non vengono visualizzati nella console di Configuration Manager. L'eccezione a questo regola è che alcuni report non sono associati a oggetti specifici a protezione diretta di Configuration Manager. Per tali report, l'utente amministratore deve disporre del diritto di **Lettura** per l'autorizzazione **Sito** per eseguire i report e del diritto **Modifica** per l'autorizzazione **Sito** per modificare i report.  

 I report sono completamente abilitati per l'amministrazione basata su ruoli. I dati per tutti i report inclusi in Configuration Manager vengono filtrati in base alle autorizzazioni dell'utente amministratore che esegue il report. Gli utenti amministratori con ruoli specifici possono solo visualizzare le informazioni definite per i loro ruoli.  

 Per altre informazioni sui diritti di sicurezza per la creazione di report, vedere [Configurare la creazione di report](configuring-reporting.md).  

 Per altre informazioni sull'amministrazione basata su ruoli in Configuration Manager, vedere [Configurare l'amministrazione basata su ruoli](../deploy/configure/configure-role-based-administration.md).  

## <a name="next-steps"></a>Passaggi successivi  
 Usare gli argomenti aggiuntivi seguenti per la pianificazione della creazione di report in Configuration Manager:  

-   [Prerequisiti per la creazione di report in System Center Configuration Manager](../../../core/servers/manage/prerequisites-for-reporting.md)  
-   [Procedure consigliate per la creazione di report in System Center Configuration Manager](../../../core/servers/manage/best-practices-for-reporting.md)  
