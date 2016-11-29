---
title: Servizi componenti e comandi dei client UNIX/Linux | System Center Configuration Manager
description: Informazioni sui servizi componenti e i comandi nei client Linux e UNIX in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
caps.latest.revision: 6
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 92ce5cadc1303fea9dbf828d22fa80e837583e32


---
# <a name="linux-and-unix-clients-component-services-and-commands-for-system-center-configuration-manager"></a>Servizi componenti e comandi dei client Linux e UNIX per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


 Nella tabella seguente sono riportati i servizi componenti client del client di Configuration Manager per Linux e UNIX.  

|Nome del file|Altre informazioni|  
|---------------|----------------------|  
|ccmexec.bin|Questo servizio equivale al servizio ccmexc in un client basato su Windows. È responsabile di tutte le comunicazioni con i ruoli del sistema del sito di Configuration Manager e comunica anche con il servizio omiserver.bin per raccogliere l'inventario hardware dal computer locale.<br /><br /> Per un elenco di argomenti della riga di comando supportati, eseguire **ccmexec -h**|  
|omiserver.bin|Questo servizio è il server CIM. Il server CIM fornisce un framework per i moduli software plug-in denominati provider. I provider interagiscono con le risorse dei computer Linux e UNIX e raccolgono i dati di inventario hardware. Ad esempio, il **provider process** per Linux computer raccoglie i dati associati ai processi del sistema operativo Linux.|  

 I seguenti comandi dell'elenco di tabelle che è possibile utilizzare per avviare, arrestare o riavviare i servizi client (CCMExec e omiserver) in ogni versione di Linux o UNIX. Quando si avvia o arresta il servizio ccmexec, viene avviato o arrestato anche il servizio omiserver.  

|Sistema operativo|Comandi:|  
|----------------------|--------------|  
|Universal Agent<br /><br /> RHEL 4 e SLES 9|Avvia: **/etc/init d/ccmexecd start**<br /><br /> Arresta: **/etc/init d/ccmexecd stop**<br /><br /> Riavvia: **/etc/init d/ccmexecd restart**|  
|Solaris 9|Avvia: **/etc/init d/ccmexecd start**<br /><br /> Arresta: **/etc/init d/ccmexecd stop**<br /><br /> Riavvia: **/etc/init d/ccmexecd restart**|  
|Solaris 10|Avvia:<br /><br /> **svcadm enable -s svc:/application/management/omiserver**<br /><br /> **svcadm enable -s svc:/application/management/ccmexecd**<br /><br /> Arresta:<br /><br /> **svcadm disable -s svc:/application/management/ccmexecd**<br /><br /> **svcadm disable -s svc:/application/management/omiserver**|  
|Solaris 11|Avvia:<br /><br /> **svcadm enable -s svc:/application/management/omiserver**<br /><br /> **svcadm enable -s svc:/application/management/ccmexecd**<br /><br /> Arresta:<br /><br /> **svcadm disable -s svc:/application/management/ccmexecd**<br /><br /> **svcadm disable -s svc:/application/management/omiserver**|  
|AIX|Avvia:<br /><br /> **startsrc -s omiserver**<br /><br /> **startsrc -s ccmexec**<br /><br /> Arresta:<br /><br /> **stopsrc -s ccmexec**<br /><br /> **stopsrc -s omiserver**|  
|HP-UX|Avvia: **/sbin/init.d/ccmexecd start**<br /><br /> Arresta: **/sbin/init.d/ccmexecd stop**<br /><br /> Riavvia: **/sbin/init.d/ccmexecd restart**|  



<!--HONumber=Nov16_HO1-->

