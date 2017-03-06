---
title: Metodi di installazione client | Microsoft Docs
description: Informazioni sui metodi di installazione client per System Center Configuration Manager.
ms.custom: na
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
caps.latest.revision: 9
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 593fbd0587d54490246f48ae54f666bac6b7830d
ms.openlocfilehash: a7d5a04cf34c49246f768f9a4757c5da3b4db31a
ms.lasthandoff: 12/16/2016


---
# <a name="client-installation-methods-in-system-center-configuration-manager"></a>Metodi di installazione client in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile usare diversi metodi per installare il software client di Configuration Manager (noto anche come ConfigMgr o SCCM). È possibile usare un metodo o una combinazione di metodi. Questo argomento presenta informazioni su ogni metodo e consente quindi di comprendere quale sia più appropriato per l'organizzazione.  

## <a name="client-push-installation"></a>Installazione push client  

 **Piattaforma client supportata:** Windows  

 **Vantaggi**  

-   Può essere utilizzato per installare il client in un singolo computer, una raccolta di computer o nei risultati di una query.  

-   Può essere utilizzato per installare automaticamente il client in tutti i computer individuati.  

-   Utilizza automaticamente le proprietà di installazione del client definite nella scheda **Client** della finestra di dialogo **Proprietà installazione push client** .  

 **Svantaggi**  

-   Può causare traffico di rete elevato quando si esegue il push in raccolte di grandi dimensioni.  

-   Può essere usato solo nei computer individuati da Configuration Manager.  

-   Non può essere utilizzato per installare client in un gruppo di lavoro.  

-   È necessario specificare un account di installazione push client che dispone di diritti amministrativi sul computer client previsto.  

-   È necessario che Windows Firewall sia configurato nei computer client con le eccezioni, in modo che l'installazione push client possa essere completata.  

-   Non è possibile annullare l'installazione push client. Quando si usa questo metodo di installazione del client per un sito, Configuration Manager tenta di installare il client in tutte le risorse individuate e ritenta l'installazione in caso di errori fino a 7 giorni.  

 Per altre informazioni su questo metodo di installazione, vedere [Come distribuire i client nei computer Windows in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="software-update-point-based-installation"></a>Installazione basata sul punto di aggiornamento software  
 **Piattaforma client supportata:** Windows  

 **Vantaggi:**  

-   Può utilizzare l'infrastruttura di aggiornamenti software esistente per gestire il software client.  

-   Può installare automaticamente il software client nei nuovi computer se le impostazioni di Windows Server Update Services (WSUS) e dei Criteri di gruppo in Servizi di dominio Active Directory sono configuRati correttamente.  

-   Non richiede l'individuazione dei computer prima di poter installare il client.  

-   I computer possono leggere le proprietà di installazione client che sono state pubblicate in Servizi di dominio Active Directory.  

-   Reinstallerà il software client se è stato rimosso.  

-   Non richiede la configurazione e il mantenimento di un account di installazione per il computer client previsto.  

 **Svantaggi:**  

-   Richiede un'infrastruttura per gli aggiornamenti software che sia funzionante come prerequisito.  

-   Deve utilizzare lo stesso server per l'installazione del client e gli aggiornamenti software e il server deve risiedere in un sito principale.  

-   Per installare nuovi client, è necessario configurare un oggetto Criteri di gruppo in Servizi di dominio Active Directory con la porta e il punto di aggiornamento software attivo del software.  

-   Se lo schema di Active Directory non viene esteso per Configuration Manager, è necessario usare le impostazioni di Criteri di gruppo per eseguire il provisioning dei computer con le proprietà di installazione client.  

 Per altre informazioni su questo metodo di installazione, vedere [Come distribuire i client nei computer Windows in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="group-policy-installation"></a>Installazione tramite Criteri di gruppo  
 **Piattaforma client supportata:** Windows  

 **Vantaggi:**  

-   Non richiede l'individuazione dei computer prima di poter installare il client.  

-   Può essere utilizzato per le nuove installazioni di client o per gli aggiornamenti.  

-   I computer possono leggere le proprietà di installazione client che sono state pubblicate in Servizi di dominio Active Directory.  

-   Non richiede la configurazione e il mantenimento di un account di installazione per il computer client previsto.  

 **Svantaggi:**  

-   Può causare traffico di rete elevato se viene installato un numero elevato di client.  

-   Se lo schema di Active Directory non viene esteso per Configuration Manager, è necessario usare le impostazioni di Criteri di gruppo per aggiungere le proprietà di installazione del client ai computer presenti nel sito.  

 Per altre informazioni su questo metodo di installazione, vedere [Come distribuire i client nei computer Windows in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="logon-script-installation"></a>Installazione tramite script di accesso  
 **Piattaforma client supportata:** Windows  

 **Vantaggi:**  

-   Non richiede l'individuazione dei computer prima di poter installare il client.  

-   Supporta l'utilizzo di proprietà della riga di comando per CCMSetup.  

 **Svantaggi:**  

-   Può causare elevato traffico di rete se viene installato un numero di client elevato in un periodo di tempo breve.  

-   Può richiedere molto tempo per l'installazione in tutti i computer client, se gli utenti non accedono spesso alla rete.  

 Per altre informazioni su questo metodo di installazione, vedere [Come distribuire i client nei computer Windows in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="manual-installation"></a>Installazione manuale  
 **Piattaforma client supportata:** Windows, UNIX/Linux, Mac OS X  

 **Vantaggi:**  

-   Non richiede l'individuazione dei computer prima di poter installare il client.  

-   Può essere utile a scopo di test.  

-   Supporta l'utilizzo di proprietà della riga di comando per CCMSetup.  

 **Svantaggi:**  

-   Non prevede automazione, pertanto risulta dispendioso in termini di tempo.  

 Per altre informazioni su come installare manualmente il client in ciascuna piattaforma, vedere gli argomenti seguenti:  

-   [Come distribuire i client nei computer Windows in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

-   [Come distribuire i client nei server UNIX e Linux in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md)  

-   [How to deploy clients to Macs in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md) (Come distribuire i client nei computer Mac in System Center Configuration Manager)  

