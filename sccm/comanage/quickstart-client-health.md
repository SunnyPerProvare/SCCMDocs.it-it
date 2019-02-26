---
title: Stato del client con CO-gestione
titleSuffix: Configuration Manager
description: Mantenere la visibilità dell'integrità del client di Configuration Manager da Intune nel portale di Azure
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5b243aac-8a1a-4f14-ba3f-5446bb483e92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6838371a80530d5ab66abd9d8a976af41513e15
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755322"
---
# <a name="client-health-with-co-management"></a>Stato del client con CO-gestione

L'integrità della rete è connessa direttamente per l'integrità dei dispositivi da e verso il. Intune può comunicare con un client non integro, anche quando non è nella rete. Usare CO-gestione per combinare questa funzionalità con capacità di Configuration Manager segnalati al 98% di client integro noto. È quindi possibile rilevare, valutare e ottenere visibilità in tutti i client in tempo reale. Intune aggiunge anche il supporto necessari per gli aggiornamenti di conformità in tutti i client connessi.

Nel video seguente, senior program manager Rob York e product marketing manager Locky Ainley discutere e lo stato del client con CO-gestione della demo:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Client-Health-Monitoring-with-Co-Management/player]



## <a name="benefits"></a>Vantaggi

Valutazione dell'integrità del client è una priorità superiore. System Center 2012 Configuration Manager aggiunte **CCMeval**. Questa utilità è esterna al client di Configuration Manager. Client fornisce monitoraggio e aggiornamento automatico e il monitoraggio dell'integrità. Tuttavia, questo tipo di report è basato su un dispositivo viene fisicamente o virtualmente nella rete interna. CO-gestione consente di risolvere il problema.

Con CO-gestione, Intune può inviare report sullo stato di integrità client. Fornisce informazioni relative al timestamp per la validità dei dati. Queste informazioni indicano se i dispositivi sono integri, in grado di connettersi, in grado di installare le app, oppure è possono aggiornare il sistema operativo richiesto le compilazioni. 

Per una panoramica dettagliata di questa funzionalità, vedere questo video dal [What ' s New in Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/64591) sessione presso Ignite 2018.

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


Quando Configuration Manager offre stato del dispositivo che viene installato il client, ma non lo è, Intune può fornire informazioni più senza la necessità di connettersi al client. Le informazioni sull'integrità del dispositivo in Intune è facile da comprendere. Se lo stato è diverso da **integro**, offre consigli e passaggi successivi per risolvere i problemi e correggerla.

> [!Note]  
> Per una versione futura sono previsti i seguenti vantaggi:
> - Configuration Manager include funzionalità aggiuntive in CCMeval  
> - Sarà più semplice identificare i computer potenzialmente non integri in Configuration Manager e Intune  
> - È possibile raggruppare i dati di integrità client di Intune  



## <a name="value-proposition"></a>Proposta di valore

Con questa funzionalità, si disporrà di un'origine dati esterna con Intune. Consente di determinare i passaggi successivi durante la risoluzione di una vasta gamma di problemi del client. A questo punto non è necessario creare altri report o usare altri strumenti per estrarre i dati del client.

Dopo aver ai client integri, è stato aggiornato immediatamente la conformità delle patch. Una migliore conformità patch significa una migliore sicurezza.



## <a name="configure"></a>Configurare

Per iniziare a usare questa funzionalità, procedere come segue:

- Aggiornare i dispositivi a Windows 10, versione 1709 o successiva  

- [Abilitare la co-gestione](/sccm/comanage/how-to-enable)  
    - Non è necessario passare qualsiasi carico di lavoro a Intune  

- Aggiornamento di un sito di Configuration Manager e ai client di *versione 1806* o versione successiva  


### <a name="review-configuration-manager-client-health-in-intune"></a>Esaminare lo stato del client Configuration Manager in Intune

1. Accedere al [portale di Azure](https://portal.azure.com/).  

2. Scegli **tutti i servizi** > **Intune**. Intune si trova nel **monitoraggio + gestione** sezione.  

3. Dopo aver aperto la **Microsoft Intune** riquadro, nel menu **Guida e supporto tecnico**, andare al **risoluzione dei problemi** pagina.  

4. Usare la **selezionare l'utente** seleziona l'opzione, trovare il dispositivo specifico nel **dispositivi** elencare e selezionarla per aprire la pagina del dispositivo.  

5. Informazioni sulla CO-gestione viene visualizzati nella parte inferiore della pagina del dispositivo. Queste informazioni includono i campi seguenti per l'integrità del client:  
    - **Stato dell'agente di Configuration Manager**  
    - **Ultimo controllo agente di Configuration Manager nel tempo**  

> [!Tip]  
> I dispositivi registrati in Intune si connettono al servizio cloud di tre volte al giorno, ogni otto ore circa. 
