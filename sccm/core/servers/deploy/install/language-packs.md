---
title: Language Pack
titleSuffix: Configuration Manager
description: Informazioni sul supporto per le lingue disponibile in System Center Configuration Manager.
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a198e15a1ef389d792acc73f2253aa4a704ac35a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32340309"
---
# <a name="language-packs-in-system-center-configuration-manager"></a>Language Pack in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In questo argomento vengono forniti dettagli tecnici sul supporto per le lingue in System Center Configuration Manager.  

## <a name="BKMK_SupLanguagePacks"></a> Lingue del sistema operativo supportate  
 È possibile installare il supporto per le lingue visualizzate nelle tabelle seguenti installando i **Language Pack server** o i **Language Pack client** in un sito di amministrazione centrale e nei siti primari. Durante il processo di installazione di un sito si selezionano le lingue per server e client da supportare in quel sito scegliendole dai file dei Language Pack disponibili.

 I file dei Language Pack vengono scaricati quando si esegue il programma di installazione come parte del download dei file di prerequisiti e ridistribuibili. È anche possibile usare [Downloader di installazione](setup-downloader.md) per scaricare questi file prima di eseguire il programma di installazione.   

 Usare la tabella seguente per eseguire il mapping di un ID impostazioni locali con una lingua da supportare nei server o nei computer client. Per altre informazioni sugli ID impostazioni locali, vedere [ID impostazioni locali assegnati da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=252609).  

### <a name="server-languages"></a>Lingue server  

|Lingua server|ID impostazioni locali (LCID)|Codice di tre lettere|  
|---------------------|------------------------|-----------------------|  
|Inglese (predefinito)|0409|ITA|  
|Cinese (tradizionale, RAS di Hong Kong)|0c04|ZHH|  
|Cinese (semplificato)|0804|CHS|  
|Cinese (tradizionale, Taiwan)|0404|CHT|  
|Ceco|0405|CSY|  
|Olandese (Paesi Bassi)|0413|NLD|  
|Francese|040c|FRA|  
|Tedesco|0407|DEU|  
|Ungherese|040e|HUN|  
|Italiano - Italia|0410|ITA|  
|Giapponese|0411|JPN|  
|Coreano|0412|KOR|  
|Polacco|0415|PLK|  
|Portoghese (Brasile)|0416|PTB|  
|Portoghese (Portogallo)|0816|PTG|  
|Russo|0419|RUS|  
|Spagnolo (Spagna)|0c0a|ESN|  
|Svedese|041d|SVE|  
|Turco|041f|TRK|  

### <a name="client-languages"></a>Lingue client  

|Lingua client|ID impostazioni locali (LCID)|Codice di tre lettere|  
|---------------------|------------------------|-----------------------|  
|Inglese (predefinito)|0409|ENG|  
|Cinese (tradizionale, Hong Kong-R.A.S.)|0c04|ZHH|  
|Cinese (semplificato)|0804|CHS|  
|Cinese (tradizionale, Taiwan)|0404|CHT|  
|Ceco|0405|CSY|  
|Danese|0406|DAN|  
|Olandese (Paesi Bassi)|0413|NLD|  
|Finlandese|040b|FIN|  
|Francese|040c|FRA|  
|Tedesco|0407|DEU|  
|Greco|0408|ELL|  
|Ungherese|040e|HUN|  
|Italiano - Italia|0410|ITA|  
|Giapponese|0411|JPN|  
|Coreano|0412|KOR|  
|Norvegese|0414|NOR|  
|Polacco|0415|PLK|  
|Portoghese (Brasile)|0416|PTB|  
|Portoghese (Portogallo)|0816|PTG|  
|Russo|0419|RUS|  
|Spagnolo (Spagna)|0c0a|ESN|  
|Svedese|041d|SVE|  
|Turco|041f|TRK|  

### <a name="mobile-device-client-languages"></a>Lingue client per dispositivi mobili  
 Quando si aggiunge il supporto per le lingue per dispositivi mobili, vengono incluse tutte le lingue client per dispositivi mobili supportate. Non è possibile selezionare singoli Language Pack per il supporto dei dispositivi mobili.  

### <a name="identify-installed-language-packs"></a>Identificare i Language Pack installati  
Per identificare i Language Pack installati in un computer che esegue il client di Configuration Manager, cercare l'ID impostazioni locali (LCID) dei Language Pack installati nel Registro di sistema del computer. Queste informazioni sono disponibili in:

 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs**  

È possibile utilizzare l'inventario hardware per raccogliere queste informazioni e quindi generare un report personalizzato per visualizzare i dettagli relativi alla lingua. Per informazioni sulla raccolta di inventario hardware, vedere [How to configure hardware inventory in System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md) (Come configurare l'inventario hardware in System Center Configuration Manager). Per informazioni sulla creazione di report, vedere la sezione [Gestire i report di Configuration Manager](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md#BKMK_ManageReports) nell'argomento [Operazioni e manutenzione per la creazione di report in System Center Configuration Manager](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md).  
