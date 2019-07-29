---
title: Nozioni fondamentali sulla gestione dei dispositivi
titleSuffix: Configuration Manager
description: Informazioni su come usare System Center Configuration Manager per gestire i dispositivi.
ms.date: 12/04/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ac213abcfa94b8c0ac842b34b6c6e42c89eb74ca
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68340192"
---
# <a name="fundamentals-of-managing-devices-with-system-center-configuration-manager"></a>Nozioni fondamentali sulla gestione dei dispositivi con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager è in grado di gestire due ampie categorie di dispositivi:

- I *client* sono i dispositivi, ad esempio workstation, portatili, server e dispositivi mobili, in cui viene installato il software client di Configuration Manager. Questo software client è necessario per alcune funzioni di gestione, come l'inventario hardware.  

- I *dispositivi gestiti* possono includere i *client*, ma in genere si tratta di dispositivi mobili in cui non è installato il software client di Configuration Manager. Per gestire questo tipo di dispositivi è possibile usare Intune oppure la gestione locale dei dispositivi mobili predefinita in Configuration Manager.

È anche possibile raggruppare e identificare i dispositivi in base all'utente e non solo in base al tipo di client.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Gestione di dispositivi con il client di Configuration Manager

Esistono due modi per usare il software client di Configuration Manager per la gestione di un dispositivo. Il primo consiste nell'individuare il dispositivo nella rete e distribuire il software client in quel dispositivo. Il secondo modo prevede l'installazione manuale del software client in un nuovo computer e l'aggiunta del computer al sito quando viene aggiunto alla rete. Per individuare i dispositivi in cui non è installato il software client, eseguire uno o più metodi di individuazione predefiniti. Dopo aver individuato un dispositivo, usare uno dei vari metodi disponibili per installare il software client. Per informazioni sull'uso dell'individuazione, vedere [Eseguire l'individuazione per System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

Dopo aver individuato i dispositivi supportati per l'esecuzione del software client di Configuration Manager, è possibile usare uno dei diversi metodi per installare il software. Dopo l'installazione del software e l'assegnazione del client a un sito primario, è possibile iniziare a gestire il dispositivo.  I metodi di installazione comuni sono i seguenti:

- Installazione push client.

- Installazione basata sull'aggiornamento software.

- Criteri di gruppo.

- Installazione manuale in un computer.
- Aggiunta del client come parte di un'immagine del sistema operativo da distribuire.  


Dopo l'installazione del client, è possibile semplificare le attività di gestione dei dispositivi tramite raccolte. Le raccolte sono gruppi di dispositivi o utenti creati per poterli gestire come gruppo. Potrebbe essere necessario ad esempio installare un'applicazione per dispositivi mobili in tutti i dispositivi mobili registrati da Configuration Manager. In questo caso è possibile usare la raccolta Tutti i dispositivi mobili.  

Per altre informazioni, vedere questi argomenti:  

- [Choose a device management solution for System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md) (Scegliere una soluzione di gestione dei dispositivi per System Center Configuration Manager)  

- [Metodi di installazione client in System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md)  

- [Introduzione alle raccolte in System Center Configuration Manager](../../core/clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Impostazioni client  
Quando si installa Configuration Manager per la prima volta, tutti i client nella gerarchia vengono configurati usando le impostazioni client predefinite che è tuttavia possibile modificare. Le impostazioni client includono le opzioni di configurazione seguenti:

- Frequenza con cui i dispositivi comunicano con il sito.

- Possibilità di impostare il client per gli aggiornamenti software e altre operazioni di gestione.

- Possibilità per gli utenti di registrare i propri dispositivi mobili in modo che siano gestiti da Configuration Manager.  

È possibile creare impostazioni client personalizzate e quindi assegnarle alle raccolte.  I membri della raccolta sono configurati in modo da avere impostazioni personalizzate ed è possibile creare più impostazioni client personalizzate che vengono applicate in base all'ordine numerico specificato.  Se ci sono impostazioni in conflitto, l'impostazione con il numero d'ordine più basso sostituisce le altre impostazioni.  

Il diagramma seguente illustra un esempio di come creare e applicare le impostazioni client personalizzate.  

![Impostazioni client](media/ClientSettings.gif)  

Per altre informazioni sulle impostazioni client, vedere [Come configurare le impostazioni client in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) e [Informazioni sulle impostazioni client in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).

## <a name="managing-devices-without-the-configuration-manager-client"></a>Gestione di dispositivi senza il client di Configuration Manager  
Configuration Manager supporta la gestione di alcuni dispositivi in cui non è installato il software client e che non sono gestiti da Intune. Per altre informazioni, vedere [Gestire i dispositivi mobili con l'infrastruttura locale in System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) e [Gestire i dispositivi mobili con System Center Configuration Manager ed Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-based-management"></a>Gestione basata sugli utenti  
Configuration Manager supporta le raccolte di utenti di Active Directory Domain Services. Quando si usa una raccolta utenti, è possibile installare il software in tutti i computer usati dai membri della raccolta. Per assicurarsi che il software distribuito venga installato solo nei dispositivi specificati come dispositivi primari dell'utente, impostare l'affinità utente-dispositivo. Un utente può disporre di uno o più dispositivi primari.  

Uno dei modi in cui gli utenti possono controllare l'esperienza di distribuzione del software consiste nell'usare l'interfaccia client **Software Center**. **Software Center** viene automaticamente installato nei computer client e viene eseguito dal menu **Start**. **Software Center** consente agli utenti di gestire il software e di eseguire le attività seguenti:  

- Installare software.  

- Pianificare l'installazione automatica del software in ore non lavorative.  

- Specificare quando Configuration Manager può installare il software in un dispositivo.  

- Configurare le impostazioni di accesso per il controllo remoto, se il controllo remoto è impostato in Configuration Manager.  

- Configurare le opzioni per il risparmio di energia, se è stato impostato da un amministratore.  


Un collegamento in **Software Center** consente agli utenti di connettersi al **Catalogo applicazioni**, in cui possono cercare, installare e richiedere software. Il **Catalogo applicazioni** viene anche usato per configurare le impostazioni delle preferenze, cancellare i dispositivi mobili e, se è impostato, specificare un dispositivo primario per l'affinità utente-dispositivo.   

Gli utenti possono accedere al **Catalogo applicazioni** anche tramite una sessione Intranet o Internet.  
