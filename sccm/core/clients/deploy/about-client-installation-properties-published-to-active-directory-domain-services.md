---
title: "Proprietà di installazione client in Active Directory Domain Services | System Center Configuration Manager"
description: "Usare le proprietà di installazione client pubblicate per Active Directory Domain Services in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 101d7d4d-92db-419d-b2ae-3c1c1dea68e9
caps.latest.revision: 6
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d5cdaa80abca6d003d3e07c2068c12de64ccab67

---
# <a name="about-client-installation-properties-published-to-active-directory-domain-services-in-system-center-configuration-manager"></a>Informazioni sulle proprietà di installazione client pubblicate in Servizi di dominio Active Directory in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Quando si estende lo schema di Active Directory per System Center Configuration Manager e il sito viene pubblicato in Active Directory Domain Services, molte proprietà di installazione client vengono pubblicate in Active Directory Domain Services. Se un computer è in grado di rilevare le proprietà di installazione del client, può usarle durante la distribuzione del client di Configuration Manager.  

 I vantaggi dell'utilizzo di Servizi di dominio Active Directory per pubblicare le proprietà dell'installazione del client includono:  

-   L'installazione client basata sul punto di aggiornamento software e le installazioni client del Criteri di gruppo non richiedono l'esecuzione del provisioning dei parametri di impostazione in ogni computer.  

-   Poiché queste informazioni vengono generate automaticamente, viene eliminato il rischio di errori umani associato all'immissione manuale delle proprietà di installazione.  

> [!NOTE]  
>  Per altre informazioni su come estendere lo schema di Active Directory per Configuration Manager e come pubblicare un sito, vedere [Estensioni dello schema per System Center Configuration Manager](../../plan-design/network/schema-extensions.md).  

 L'installazione client (CCMSetup) utilizza le proprietà di installazione client pubblicate in Servizi di dominio Active Directory solo se non sono specificate altre proprietà utilizzando uno dei seguenti metodi:  

-   Installazione manuale  

-   Provisioning delle proprietà di installazione client utilizzando i Criteri di gruppo  

> [!NOTE]  
>  Le proprietà di installazione client vengono usate per installare il client e possono essere sovrascritte con le nuove impostazioni del sito assegnato, dopo l'installazione del client e l'assegnazione riuscita a un sito di Configuration Manager.  

 Usare le informazioni dettagliate nelle sezioni seguenti per determinare quali metodi di installazione client di Configuration Manager usano Active Directory Domain Services per ottenere le proprietà di installazione client.  

## <a name="client-push-installation"></a>Installazione push client  
 L'installazione push del client non utilizza i Servizi di dominio Active Directory per ottenere le proprietà di installazione.  

 È possibile specificare le proprietà di installazione client.msi nella scheda **Client** della finestra di dialogo **Proprietà installazione push client** . Queste opzioni e impostazioni del sito relative al client vengono archiviate in un file che il client legge durante l'installazione client.  

> [!NOTE]  
>  Non è necessario specificare alcuna proprietà CCMSetup per l'installazione push client né il punto di stato di fallback né la chiave radice attendibile nella scheda **Client** . Queste impostazioni vengono fornite ai client automaticamente al momento dell'installazione tramite installazione push del client.  

 Qualsiasi proprietà client.msi specificata nella scheda **Client** viene pubblicata in Servizi di dominio Active Directory se il sito viene pubblicato in Servizi di dominio Active Directory. Queste impostazioni vengono lette dalle installazioni del client quando CCMSetup viene eseguito senza proprietà di installazione.  

## <a name="software-update-point-based-installation"></a>Installazione basata sul punto di aggiornamento software  
 Il metodo di installazione basata sul punto di aggiornamento software non supporta l'aggiunta di proprietà di installazione nella riga di comando di CCMSetup.  

 Se non è stato eseguito il provisioning delle proprietà della riga di comando nel computer client utilizzando i Criterio di gruppo, CCMSetup cerca le proprietà di installazione nei Servizi di dominio Active Directory.  

## <a name="group-policy-installation"></a>Installazione tramite Criteri di gruppo  
 Il metodo di installazione con Criteri di gruppo non supporta l'aggiunta di proprietà di installazione nella riga di comando di CCMSetup.  

 Se non è stato eseguito il provisioning delle proprietà della riga di comando nel computer client, CCMSetup cerca le proprietà di installazione nei Servizi di dominio Active Directory.  

## <a name="manual-installation"></a>Installazione manuale  
 CCMSetup cerca le proprietà di installazione nei Servizi di dominio Active Directory nelle seguenti circostanze:  

-   Nessuna proprietà della riga di comando viene specificata dopo il comando CCMSetup.exe.  

-   Non è stato eseguito il provisioning del computer con le proprietà di installazione utilizzando i Criteri di gruppo.  

## <a name="logon-script-installation"></a>Installazione tramite script di accesso  
 CCMSetup cerca le proprietà di installazione nei Servizi di dominio Active Directory nelle seguenti circostanze:  

-   Nessuna proprietà della riga di comando viene specificata dopo il comando CCMSetup.exe.  

-   Non è stato eseguito il provisioning del computer con le proprietà di installazione utilizzando i Criteri di gruppo.  

## <a name="software-distribution-installation"></a>Installazione della distribuzione software  
 CCMSetup cerca le proprietà di installazione nei Servizi di dominio Active Directory nelle seguenti circostanze:  

-   Nessuna proprietà della riga di comando viene specificata dopo il comando CCMSetup.exe.  

-   Non è stato eseguito il provisioning del computer con le proprietà di installazione utilizzando i Criteri di gruppo.  

## <a name="installations-for-clients-that-cannot-access-active-directory-domain-services-for-published-information"></a>Installazioni per i client che non possono accedere a Active Directory Domain Services per le informazioni pubblicate  
 Tra questi client sono inclusi:  

-   Computer del gruppo di lavoro  

-   Client assegnati a un sito di Configuration Manager non pubblicato in Active Directory Domain Services  

-   Client installati quando si trovano in Internet  

 Questi computer client non sono in grado di leggere le proprietà di installazione dai Servizi di dominio Active Directory e quindi non saranno in grado di accedere alle proprietà di installazione pubblicate.  

## <a name="client-installation-properties-published-to-active-directory-domain-services"></a>Proprietà di installazione client pubblicate in Active Directory Domain Services  
 Per altre informazioni sugli elementi elencati di seguito, vedere [Informazioni sulle proprietà di installazione client in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

-   Codice del sito di Configuration Manager.  

-   Il certificato di firma del server del sito.  

-   La chiave radice attendibile.  

-   Le porte di comunicazione client per HTTP e HTTPS.  

-   Il punto di stato di fallback. Se nel sito sono presenti più punti di stato di fallback, soltanto il primo elemento installato verrà pubblicato Servizi di dominio Active Directory.  

-   Un'impostazione per indicare che il client deve comunicare solo tramite HTTPS.  

-   Impostazioni relative ai certificati PKI:  

    -   Se si desidera utilizzare un certificato PKI del client.  

    -   I criteri di selezione dei certificati, se necessario perché il client dispone di più certificati PKI validi che possono essere usati per Configuration Manager.  

    -   Un'impostazione per stabilire quale certificato utilizzare se il client dispone di più certificati validi dopo il processo di selezione del certificato.  

    -   L'elenco di autorità emittenti del certificato che contiene un elenco di certificati CA radice attendibili.  

-   Le proprietà di installazione client.msi specificate nella scheda **Client** della finestra di dialogo **Proprietà installazione push client** .



<!--HONumber=Nov16_HO1-->


