---
title: Prerequisiti per gli aggiornamenti software
titleSuffix: Configuration Manager
description: Informazioni sui prerequisiti per aggiornamenti software in Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/22/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: 1885fdb11786cce5ae65aaeb4d407fb226b6a670
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75818554"
---
# <a name="prerequisites-for-software-updates-in-configuration-manager"></a>Prerequisiti per aggiornamenti software in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo elenca i prerequisiti per gli aggiornamenti software in Configuration Manager. Per ogni prerequisito, le dipendenze esterne e interne sono elencate in tabelle separate.  

## <a name="software-update-dependencies-that-are-external-to-configuration-manager"></a>Dipendenze aggiornamenti software esterne a Configuration Manager  
 Le sezioni seguenti elencano le dipendenze esterne per gli aggiornamenti software.  

### <a name="internet-information-services"></a>Internet Information Services  
 Internet Information Services (IIS) deve essere installato nei server di sistema del sito per eseguire il punto di aggiornamento software, il punto di gestione e il punto di distribuzione. Per altre informazioni, vedere [Prerequisiti per i ruoli di sistema del sito](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### <a name="windows-server-update-services"></a>Windows Server Update Services  
 Windows Server Update Services (WSUS) è necessario per la sincronizzazione degli aggiornamenti software e per l'analisi dell'applicabilità degli aggiornamenti software nei client. È necessario installare il server WSUS prima di creare il ruolo del punto di aggiornamento software. Per un punto di aggiornamento software sono supportate le versioni di WSUS seguenti:  

- WSUS 10.0.14393 (ruolo in Windows Server 2016)
- WSUS 10.0.17763 (ruolo in Windows Server 2019) (richiede Configuration Manager 1810 o versioni successive)
- WSUS 6.2 e 6.3 (ruolo in Windows Server 2012 e Windows Server 2012 R2)
  - Se si distribuiscono gli aggiornamenti di Windows 10, sono necessari [kb 3095113 e kb 3159706 (o un aggiornamento equivalente)](#BKMK_wsus2012) per WSUS 6,2 e 6,3.

> [!NOTE]
> - A partire dalla versione 1702, Windows Server 2008 R2 non è supportato per il ruolo del punto di aggiornamento software. Per altre informazioni, vedere [Sistemi operativi supportati per i server dei sistemi del sito](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers#bkmk_2008r2sp1).
> - Quando esistono più punti di aggiornamento software in un sito, verificare che tutti eseguano la stessa versione di WSUS.

### <a name="wsus-administration-console"></a>Console di amministrazione di WSUS  
È necessaria la console di amministrazione di WSUS nel server del sito di Configuration Manager se il punto di aggiornamento software si trova in un server di sistema del sito remoto e WSUS non è ancora stato installato nel server del sito.  

> [!IMPORTANT]  
> - La versione di WSUS nel server del sito deve corrispondere alla versione di WSUS in esecuzione nei punti di aggiornamento software.
> - Non usare la console di amministrazione di WSUS per configurare le impostazioni WSUS. Configuration Manager si connette all'istanza di WSUS in esecuzione nel punto di aggiornamento software e configura le impostazioni appropriate.  


### <a name="windows-update-agent"></a>Agente di Windows Update  
 È necessario che il client dell'agente di Windows Update (WUA) sia presente nei client in modo che questi possano connettersi al server WSUS. WUA recupera l'elenco di aggiornamenti software che devono essere esaminati per verificare la conformità.  

 Quando si installa Configuration Manager, viene scaricata la versione più recente di dell'agente di Windows Update. Quando viene installato il client di Configuration Manager, l'agente di Windows Update viene aggiornato se necessario. Se l'installazione non riesce, è necessario usare un metodo diverso per eseguire l'aggiornamento dell'agente di Windows Update.  

## <a name="software-update-dependencies-that-are-internal-to-configuration-manager"></a>Dipendenze aggiornamenti software interne a Configuration Manager  
 Le sezioni seguenti elencano le dipendenze interne per gli aggiornamenti software in Configuration Manager.  

### <a name="management-points"></a>Punti di gestione  
 I punti di gestione trasferiscono le informazioni tra i computer client e il sito di Configuration Manager. I punti di gestione sono necessari per gli aggiornamenti software.  

### <a name="software-update-points"></a>Punti di aggiornamento software  
 È necessario installare un punto di aggiornamento software nel server WSUS per distribuire gli aggiornamenti software in Configuration Manager. Per altre informazioni, vedere [Installare e configurare un punto di aggiornamento software](../get-started/install-a-software-update-point.md).

### <a name="distribution-points"></a>Punti di distribuzione  
 I punti di distribuzione sono necessari per archiviare il contenuto per gli aggiornamenti software. Per altre informazioni su come installare i punti di distribuzione e gestire il contenuto, vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="client-settings-for-software-updates"></a>Impostazioni client per gli aggiornamenti software  
Gli aggiornamenti software sono abilitati per i client per impostazione predefinita. Sono disponibili altre impostazioni che controllano come e quando i client valutano la conformità per gli aggiornamenti software e la relativa modalità di installazione.  

 Per altre informazioni, vedere gli articoli seguenti:  

- [Impostazioni client per gli aggiornamenti software](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

- [Informazioni sulle impostazioni client per gli aggiornamenti software](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-points"></a>Punti di Reporting Services  
 Il ruolo del sistema del sito del punto di Reporting Services può visualizzare i report per gli aggiornamenti software. Questo ruolo è facoltativo ma consigliato. Per altre informazioni su come creare un punto di Reporting Services, vedere [Configurazione della creazione di report](../../core/servers/manage/configuring-reporting.md).  

## <a name="BKMK_wsus2012"></a>Quali aggiornamenti sono necessari in WSUS 6,2 e 6,3?

Sono necessari due aggiornamenti per la sincronizzazione della classificazione degli **aggiornamenti** in WSUS 6,2 e 6,3. In alcuni casi, è possibile che venga visualizzato un errore durante il download o la distribuzione degli aggiornamenti, se sincronizzati prima dell'installazione di KB3095113 e KB3159706. Le informazioni sui possibili problemi sono disponibili nella sezione successiva.  

- È necessario installare [KB 3095113](https://support.microsoft.com/kb/3095113), rilasciato in ottobre 2015, nei punti di aggiornamento software e nei server del sito prima della sincronizzazione della classificazione **Aggiornamenti**.
  - Questo aggiornamento Abilita la classificazione degli **aggiornamenti** .
- Per eseguire il servizio Windows 10 versione 1607 e successive, è necessario installare e configurare [KB 3159706](https://support.microsoft.com/en-us/help/3159706). La versione KB 3159706 è stata rilasciata nel maggio 2016.
  - Questo aggiornamento consente a WSUS di decrittografare in modo nativo i file usati per l'aggiornamento di Windows 10 versione 1607 e successive.

>[!IMPORTANT]
> Entrambe le KB 3095113 e KB 3159706 sono incluse nel **rollup di qualità mensile** per la sicurezza a partire dal 2017 luglio. Ciò significa che è possibile che non vengano visualizzati KB 3095113 e KB 3159706 come aggiornamenti installati, dal momento che potrebbero essere stati installati con un rollup. Tuttavia, se è necessario uno di questi aggiornamenti, si consiglia di installare un **rollup di qualità mensile** per la sicurezza rilasciato dopo il 2017 ottobre poiché contengono un aggiornamento WSUS aggiuntivo per ridurre l'utilizzo della memoria nei CLIENTWEBSERVICE di WSUS.

## <a name="BKMK_RecoverUpgrades"></a>Il download degli aggiornamenti di Windows 10 non riesce con "errore: firma del certificato non valida" o 0xc1800118

Gli aggiornamenti e il problema descritti in questa sezione si applicano solo a WSUS in esecuzione in computer Windows Server 2012 o Windows Server 2012 R2 (WSUS 6,2 e 6,3). In genere, verranno visualizzati solo i problemi descritti in questa sezione se WSUS è stato installato prima di luglio 2017 e la classificazione degli **aggiornamenti** è stata abilitata di recente. Tuttavia, è possibile riscontrare questi problemi anche in altre situazioni.

### <a name="historical-information-about-kb-3095113"></a>Informazioni cronologiche su KB 3095113

 La versione [KB 3095113](https://support.microsoft.com/kb/3095113) è stata [rilasciata come hotfix](https://blogs.technet.microsoft.com/wsus/2015/12/03/important-update-for-wsus-4-0-kb-3095113/) nel ottobre 2015 per aggiungere il supporto per gli aggiornamenti di Windows 10 a WSUS. L'aggiornamento Abilita WSUS per la sincronizzazione e la distribuzione degli aggiornamenti nella classificazione degli **aggiornamenti** per Windows 10.

Se si sincronizzano gli eventuali aggiornamenti senza avere prima installato [KB 3095113](https://support.microsoft.com/kb/3095113), nel database WSUS (SUSDB) vengono inseriti dati inutilizzabili. Tali dati devono essere cancellati prima di poter distribuire correttamente gli aggiornamenti. Non è possibile scaricare gli aggiornamenti di Windows 10 in questo stato usando il download guidato degli aggiornamenti software.

Gli errori simili ai seguenti vengono visualizzati nella pagina completamento del download guidato degli aggiornamenti software:

``` Output
Error: Upgrade to Windows 10 Pro, version 1511, 10586
Failed to download content id {content_id}. Error: Invalid certificate signature
```

Inoltre, gli errori simili a quelli riportati di seguito vengono registrati nel file PatchDownloader. log:

``` Log
Download http://wsus.ds.b1.download.windowsupdate.com/d/upgr/2015/12/10586.0.151029-1700.th2_release_...esd...
Authentication of file C:\Users\{username}\AppData\Local\Temp\2\{temporary_filename}.tmp failed, error 0x800b0004
ERROR: DownloadContentFiles() failed with hr=0x80073633
# This log is truncated for readability.
```

Storicamente, quando si sono verificati questi errori, questi vengono risolti eseguendo una versione modificata dei [passaggi di risoluzione per WSUS](https://blogs.technet.microsoft.com/wsus/2016/01/29/how-to-delete-upgrades-in-wsus/). Poiché questi passaggi sono simili alla risoluzione per non eseguire i passaggi manuali necessari dopo l'installazione di KB 3159706, sono stati combinati entrambi i set di passaggi in un'unica risoluzione nella sezione seguente:

- [Per eseguire il ripristino dalla sincronizzazione degli aggiornamenti prima di installare KB 3095113 o KB 3159706](#bkmk_fix-upgrades).

### <a name="historical-information-about-kb-3159706"></a>Informazioni cronologiche su KB 3159706

La versione KB 3148812 è stata inizialmente rilasciata nel aprile 2016 per consentire a WSUS di decrittografare in modo nativo i file con estensione ESD usati per l'aggiornamento dei pacchetti Windows 10 La [kb 3148812 ha causato problemi per alcuni clienti](https://blogs.technet.microsoft.com/wsus/2016/05/05/the-long-term-fix-for-kb3148812-issues/) ed è stata sostituita con [KB 3159706](https://support.microsoft.com/en-us/help/3159706). Prima di poter soddisfare i dispositivi Windows 10 versione 1607 e successive, è necessario installare KB 3159706 in tutti i punti di aggiornamento software e nei server del sito. Tuttavia, possono verificarsi problemi se non si è consapevoli che la KB richiede i seguenti passaggi manuali dopo l'installazione:

1. Da un prompt dei comandi con privilegi elevati eseguire `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing`.
1. Riavviare il servizio WSUS in tutti i server WSUS.

Se non si è consapevoli del fatto che la KB 3159706 ha eseguito una procedura manuale dopo l'installazione o che è stata eseguita la sincronizzazione nell'aggiornamento per Windows 10 1607 prima di installare KB 3159706, si verificheranno problemi di connessione alla console WSUS e la distribuzione dell'aggiornamento rispettivamente. Quando un client Scarica il file di aggiornamento, riceverà un [codice di errore **0xC1800118** ](https://support.microsoft.com/help/3194588/0xc1800118-error-when-you-push-windows-10-version-1607-by-using-wsus).

Poiché i passaggi di risoluzione sono simili alla risoluzione per la sincronizzazione degli aggiornamenti prima dell'installazione di KB 3095113, sono stati combinati entrambi i set di passaggi in un'unica risoluzione nella sezione successiva.
 

### <a name="bkmk_fix-upgrades"></a> Per eseguire il ripristino dalla sincronizzazione degli aggiornamenti prima di installare KB 3095113 o KB 3159706

Attenersi alla procedura seguente per risolvere l'errore 0xc1800118 e "errore: firma del certificato non valida":

1. Disabilitare la classificazione **aggiornamenti** sia in WSUS che in Configuration Manager. Non si vuole che venga eseguita una sincronizzazione fino a quando non si viene reindirizzati a queste istruzioni.  
   - Deselezionare la classificazione **Aggiornamenti** nelle proprietà del componente del punto di aggiornamento software per il sito di primo livello.
     - Per altre informazioni, vedere [Configurare le classificazioni e i prodotti](../get-started/configure-classifications-and-products.md).
   - Deselezionare la classificazione **aggiornamenti** da WSUS in **prodotti e classificazioni** nella [pagina **Opzioni** ](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/setting-up-update-synchronizations)oppure usare PowerShell ISE eseguito come amministratore.
      ```PowerShell
      Get-WsusClassification | Where-Object -FilterScript {$_.Classification.Title -Eq “Upgrades”} | Set-WsusClassification -Disable
      ```  
     - Se si condivide il database WSUS tra più server WSUS, è sufficiente deselezionare gli **aggiornamenti** una volta per ogni database.  
1. In ogni server WSUS, da un prompt dei comandi con privilegi elevati eseguire: `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing`. Riavviare quindi il servizio WSUS in tutti i server WSUS.
   -  WSUS posiziona il database in [modalità utente singolo](https://docs.microsoft.com/sql/relational-databases/databases/set-a-database-to-single-user-mode) prima di verificare se è necessaria la manutenzione. La manutenzione viene eseguita o non viene eseguita in base ai risultati del controllo. Quindi, il database viene ripristinato in modalità multiutente. 
   - Se si condivide il database WSUS tra più server WSUS, è necessario eseguire questa operazione una sola volta per ogni database.
1. Eliminare tutti gli aggiornamenti di Windows 10 da ogni database WSUS usando PowerShell ISE eseguito come amministratore.
   ```PowerShell
   [reflection.assembly]::LoadWithPartialName("Microsoft.UpdateServices.Administration")
   $wsus = [Microsoft.UpdateServices.Administration.AdminProxy]::GetUpdateServer();
   $wsus.GetUpdates() | Where {$_.UpdateClassificationTitle -eq 'Upgrades' -and $_.Title -match 'Windows 10'} `
   | ForEach-Object {$wsus.DeleteUpdate($_.Id.UpdateId.ToString()); Write-Host $_.Title removed}
   ```
1. Eliminare i file dalla tabella tbFile da ognuno dei database WSUS usati dai punti di aggiornamento software. Nel database WSUS eseguire i comandi seguenti da SQL Server Management Studio:
   ```SQL
   declare @NotNeededFiles table (FileDigest binary(20) UNIQUE)
   insert into @NotNeededFiles(FileDigest) (select FileDigest from tbFile where FileName like '%.esd%'  except select FileDigest from tbFileForRevision)
   delete from tbFileOnServer where FileDigest in (select FileDigest from @NotNeededFiles)
   delete from tbFile where FileDigest in (select FileDigest from @NotNeededFiles)
   ```
1. Avviare la sincronizzazione degli aggiornamenti software nel sito di livello superiore in Configuration Manager e attenderne il completamento. Si verifica una sincronizzazione completa perché è stata apportata una modifica alle classificazioni Configuration Manager quando sono stati rimossi gli **aggiornamenti**. Per altre informazioni, vedere [Sincronizzare gli aggiornamenti software](../get-started/synchronize-software-updates.md).
1. Selezionare la classificazione **Aggiornamenti** nelle proprietà del componente del punto di aggiornamento software. Avviare quindi un'altra sincronizzazione degli aggiornamenti software per riportare gli **aggiornamenti** in WSUS e Configuration Manager. Non è necessario abilitare la classificazione degli **aggiornamenti** in WSUS poiché Configuration Manager lo eseguirà per l'utente.
1. Se i client hanno ricevuto il codice di errore **0xC1800118** durante il download di un aggiornamento, è necessario eliminare l'archivio dati usato dall'agente di Windows Update. Potrebbe anche essere necessario eliminare la cartella nascosta ~ BT nel dispositivo. Alla successiva analisi da parte del client, sarà eseguita un'analisi completa sul server WSUS invece che su un Delta. È possibile usare uno script di PowerShell simile allo script di esempio riportato di seguito:  
   ```PowerShell
   stop-service wuauserv
   remove-item -path c:\windows\softwaredistribution\datastore -recurse -force
   # If the device has a hidden ~BT folder on the c drive, delete it too by uncommenting the next line.
   # remove-item -path c:\~BT -recurse -force
   start-service wuauserv
   ```

## <a name="next-steps"></a>Passaggi successivi
[Preparare la gestione degli aggiornamenti software](../get-started/prepare-for-software-updates-management.md)
