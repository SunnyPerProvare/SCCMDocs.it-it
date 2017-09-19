---
title: Gestire i client Linux e UNIX | Microsoft Docs
description: Gestire i client su server Linux e UNIX in System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
caps.latest.revision: "7"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 198d0cf322dfc8491ed4cfd5229e829c2279f32b
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/15/2017
---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Come gestire i client per i server Linux e UNIX in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Quando si gestiscono server Linux e UNIX con System Center Configuration Manager, è possibile configurare raccolte, finestre di manutenzione e impostazioni client per semplificare la gestione dei server. Inoltre, anche se il client di Configuration Manager per Linux e UNIX non ha un'interfaccia utente, è possibile forzarne manualmente il polling dei criteri client.

##  <a name="BKMK_CollectionsforLnU"></a> Collections of Linux and UNIX servers  
 Usare le raccolte per gestire i gruppi di server Linux e UNIX in modo analogo all'uso delle raccolte per gestire altri tipi di client. Le raccolte possono essere raccolte di appartenenza diretta o raccolte basate su query. Le raccolte basate su query identificano i sistemi operativi client, le configurazioni hardware o altri dettagli relativi ai client archiviati nel database del sito. Ad esempio, è possibile usare le raccolte che includono server Linux e UNIX per gestire le impostazioni seguenti:  

-   Impostazioni client  

-   Distribuzioni software  

-   Imposizione delle finestre di manutenzione  

 Prima di poter identificare un client Linux o UNIX mediante il relativo sistema operativo o la relativa distribuzione, è necessario raccogliere l'[inventario hardware](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md) dal client.  

 Le impostazioni client predefinite per l'inventario hardware includono le informazioni sul sistema operativo di un computer client. È possibile usare la proprietà **Didascalia** della classe **Sistema operativo** per identificare il sistema operativo di un server Linux o UNIX.  

 È possibile visualizzare i dettagli relativi ai computer che eseguono il client di Configuration Manager per Linux e UNIX nel nodo **Dispositivi** dell'area di lavoro **Asset e conformità** della console di Configuration Manager. Nell'area di lavoro **Asset e conformità** della console di Configuration Manager è possibile visualizzare il nome del sistema operativo di ogni computer nella colonna **Sistema operativo**.  

 Per impostazione predefinita i server Linux e UNIX sono membri della raccolta **Tutti i sistemi** . È consigliabile creare raccolte personalizzate che includono solo i server Linux e UNIX o un loro subset. Le raccolte personalizzate consentono di gestire operazioni quali la distribuzione del software o l'assegnazione di impostazioni client ai gruppi di computer applicabili, in modo da poter misurare con precisione l'esito di una distribuzione.   

 Quando si crea una raccolta personalizzata per server Linux e UNIX, includere le query relative alle regole di appartenenza contenenti l'attributo Didascalia per l'attributo Sistema operativo. Per informazioni sulla creazione delle raccolte, vedere [Come creare le raccolte in System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

##  <a name="BKMK_MaintenanceWindowsforLnU"></a> Maintenance windows for Linux and UNIX servers  
 Il client di Configuration Manager per i server Linux e UNIX supporta l'uso di [finestre di manutenzione](../../../core/clients/manage/collections/use-maintenance-windows.md). Questo supporto è lo stesso dei client basati su Windows.  

##  <a name="BKMK_ClientSettingsforLnU"></a> Client settings for Linux and UNIX servers  
 È possibile [configurare le impostazioni client](../../../core/clients/deploy/configure-client-settings.md) che si applicano a server Linux e UNIX in modo analogo alla configurazione delle impostazioni per gli altri client.  

 Per impostazione predefinita l'opzione **Impostazioni agente client predefinite** si applica a server Linux e UNIX. È anche possibile creare impostazioni client personalizzate e distribuirle alle raccolte di client specifici.  

 Non sono presenti impostazioni client aggiuntive che si applicano solo ai client Linux e UNIX. Tuttavia, esistono impostazioni client predefinite che non si applicano ai client Linux e UNIX. Il client per Linux e UNIX applica le impostazioni solo per le funzionalità supportate.  

 Ad esempio, un'impostazione del dispositivo client personalizzata che abilita e configura le impostazioni di controllo remoto viene ignorata dal server Linux e UNIX, perché il client per Linux e UNIX non supporta il controllo remoto.  

##  <a name="BKMK_PolicyforLnU"></a> Computer policy for Linux and UNIX servers  
 Il client per i server Linux e UNIX esegue periodicamente il polling dei criteri del computer nel relativo sito per recuperare informazioni sulle configurazioni richieste e per controllare le distribuzioni.  

 È anche possibile imporre il client a un server Linux o UNIX per eseguire il polling immediato dei criteri del computer. A tale scopo, usare le credenziali **root** nel server per eseguire il comando seguente: **/opt/microsoft/configmgr/bin/ccmexec -rs policy**  

 I dettagli relativi al polling dei criteri del computer vengono inseriti nel file di log del client condiviso **scxcm.log**.  

> [!NOTE]  
>  Il client di Configuration Manager per Linux e UNIX non richiede né elabora mai i criteri utente.  

##  <a name="BKMK_ManageLinuxCerts"></a> How to manage certificates on the client for Linux and UNIX  
 Dopo aver installato il client per Linux e UNIX, è possibile usare lo strumento **certutil** per aggiornare il client con un nuovo certificato PKI e per importare un nuovo elenco di revoche di certificati (CRL). Quando si installa il client per Linux e UNIX, questo strumento viene inserito in **/opt/microsoft/configmgr/bin/certutil**. 

 Per gestire i certificati, in ogni client eseguire lo strumento certutil con una delle opzioni seguenti:  

|Opzione|Altre informazioni|  
|------------|----------------------|  
|importPFX|Usare questa opzione per specificare un certificato per sostituire il certificato attualmente usato da un client.<br /><br /> Quando si usa **-importPFX** è necessario usare anche il parametro della riga di comando **-password** per specificare la password associata al file PKCS#12.<br /><br /> Usare **-rootcerts** per specificare eventuali requisiti aggiuntivi relativi al certificato radice.<br /><br /> Esempio:  **certutil -importPFX &lt;Percorso del certificato PKCS#12> -password &lt;Password certificato\> [-rootcerts &lt;elenco certificati separati da virgola>]**|  
|-importsitecert|Usare questa opzione per aggiornare il certificato di firma del server del sito che si trova nel server di gestione.<br /><br /> Esempio: **certutil -importsitecert &lt;Percorso del certificato DER\>**|  
|-importcrl|Usare questa opzione per aggiornare l'elenco di revoche di certificati sul client con uno o più percorsi di file CRL.<br /><br /> Esempio: **certutil -importcrl &lt;percorsi file CRL separati da virgola\>**|  
