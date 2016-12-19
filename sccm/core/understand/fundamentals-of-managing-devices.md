---
title: Nozioni fondamentali sulla gestione dei dispositivi | Documentazione Microsoft
description: Informazioni su come usare System Center Configuration Manager per gestire i dispositivi.
ms.custom: na
ms.date: 12/04/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
caps.latest.revision: 6
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 17b36eae97272c408fce20e1f88812dafc984773
ms.openlocfilehash: b907975db5b5ffa6fefef58902319b987e57dca6


---
# <a name="fundamentals-of-managing-devices-with-system-center-configuration-manager"></a>Nozioni fondamentali sulla gestione dei dispositivi con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager è in grado di gestire due ampie categorie di dispositivi:

I **client**, ovvero dispositivi come workstation, portatili, server e dispositivi mobili in cui viene installato il software client di Configuration Manager. Questo software client è necessario per alcune funzioni di gestione, come l'inventario hardware.  

I **dispositivi gestiti**, che possono includere *client*, ma in genere sono costituiti da dispositivi mobili in cui non è installato il software client di Configuration Manager e che vengono gestiti con Microsoft Intune o con lo strumento di gestione di dispositivi mobili locale incluso in Configuration Manager.

È anche possibile raggruppare e identificare i dispositivi in base all'utente, e non solo al tipo di client.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Gestione di dispositivi con il client di Configuration Manager

Per gestire un dispositivo usando il software client di Configuration Manager, è necessario individuare il dispositivo nella rete e quindi distribuire il software client nel dispositivo oppure installare manualmente il software client in un nuovo computer e quindi fare in modo che il computer venga aggiunto al sito quando viene aggiunto alla rete. Per individuare i dispositivi in cui non è ancora installato il software client, eseguire uno o più dei metodi di individuazione predefiniti. Dopo aver individuato un dispositivo, usare uno dei vari metodi disponibili per installare il software client. Per informazioni sull'uso dell'individuazione, vedere [Eseguire l'individuazione per System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

 Dopo l'individuazione dei dispositivi supportati per l'esecuzione del software client di Configuration Manager, è possibile usare uno dei diversi metodi per installare il software. Dopo l'installazione del software e l'assegnazione del client a un sito primario, è possibile iniziare a gestire il dispositivo.  Tra i metodi di installazione più comuni ci sono l'installazione push client, l'installazione basata su aggiornamenti software, l'uso di Criteri di gruppo, l'installazione manuale in un computer o l'inserimento del client come parte di un'immagine del sistema operativo distribuita.  

 Dopo l'installazione del client, è possibile semplificare le attività di gestione dei dispositivi tramite raccolte. Le raccolte sono gruppi di dispositivi o utenti creati per poterli gestire come gruppo. Potrebbe essere necessario, ad esempio, installare un'applicazione in tutti i dispositivi mobili registrati da Configuration Manager. In questo caso, è possibile usare la raccolta **Tutti i dispositivi mobili**.  

 Per altre informazioni, vedere questi argomenti:  

-   [Choose a device management solution for System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md) (Scegliere una soluzione di gestione dei dispositivi per System Center Configuration Manager)  

-   [Metodi di installazione client in System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md)  

-   [Introduzione alle raccolte in System Center Configuration Manager](../../core/clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Impostazioni client  
 Quando si installa per la prima volta Configuration Manager, tutti i client nella gerarchia vengono configurati usando le impostazioni client predefinite che è possibile modificare. Queste impostazioni client includono opzioni di configurazione, ad esempio la frequenza con cui i dispositivi comunicano con il sito, se il client è abilitato per gli aggiornamenti software e altre operazioni di gestione oppure se gli utenti possono registrare i dispositivi mobili in modo che vengano gestiti da Configuration Manager.  

È possibile creare impostazioni client personalizzate e quindi assegnarle alle raccolte.  I membri della raccolta vengono configurati con le impostazioni personalizzate ed è possibile creare più impostazioni client personalizzate che vengono applicate nell'ordine specificato (in base a un ordine numerico).  Se ci sono impostazioni in conflitto, l'impostazione con il numero d'ordine più basso sostituisce le altre impostazioni.  

Il diagramma seguente mostra un esempio di come sia possibile creare e applicare le impostazioni client personalizzate.  

 ![Impostazioni client](media/ClientSettings.gif)  

 Per altre informazioni sulle impostazioni client, vedere  
                [Come configurare le impostazioni client in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) e [Informazioni sulle impostazioni client in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).

## <a name="managing-devices-without-the-configuration-manager-client"></a>Gestione di dispositivi senza il client di Configuration Manager  
 Configuration Manager supporta la gestione di alcuni dispositivi in cui non è installato il software client e che non sono gestiti da Microsoft Intune. Per altre informazioni, vedere [Gestire i dispositivi mobili con l'infrastruttura locale in System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) e [Gestire i dispositivi mobili con System Center Configuration Manager ed Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-based-management"></a>Gestione basata sugli utenti  
 Raccolte di Configuration Manager di utenti di Servizi di dominio Active Directory. Quando si usa una raccolta di utenti, è possibile installare il software in tutti i computer a cui accedono i membri della raccolta e configurare l'**affinità utente-dispositivo** in modo che il software distribuito venga installato solo nei dispositivi specificati come dispositivo primario dell'utente. Un utente può disporre di uno o più dispositivi primari.  

 Uno dei modi in cui gli utenti possono controllare l'esperienza di distribuzione software consiste nell'usare l'interfaccia client computer, ovvero **Software Center**. Software Center viene automaticamente installato nei computer client ed è accessibile dal menu Start degli utenti. Software Center consente agli utenti di gestire il software e di eseguire le operazioni seguenti:  

-   Installare il software  

-   Pianificare l'installazione del software in orari non lavorativi  

-   Specificare quando Configuration Manager è in grado di installare il software nel dispositivo  

-   Configurare le impostazioni di accesso per il controllo remoto, se il controllo remoto è abilitato in Configuration Manager  

-   Configurare le opzioni per il risparmio energetico se un utente amministratore lo ha abilitato  

 Un collegamento in Software Center consente agli utenti di connettersi al **Catalogo applicazioni**, in cui possono esplorare, installare e richiedere software. Il Catalogo Applicazioni consente inoltre agli utenti di configurare alcune impostazioni preferenziali, cancellare i dati dai dispositivi mobili e, quando questa configurazione è consentita, specificare i propri dispositivi primari per l'affinità utente-dispositivo.   

 Poiché il Catalogo applicazioni è un sito Web ospitato in IIS, gli utenti possono accedere al Catalogo applicazioni anche direttamente da un browser, dalla Intranet o da Internet.  



<!--HONumber=Dec16_HO3-->


