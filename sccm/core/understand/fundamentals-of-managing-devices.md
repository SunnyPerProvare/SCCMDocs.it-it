---
title: Nozioni fondamentali sulla gestione dei dispositivi | System Center Configuration Manager
description: Informazioni su come usare System Center Configuration Manager per gestire i dispositivi.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
caps.latest.revision: 6
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f4d39f31723711a7f5ec2b1aa39e81d3a3188029


---
# <a name="fundamentals-of-managing-devices-with-system-center-configuration-manager"></a>Nozioni fondamentali sulla gestione dei dispositivi con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager è in grado di gestire due ampie categorie di dispositivi.

La prima è costituita dai **client**, ovvero dispositivi come workstation, portatili, server e dispositivi mobili in cui è installato il software client di Configuration Manager che ne consente la gestione.   

La seconda è costituita dai **dispositivi gestiti**, che possono includere client, ma in genere sono costituiti da dispositivi mobili in cui non è installato il software client di Configuration Manager e che vengono gestiti con Microsoft Intune o con lo strumento di gestione di dispositivi mobili locale integrato in Configuration Manager.

Oltre a gestire i dispositivi con o senza il client di Configuration Manager, è possibile usare la gestione incentrata sull'utente per supportare il gruppo e identificare i dispositivi gestiti.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Gestione di dispositivi con il client di Configuration Manager

 La gestione dei client include operazioni come la raccolta dell'inventario di hardware o software dai dispositivi, l'installazione di nuovo software in un dispositivo o la definizione di impostazioni per l'applicazione della conformità a una configurazione specifica o la creazione di report su tale conformità. Alcune funzioni di gestione, come l'inventario hardware, richiedono l'esecuzione del software client di Configuration Manager nel dispositivo. Altre operazioni, come l'installazione (distribuzione) di software in un dispositivo, sono supportate per tutti i dispositivi gestiti.  

 Per gestire un dispositivo usando il software client di Configuration Manager, è necessario individuare il dispositivo nella rete e quindi distribuire (installare) il software client nel dispositivo oppure installare manualmente il software client in un nuovo computer e quindi fare in modo che il computer venga aggiunto al sito quando viene aggiunto alla rete. Per individuare i dispositivi in cui non è ancora installato il software client, eseguire uno o più dei metodi di individuazione predefiniti. Dopo l'individuazione di un dispositivo, è possibile usare uno dei diversi metodi per installare il software client. Per informazioni sull'uso dell'individuazione, vedere [Eseguire l'individuazione per System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

 Dopo l'individuazione dei dispositivi supportati per l'esecuzione del software client di Configuration Manager, è possibile usare uno dei diversi metodi per installare il software. Dopo l'installazione del software e l'assegnazione del client a un sito primario, è possibile iniziare a gestire il dispositivo.  Tra i metodi di installazione più comuni ci sono l'installazione push client, l'installazione basata su aggiornamenti software, l'uso di Criteri di gruppo, l'installazione manuale in un computer o l'inserimento del client come parte di un'immagine del sistema operativo distribuita.  

 Dopo l'installazione del client, è possibile semplificare le attività di gestione dei dispositivi tramite raccolte. Le raccolte sono gruppi logici di dispositivi o utenti creati per eseguire attività di gestione su più dispositivi che condividono un set comune di criteri. Potrebbe essere necessario, ad esempio, installare un'applicazione in tutti i dispositivi mobili registrati da Configuration Manager. In questo caso, è possibile usare la raccolta **Tutti i dispositivi mobili** , che esclude automaticamente i computer. È possibile creare raccolte personalizzate per raggruppare logicamente i dispositivi gestiti, in base alle proprie esigenze.  

 Per altre informazioni, vedere gli argomenti seguenti:  

