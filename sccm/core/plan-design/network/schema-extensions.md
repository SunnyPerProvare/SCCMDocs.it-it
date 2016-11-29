---
title: Estensioni dello schema | System Center Configuration Manager
description: Estendere lo schema di Active Directory per supportare System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95c13c00-909f-4fbb-bbaa-1eba9d54d8c5
caps.latest.revision: 8
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f8c8533da62d215ed22f5235eefa687d5df41394


---
# <a name="schema-extensions-for-system-center-configuration-manager"></a>Estensioni dello schema per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile estendere lo schema di Active Directory per supportare Configuration Manager. In questo modo si modifica lo schema di Active Directory di una foresta per aggiungere un nuovo contenitore e vari attributi usati dai siti di Configuration Manager per pubblicare informazioni importanti in Active Directory accessibili in modo sicuro.  Queste informazioni possono semplificare la distribuzione e la configurazione dei client e consentono loro di trovare facilmente risorse del sito come server con contenuto distribuito o che forniscono vari servizi ai client.  

-   L'estensione dello schema di Active Directory non è necessaria, ma è consigliata.  

Prima di [estendere lo schema di Active Directory](https://msdnstage.redmond.corp.microsoft.com/en-US/library/mt345589\(TechNet.10\).aspx)occorre acquisire familiarità con Servizi di dominio Active Directory e la [modifica dello schema di Active Directory](https://technet.microsoft.com/library/cc759402\(v=ws.10\).aspx).  

## <a name="considerations-for-extending-the-active-directory-schema-for-configuration-manager"></a>Considerazioni per l'estensione dello Schema di Active Directory per Configuration Manager  

-   Le estensioni dello schema di Active Directory per System Center Configuration Manager sono identiche a quelle usate da Configuration Manager 2007 e Configuration Manager 2012. Se in precedenza si è esteso lo schema per una di queste versioni, non è necessario estendere nuovamente lo schema.  

-   L'estensione dello schema di Active Directory è un'azione irreversibile a livello di foresta, che può essere eseguita solo una volta.  

-   L'estensione dello schema deve essere eseguita da un utente membro del gruppo Schema Admins o che abbia le autorizzazioni sufficienti per modificare lo schema.  

-   Nonostante sia possibile estendere lo schema sia prima che dopo l'installazione di Configuration Manager, è consigliabile farlo prima di iniziare la configurazione dei siti e delle impostazioni di gerarchia.  Questo semplificherà molte delle procedure di configurazione successive.  

-   Dopo l'estensione dello schema, il catalogo globale di Active Directory viene replicato in tutta la foresta. Di conseguenze, pianificare l'estensione dello schema in un momento in cui il traffico di replica non possa influire negativamente sugli altri processi dipendenti dalla rete.  

    -   Nelle foreste Windows 2000, l'estensione dello schema causa una sincronizzazione completa dell'intero catalogo globale.  

    -   A partire dalle foreste di Windows 2003, vengono replicati solo gli attributi appena aggiunti.  

**Dispositivi e client che non usano lo schema di Active Directory:**  

-   Dispositivi mobili gestiti dal connettore Exchange Server  

-   Il client per computer Mac  

-   Il client per i server Linux e UNIX  

-   Dispositivi mobili registrati da Configuration Manager  

-   Dispositivi mobili registrati da Microsoft Intune  

-   I client legacy del dispositivo mobile  

-   I client Windows configurati solo per la gestione client Internet  

-   Client Windows rilevati da Configuration Manager in Internet  

## <a name="capabilities-that-benefit-from-extending-the-schema"></a>Funzionalità che traggono vantaggio dall'estensione dello schema  
**Installazione del computer client e assegnazione sito**: quando si installa un nuovo client in un computer Windows, il client cerca le proprietà di installazione in Active Directory Domain Services.  

-   **Soluzioni alternative:** Se non si estende lo schema, usare una delle soluzioni alternative seguenti per fornire i dettagli di configurazione necessari ai computer per l'installazione:  

    -   **Usare l'installazione push client**. Prima di usare il metodo di installazione client, assicurarsi che tutti i prerequisiti siano soddisfatti. Per altre informazioni, vedere la sezione "Dipendenze del metodo di installazione" in Prerequisiti per computer client.  

    -   **Installare manualmente i client** e specificare le proprietà di installazione client usando le proprietà della riga di comando di installazione CCMSetup. È necessario includere le seguenti operazioni:  

        -   Specificare un punto di gestione o un percorso di origine da cui il computer può scaricare i file di installazione tramite la proprietà CCMSetup **/mp:=&lt;nome computer punto di gestione\>** o **/source:&lt;percorso ai file di origine client\>** nella riga di comando CCMSetup durante l'installazione del client.  

        -   Specificare un elenco di punti di gestione iniziali che il client utilizzerà per eseguire l'assegnazione al sito e quindi scaricare i criteri client e le impostazioni del sito. A tale scopo, usare la proprietà Client.msi SMSMP di CCMSetup.  

    -   **Pubblicare il punto di gestione in DNS o WINS** e configurare i client per usare questo metodo di individuazione della posizione del servizio.  

**Configurazione della porta per la comunicazione "client a server"**: durante l'installazione, il client viene configurato con le informazioni della porta archiviate in Active Directory. Se in seguito si modifica la porta per la comunicazione tra client e server di un sito, il client può ottenere l'impostazione della nuova porta da Servizi di dominio Active Directory.  

-   **Soluzioni alternative:** Se non si estende lo schema, usare una delle soluzioni alternative seguenti per fornire ai client esistenti la configurazione della nuova porta:  

    -   **Reinstallare i client** usando opzioni che configurano la nuova porta.  

    -   **Distribuire ai client uno script personalizzato che aggiorna le informazioni sulla porta**. Se i client non possono comunicare con un sito a causa della modifica di una porta, è possibile usare Configuration Manager per distribuire lo script. È ad esempio possibile usare Criteri di gruppo.  

**Scenari di distribuzione del contenuto**: quando si crea contenuto in un sito e lo si distribuisce a un altro sito nella gerarchia, il sito ricevente deve essere in grado di verificare la firma dei dati del contenuto firmato. A tale scopo, è necessario l'accesso alla chiave pubblica del sito di origine in cui vengono creati i dati. Quando si estende lo schema di Active Directory per Configuration Manager, viene resa disponibile una chiave pubblica del sito per tutti i siti nella gerarchia.  

-   **Soluzione alternativa:** Se non si estende lo schema di Active Directory, usare lo strumento di manutenzione gerarchia, **preinst.exe**, per scambiare le informazioni sulla chiave di sicurezza tra i siti.  

     Se ad esempio si intende creare il contenuto nel sito primario e distribuirlo in un sito secondario di un sito primario diverso, è necessario estendere lo schema di Active Directory per consentire al sito secondario di ottenere la chiave pubblica per il sito primario di origine oppure usare preinst.exe per condividere direttamente le chiavi tra i due siti.  

## <a name="active-directory-attributes-and-classes"></a>Classi e attributi di Active Directory  
Quando si estende lo schema per System Center Configuration Manager, le classi e gli attributi seguenti vengono aggiunti allo schema e resi disponibili a tutti i siti di Configuration Manager nella foresta di Active Directory.  

-   Attributi:  

    -   cn=mS-SMS-Assignment-Site-Code  

    -   cn=mS-SMS-Capabilities  

    -   cn=MS-SMS-Default-MP  

    -   cn=mS-SMS-Device-Management-Point  

    -   cn=mS-SMS-Health-State  

    -   cn=MS-SMS-MP-Address  

    -   cn=MS-SMS-MP-Name  

    -   cn=MS-SMS-Ranged-IP-High  

    -   cn=MS-SMS-Ranged-IP-Low  

    -   cn=MS-SMS-Roaming-Boundaries  
        in  

    -   cn=MS-SMS-Site-Boundaries  

    -   cn=MS-SMS-Site-Code  

    -   cn=mS-SMS-Source-Forest  

    -   cn=mS-SMS-Version  

-   Classi:  

    -   cn=MS-SMS-Management-Point  

    -   cn=MS-SMS-Roaming-Boundary-Range  

    -   cn=MS-SMS-Server-Locator-Point  

    -   cn=MS-SMS-Site  

> [!NOTE]  
>  Le estensioni dello schema possono includere attributi e classi ereditati da versioni precedenti del prodotto, ma non usati da Configuration Manager 2015. Ad esempio:  
>   
>  -   Attributo: cn=MS-SMS-Site-Boundaries  
> -   Classe: cn=MS-SMS-Server-Locator-Point  

Per assicurarsi che gli elenchi precedenti siano aggiornati, esaminare il file **ConfigMgr_ad_schema.LDF** nella cartella **\SMSSETUP\BIN\x64** del supporto di installazione di System Center Configuration Manager.  



<!--HONumber=Nov16_HO1-->

