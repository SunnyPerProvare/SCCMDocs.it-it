---
title: Creare query | System Center Configuration Manager
description: Questo argomento illustra come creare e importare query in System Center Configuration Manager. Include query di esempio e suggerimenti.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1cbba80a73fdd66d84d38e710c02cc79ab972b81


---
# <a name="how-to-create-queries-in-system-center-configuration-manager"></a>Come creare query in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare le sezioni seguenti di questo argomento per informazioni su come creare o importare query in System Center Configuration Manager.  

-   [How to Create Queries](#BKMK_Create)  

-   [How to Import Queries](#BKMK_Import)  

-   [Example WQL Queries](#BKMK_Example)  

##  <a name="a-namebkmkcreatea-how-to-create-queries"></a><a name="BKMK_Create"></a> Come creare query  
 Usare questa procedura per creare query in Configuration Manager.  

#### <a name="to-create-a-query"></a>Per creare una query  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** fare clic su **Query** e quindi nel gruppo **Crea** della scheda **Home** fare clic su **Crea query**.  

3.  Nella scheda **Generale** della **Creazione guidata query**specificare un nome univoco e un commento facoltativo per la query.  

4.  Se si vuole importare una query esistente da usare come base per la nuova query, fare clic su **Importa istruzione query** e quindi nella finestra di dialogo **Sfoglia query** selezionare una query esistente da importare e infine fare clic su **OK**.  

5.  Nell'elenco **Tipo oggetto** selezionare il tipo di oggetto che si vuole che la query restituisca. Nella tabella seguente vengono descritti alcuni esempi del tipo di oggetto che è possibile cercare:  

    |Tipo oggetto|Descrizione|  
    |-----------------|-----------------|  
    |**Risorsa di sistema**|Usare questo tipo di oggetto per cercare attributi di sistema standard, ad esempio il nome NetBIOS di un dispositivo, la versione del client, l'indirizzo IP del client e informazioni su Servizi di dominio Active Directory.|  
    |**Risorsa utente**|Usare questo tipo di oggetto per cercare informazioni utente standard, ad esempio nomi utente, nomi di gruppi di utenti e nomi dei gruppi di sicurezza.|  
    |**Distribuzione**|Usare questo tipo di oggetto per cercare gli attributi standard di una distribuzione, ad esempio il nome della distribuzione, la pianificazione e la raccolta in cui è stata distribuita.|  

6.  Fare clic su **Modifica istruzione query** per aprire la finestra di dialogo *&lt;Nome query\>***Proprietà istruzione**.  

7.  Nella scheda **Generale** della finestra di dialogo *&lt;Nome query\>***Proprietà istruzione** specificare gli attributi restituiti da questa query e la relativa modalità di visualizzazione. Fare clic sull'icona **Nuovo** per aggiungere un nuovo attributo. È anche possibile fare clic su **Mostra linguaggio query** per immettere o modificare la query direttamente in WMI Query Language (WQL). Per esempi di query WMI, vedere la sezione [Example WQL queries](#BKMK_Example) in questo argomento.  

    > [!TIP]  
    >  È possibile usare la documentazione di riferimento MSDN seguente per creare query WQL personalizzate:  
    >   
    >  -   [WQL (SQL per WMI)](http://go.microsoft.com/fwlink/p/?LinkId=256653)  
    > -   [Clausola WHERE](http://go.microsoft.com/fwlink/p/?LinkId=256654)  
    > -   [Operatori WQL](http://go.microsoft.com/fwlink/p/?LinkId=256655)  

8.  Nella scheda **Criteri** della finestra di dialogo *&lt;Nome query\>***Proprietà istruzione** specificare i criteri usati per definire i risultati della query. Ad esempio, è possibile restituire solo le risorse con un codice di sito **XYZ** nei risultati della query. È possibile configurare più criteri per una query.  

    > [!IMPORTANT]  
    >  Se si crea una query che non contiene alcun criterio, verranno restituiti tutti i dispositivi presenti nella raccolta **Tutti i sistemi** .  

9. Nella scheda **Join** della finestra di dialogo *&lt;Nome query\>***Proprietà istruzione** è possibile combinare i dati di due attributi diversi nei risultati della query. Anche se Configuration Manager crea automaticamente join di query quando vengono selezionati attributi diversi per il risultato della query, nella scheda **Join** sono disponibili ulteriori opzioni avanzate. Le classi di attributi supportate da System Center 2012 Configuration Manager sono illustrate nella tabella seguente:  

    |Tipo di join|Descrizione|  
    |---------------|-----------------|  
    |Inner|Consente di visualizzare solo i risultati corrispondenti e viene sempre usato per i join creati automaticamente.|  
    |Sinistra|Consente di visualizzare tutti i risultati per l'attributo di base e solo i risultati corrispondenti per l'attributo di join.|  
    |Destra|Consente di visualizzare tutti i risultati per l'attributo di join e solo i risultati corrispondenti per l'attributo di base.|  
    |Completo|Consente di visualizzare tutti i risultati sia per l'attributo di base che per l'attributo di join.|  

     Per altre informazioni su come usare le operazioni di join, vedere la documentazione di SQL Server.  

10. Fare clic su **OK** per chiudere la finestra di dialogo *&lt;Nome query\>***Proprietà istruzione**.  

11. Nella scheda **Generale** della **Creazione guidata query**specificare se i risultati della query non sono limitati ai membri di una raccolta, sono limitati ai membri di una raccolta specificata oppure se viene richiesta una raccolta ogni volta che viene eseguita la query.  

12. Completare la procedura guidata per creare la query. La nuova query verrà visualizzata nel nodo **Query** nell'area di lavoro **Monitoraggio** .  

##  <a name="a-namebkmkimporta-how-to-import-queries"></a><a name="BKMK_Import"></a> Come importare le query  
 Usare questa procedura per importare una query in Configuration Manager. Per informazioni su come esportare le query, vedere [Come gestire le query in System Center Configuration Manager](../../../core/servers/manage/manage-queries.md).  

#### <a name="to-import-a-query"></a>Per importare una query  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** fare clic su **Query** e quindi nel gruppo **Crea** della scheda **Home** fare clic su **Importa oggetti**.  

3.  Nella pagina **Nome file MOF** dell' **Importazione guidata oggetti**fare clic su **Sfoglia** per selezionare un file MOF (Managed Object Format) contenente la query da importare.  

4.  Esaminare le informazioni relative alla query da importare e quindi completare la procedura guidata. La nuova query verrà visualizzata nel nodo **Query** nell'area di lavoro **Monitoraggio** .  

##  <a name="a-namebkmkexamplea-example-wql-queries"></a><a name="BKMK_Example"></a> Example WQL queries  
 Questa sezione contiene query WMI di esempio che è possibile usare nella gerarchia o modificare per altri scopi. Per usare queste query, fare clic su **Mostra linguaggio query** nella finestra di dialogo **Proprietà istruzione query** e quindi copiare e incollare la query nel campo **Istruzione query** .  

> [!TIP]  
>  Usare il carattere jolly **%** per indicare qualsiasi stringa di caratteri. Ad esempio, **%Visio%** restituisce Microsoft Office Visio 2010.  

### <a name="computers-that-run-windows-7"></a>Computer che eseguono Windows 7  
 Usare la query seguente per restituire il nome NetBIOS e la versione del sistema operativo di tutti i computer che eseguono Windows 7.  

> [!TIP]  
>  Per restituire i computer che eseguono Windows Server 2008 R2, modificare **%Workstation 6.1%** in **%Server 6.1%**.  

```  
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from    
SMS_R_System where   
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 6.1%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>Computer con uno specifico pacchetto software installato  
 Usare la query seguente per restituire il nome NetBIOS e il nome del pacchetto software di tutti i computer in cui è installato un pacchetto software specifico. Questo esempio visualizza tutti i computer con una versione di Microsoft Visio installata. Sostituire **%Visio%** con il pacchetto software che si vuole cercare.  

> [!TIP]  
>  Questa query cerca il pacchetto software usando i nomi visualizzati nell'elenco di programmi nel Pannello di controllo di Windows.  

```  
select SMS_R_System.NetbiosName,   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from    
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on   
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =   
SMS_R_System.ResourceId where   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "%Visio%"  
```  

### <a name="computers-that-are-in-a-specific-active-directory-domain-services-organizational-unit-ou"></a>Computer inclusi in una specifica unità organizzativa di Servizi di dominio Active Directory  
 Usare la query seguente per restituire il nome NetBIOS e il nome dell'unità organizzativa di tutti i computer in un'unità organizzativa specificata. Sostituire il testo **OU Name** con il nome dell'unità organizzativa che si vuole cercare.  

```  
select SMS_R_System.NetbiosName,   
SMS_R_System.SystemOUName from    
SMS_R_System where   
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>Computer con un nome NetBIOS specifico  
 Usare la query seguente per restituire il nome NetBIOS di tutti i computer il cui nome inizia con una stringa specifica di caratteri. In questo esempio la query restituisce tutti i computer con un nome NetBIOS che inizia con **ABC**.  

```  
select SMS_R_System.NetbiosName from    
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="a-namebkmkdevicetypea-devices-of-a-specific-type"></a><a name="BKMK_DeviceType"></a> Dispositivi di un tipo specifico  
 I tipi di dispositivo vengono archiviati nel database di Configuration Manager con la classe di risorse **sms_r_system** e il nome di attributo **AgentEdition**. Usare la query seguente per recuperare solo i dispositivi che corrispondono all'edizione dell'agente del tipo di dispositivo specificato:  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

 Usare uno dei valori seguenti per *&lt;ID dispositivo\>*:  

|Tipo di dispositivo|Valore di AgentEdition|  
|-----------------|---------------------------|  
|Computer desktop o portatile Windows|0|  
|Dispositivo Windows basato su ARM (che esegue Windows RT)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Computer Mac|5|  
|Windows CE|6|  
|Windows Embedded|7|  
|iOS|8|  
|iPad|9|  
|iPod Touch|10|  
|Android|11|  
|Intel System On Chip (SOC)|12|  
|Server UNIX e Linux|13|  

 Ad esempio, se si vuole che la query restituisca solo i computer Mac, usare la query seguente:  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="see-also"></a>Vedere anche  
 [Operazioni e manutenzione per le query in System Center Configuration Manager](../../../core/servers/manage/operations-and-maintenance-for-queries.md)



<!--HONumber=Nov16_HO1-->