-   [Scegliere una soluzione di gestione dei dispositivi per System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  

-   [Metodi di installazione client in System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md)  

-   [Introduzione alle raccolte in System Center Configuration Manager](../../core/clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Impostazioni client  
 Quando si installa per la prima volta Configuration Manager, tutti i client nella gerarchia vengono configurati usando le impostazioni client predefinite che è possibile modificare. Queste impostazioni client includono opzioni di configurazione, ad esempio la frequenza con cui i dispositivi comunicano con il sito, se il client è abilitato per gli aggiornamenti software e altre operazioni di gestione oppure se gli utenti possono registrare i dispositivi mobili in modo che vengano gestiti da Configuration Manager.  

 Se sono necessarie impostazioni client diverse per i gruppi di utenti o dispositivi, è possibile creare impostazioni client personalizzate e quindi assegnarle alle raccolte.  I membri della raccolta vengono configurati con le impostazioni personalizzate ed è possibile creare più impostazioni client personalizzate che vengono applicate nell'ordine specificato (in base a un ordine numerico).  Se ci sono impostazioni in conflitto, l'impostazione con il numero d'ordine più basso sostituisce le altre impostazioni.  

 Il diagramma seguente mostra un esempio di come sia possibile creare e applicare le impostazioni client personalizzate.  

 ![Impostazioni client](media/ClientSettings.gif)  

 Per altre informazioni sulle impostazioni client, vedere  
                [Come configurare le impostazioni client in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) e [Informazioni sulle impostazioni client in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).

## <a name="managing-devices-without-the-configuration-manager-client"></a>Gestione di dispositivi senza il client di Configuration Manager  
 Configuration Manager supporta la gestione di alcuni dispositivi in cui non è installato il software client e che non sono gestiti tramite interoperabilità con Microsoft Intune. Per altre informazioni, vedere [Gestire i dispositivi mobili con l'infrastruttura locale in System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) e [Gestire i dispositivi mobili con System Center Configuration Manager ed Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-centric-management"></a>Gestione incentrata sull'utente  
 Oltre alle raccolte per i dispositivi, esistono anche raccolte contenenti utenti di Servizi di dominio Active Directory. Quando si usa una raccolta di utenti, è possibile installare il software in tutti i computer membri della raccolta a cui l'utente accede e configurare **l'affinità utente-dispositivo** in modo che il software distribuito venga installato solo nei dispositivi specificati come dispositivo primario dell'utente. Questi dispositivi principali vengono chiamati dispositivi primari. Un utente può disporre di uno o più dispositivi primari.  

 Uno dei modi in cui gli utenti possono controllare l'esperienza di distribuzione software consiste nell'usare l'interfaccia client computer, ovvero **Software Center**. Software Center viene automaticamente installato nei computer client ed è accessibile dal menu Start degli utenti. Software Center consente agli utenti di gestire il software e di eseguire le operazioni seguenti:  

-   Installare il software  

-   Pianificare l'installazione del software in orari non lavorativi  

-   Specificare quando Configuration Manager è in grado di installare il software nel dispositivo  

-   Configurare le impostazioni di accesso per il controllo remoto, se il controllo remoto è abilitato in Configuration Manager  

-   Configurare le opzioni per il risparmio energetico se un utente amministratore lo ha abilitato  

 Un collegamento in Software Center consente agli utenti di connettersi al **Catalogo applicazioni**, in cui possono esplorare, installare e richiedere software. Il Catalogo Applicazioni consente inoltre agli utenti di configurare alcune impostazioni preferenziali, cancellare i dati dai dispositivi mobili e, quando questa configurazione è consentita, specificare i propri dispositivi primari per l'affinità utente-dispositivo. Gli altri metodi di configurazione delle informazioni di affinità utente-dispositivo includono l'importazione delle informazioni da un file e la generazione automatica dai dati di utilizzo.  

 Poiché il Catalogo applicazioni è un sito Web ospitato in IIS, gli utenti possono accedere al Catalogo applicazioni anche direttamente da un browser, dalla Intranet o da Internet.  



<!--HONumber=Nov16_HO1-->


