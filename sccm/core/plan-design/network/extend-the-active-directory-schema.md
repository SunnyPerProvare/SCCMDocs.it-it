---
title: Schema di Active Directory | System Center Configuration Manager
description: Estendere lo schema di Active Directory per System Center Configuration Manager per semplificare il processo di distribuzione e configurazione dei client.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bc15ee7e-4d0a-4463-ae2c-f72d8d45d65d
caps.latest.revision: 17
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d4cdaa646265b2d05ec93aeaefaf3a6e7a2c269f


---
# <a name="extend-the-active-directory-schema-for-system-center-configuration-manager"></a>Estendere lo schema di Active Directory per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Quando si estende lo schema di Active Directory per System Center Configuration Manager si introducono nuove strutture in Active Directory usate dai siti di System Center Configuration Manager per pubblicare le informazioni chiave in una posizione sicura facilmente accessibile ai client.  

 È consigliabile usare Configuration Manager con uno schema di Active Directory esteso quando si gestiscono client locali. Uno schema esteso può semplificare il processo di distribuzione e configurazione dei client e consente ai client di individuare in modo efficiente le risorse, ad esempio server di contenuti e altri servizi forniti dai diversi ruoli del sistema del sito di Configuration Manager.  

-   Se non si sa quale schema esteso offra una distribuzione di Configuration Manager, vedere [Schema extensions for System Center Configuration Manager](../../../core/plan-design/network/schema-extensions.md)  (Estensioni dello schema per System Center Configuration Manager) per informazioni utili in proposito.  

-   Se non si usa uno schema esteso, è possibile rilevare i servizi e i server del sistema del sito configurando altri metodi, ad esempio DNS e WINS. Questi metodi di individuazione de della posizione del servizio richiedono configurazioni aggiuntive e non sono il metodo preferito per l'individuazione della posizione del servizio da parte dei client. Per altre informazioni, vedere [Informazioni su come i client trovano i servizi e le risorse del sito per System Center Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md),  

-   Se lo schema di Active Directory è stato esteso per Configuration Manager 2007 o System Center Configuration Manager 2012, non è necessario eseguire altre operazioni. Le estensioni dello schema sono invariate e saranno già applicate.  

L'estensione dello schema è un'operazione eseguita una sola volta per ogni foresta. Per estendere e quindi usare lo schema di Active Directory esteso è necessario quanto segue:  

## <a name="step-1-extend-the-schema"></a>Passaggio 1. Estendere lo schema  
Per l'estensione dello schema per Configuration Manager è necessario:  

-   Usare un account che sia membro del gruppo di sicurezza Schema Admins  

-   Avere eseguito l'accesso al controller di dominio master dello schema  

-   Eseguire lo strumento **Extadsch.exe** oppure usare l'utilità della riga di comando LDIFDE con il file **ConfigMgr_ad_schema.ldf** . Lo strumento e il file si trovano entrambi nella cartella **SMSSETUP\BIN\X64** del supporto di installazione di Configuration Manager.  

#### <a name="option-a-use-extadschexe"></a>Opzione A: usare Extadsch.exe  

1.  Eseguire **extadsch.exe** per aggiungere nuove classi e attributi allo schema di Active Directory.  

    > [!TIP]  
    >  Eseguire lo strumento da una riga di comando per visualizzare il feedback mentre è in esecuzione.  

2.  Verificare che l'estensione dello schema abbia avuto esito positivo riesaminando il file extadsch.log che si trova nella radice dell'unità di sistema.  

#### <a name="option-b-use-the-ldif-file"></a>Opzione B: usare il file LDIF  

1.  Modificare il file **ConfigMgr_ad_schema.ldf** per definire il dominio radice di Active Directory da estendere:  

    -   Tutte le istanze del testo **DC=x** nel file devono essere sostituite con il nome completo del dominio da estendere  

    -   Se ad esempio il nome completo del dominio da estendere è widgets.microsoft.com, modificare tutte le istanze di DC=x nel file in **DC=widgets, DC=microsoft, DC=com**.  

2.  Usare l'utility della riga di comando LDIFDE per importare i contenuti del file **ConfigMgr_ad_schema.ldf** in Servizi di dominio Active Directory:  

    -   Ad esempio, la seguente riga di comando importa le estensioni dello schema in Active Directory Domain Services, attiva la registrazione dettagliata e crea un file di log durante il processo di importazione: **ldifde -i -f ConfigMgr_ad_schema.ldf -v -j &lt;percorso di archiviazione del file di log\>**  

3.  Per verificare la riuscita dell'estensione dello schema, è possibile esaminare il file di log creato dalla riga di comando usata nel passaggio precedente.  

## <a name="step-2-create-the-system-management-container-and-grant-sites-permissions-to-the-container"></a>Passaggio 2:  Creare il contenitore di System Management e concedere le autorizzazioni per i siti al contenitore  
 Dopo aver esteso lo schema, è necessario creare un contenitore denominato **System Management** in Active Directory Domain Services:  

-   Questo contenitore viene creato una sola volta in ogni dominio che include un sito primario o secondario che pubblicherà dati in Active Directory  

-   Per ogni contenitore vengono concesse autorizzazioni all'account del computer di ogni server del sito primario e secondario che pubblica dati nel dominio. Ogni account deve avere **Controllo completo** sul contenitore con l'autorizzazione avanzata **Applica a** impostata su **Questo oggetto e tutti i discendenti**  

#### <a name="to-add-the-container"></a>Per aggiungere il contenitore  

1.  Accedere con un account con l'autorizzazione **Crea tutti gli oggetti figlio** per il contenitore **Sistema** nei Servizi di dominio Active Directory.  

2.  Eseguire **ADSI Edit** (adsiedit.msc) e connettersi al dominio del server del sito.  

3.  Creare il contenitore:  

    -   Espandere **Dominio** &lt;nome di dominio completo del computer\>, espandere &lt;nome distinto\>, fare clic con il pulsante destro del mouse su **CN=System**, fare clic su **Nuovo** e quindi fare clic su **Oggetto**.  

    -   Nella finestra di dialogo **Crea oggetto** , selezionare **Contenitore**, quindi fare clic su **Avanti**.  

    -   Nella casella **Valore** , digitare **System Management**, quindi fare clic su **Avanti**.  

4.  Assegnare le autorizzazioni:  

    > [!NOTE]  
    >  Se si preferisce, è possibile usare altri strumenti come lo strumento di amministrazione Utenti e computer di Active Directory (dsa.msc) per aggiungere autorizzazioni al contenitore.  

    -   Fare clic con il pulsante destro del mouse su **CN = System Management**, quindi su **Proprietà**.  

    -   Selezionare la scheda **Sicurezza**, fare clic su **Aggiungi**, quindi aggiungere l'account computer del server del sito con l'autorizzazione  
        **Controllo completo** .  

    -   Fare clic su **Avanzate**, selezionare l'account computer del server del sito e quindi fare clic su **Modifica**.  

    -   Nell'elenco **Applica a** , selezionare **Questo oggetto e tutti i discendenti**.  

5.  Fare clic su **OK** per chiudere la console e salvare la configurazione.  

## <a name="step-3-configure-sites-to-publish-to-active-directory-domain-services"></a>Passaggio 3. Configurare i siti per la pubblicazione in Servizi di dominio Active Directory  
 Dopo avere configurato il contenitore, avere ottenuto le autorizzazioni e avere installato un sito primario di Configuration Manager, è possibile configurare il sito per la pubblicazione di dati in Active Directory.  

 Per informazioni sulla pubblicazione, vedere [Publish site data for System Center Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md).  



<!--HONumber=Nov16_HO1-->


