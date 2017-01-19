---
title: Concetti base sull&quot;amministrazione basata su ruoli | Microsoft Docs
description: L&quot;amministrazione basata sui ruoli consente di controllare l&quot;accesso amministrativo a Configuration Manager e agli oggetti gestiti.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0a2d6c3f-a4e4-4c19-b087-3caada480de9
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6cf3ac76ea3fb9c9b093ed4927255102930bbe26
ms.openlocfilehash: 5bdfe43c86d5b700c50b4d55d2f3bbb15bb504e9


---
# <a name="fundamentals-of-role-based-administration-for-system-center-configuration-manager"></a>Nozioni fondamentali di amministrazione basata su ruoli per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager l'amministrazione basata su ruoli consente di proteggere l'accesso all'amministrazione di Configuration Manager e agli oggetti gestiti, come raccolte, distribuzioni e siti.   Dopo aver compreso i concetti introdotti in questo argomento è possibile [configurare l'amministrazione basata su ruoli per System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

 Questo modello di amministrazione basata su ruoli definisce e gestisce centralmente le impostazioni di accesso di protezione a livello di gerarchia per tutti i siti e le impostazioni del sito usando quanto segue:  

-   I**ruoli di sicurezza** , che vengono assegnati agli utenti (o a gruppi di utenti) amministratori per fornire loro le autorizzazioni per diversi oggetti di Configuration Manager, ad esempio le autorizzazioni per la creazione o la modifica delle impostazioni client.  

-   Gli**ambiti di protezione** , che raggruppano istanze specifiche di oggetti che un utente amministratore ha la responsabilità di gestire, ad esempio, un'applicazione che consente di installare Microsoft Office 2010.  

-   Le**raccolte** , cioè il modo in cui si specificano i gruppi di utenti e le risorse dispositivi che l'utente amministratore può gestire.  

 La combinazione di ruoli di protezione, ambiti di protezione e raccolte consente di segregare le assegnazioni amministrative che soddisfano i requisiti aziendali e definire l'ambito amministrativo di un utente, ovvero che cosa può visualizzare e gestire l'utente nella distribuzione di Configuration Manager.  

**L'amministrazione basata su ruoli offre i seguenti vantaggi:**  

-   I siti non vengono usati come limiti amministrativi  

-   È possibile creare gli utenti amministratori per una gerarchia ed è necessario assegnare loro la protezione una sola volta.  

-   Tutte le assegnazioni di protezione vengono replicate e rese disponibili in tutta la gerarchia  

-   Ci sono diversi ruoli di sicurezza incorporati da assegnare alle tipiche attività amministrative. È possibile creare ruoli di sicurezza personalizzati per soddisfare particolari esigenze aziendali  

-   Gli utenti amministratori vedono solo gli oggetti per cui hanno le autorizzazioni di gestione  

-   È possibile controllare le azioni di protezione amministrativa.  

Quando si progetta e implementa la protezione amministrativa per Configuration Manager seguire questa procedura per creare un **ambito amministrativo** per un utente amministratore:  

-   [ruoli di sicurezza](#bkmk_Planroles)  

-   [raccolte](#bkmk_planCol)  

-   [ambiti di protezione](#bkmk_PlanScope)  

 L'ambito amministrativo controlla gli oggetti che un utente amministratore può visualizzare nella console di Configuration Manager e le autorizzazioni dell'utente per tali oggetti. Le configurazione dell'amministrazione basata su ruoli vengono replicate in ogni sito della gerarchia come dati globali e quindi vengono applicate a tutte le connessioni amministrative.  

> [!IMPORTANT]  
>  I ritardi di replica tra siti possono impedire a un sito di ricevere modifiche per l'amministrazione basata su ruoli. Per informazioni sul monitoraggio della replica del database tra siti, vedere l'argomento [Trasferimenti di dati tra siti in System Center Configuration Manager](../../core/servers/manage/data-transfers-between-sites.md).  

##  <a name="a-namebkmkplanrolesa-security-roles"></a><a name="bkmk_Planroles"></a> ruoli di sicurezza  
 Usare i ruoli di sicurezza per concedere le autorizzazioni di sicurezza a utenti amministratori. I ruoli di sicurezza sono gruppi di autorizzazioni di sicurezza assegnate agli utenti amministratori in modo che possano eseguire le relative attività amministrative. Le autorizzazioni di sicurezza definiscono le azioni amministrative che un utente amministratore può eseguire e le autorizzazioni concesse per determinati tipi di oggetto. Come procedura consigliata di sicurezza, assegnare i ruoli di sicurezza che forniscono i privilegi minimi.  

 In Configuration Manager sono incorporati diversi ruoli di sicurezza per supportare i raggruppamenti tipici di attività amministrative. È possibile creare ruoli di sicurezza personalizzati per soddisfare particolari esigenze aziendali. Esempi di ruoli di sicurezza incorporati:  

-   **Amministratore completo**: questo ruolo di sicurezza concede tutte le autorizzazioni in Configuration Manager.  

-   **Analista asset**: questo ruolo di sicurezza consente agli utenti amministratori di visualizzare i dati raccolti con Asset Intelligence, l'inventario software, l'inventario hardware e la misurazione del software. Gli utenti amministratori possono creare regole di controllo software ed etichette, famiglie e categorie di Asset Intelligence.  

-   **Amministratore aggiornamento software**: questo ruolo di sicurezza concede le autorizzazioni per definire e distribuire gli aggiornamenti software. Gli utenti amministratori associati a questo ruolo possono creare raccolte, gruppi di aggiornamento software, distribuzioni e modelli e attivare gli aggiornamenti software per la funzionalità Protezione accesso alla rete (NAP).  

> [!TIP]  
>  È possibile visualizzare l'elenco di ruoli di sicurezza incorporati e i ruoli di sicurezza personalizzati creati, incluse le descrizioni, nella console di Configuration Manager. A tale scopo, nell'area di lavoro **Amministrazione** espandere **Sicurezza**e selezionare **Ruoli di protezione**.  

 Ogni ruolo di sicurezza dispone di autorizzazioni specifiche per diversi tipi di oggetto. Ad esempio, il ruolo di sicurezza **Application MMM** (MMM applicazione) ha le autorizzazioni seguenti per le applicazioni: **Approva**, **Crea**, **Elimina**, **Modifica**, **Modifica cartella**, **Sposta oggetto**, **Read/Deploy** (Leggi/Distribuisci), **Imposta ambito di protezione**. Non è possibile modificare le autorizzazioni per i ruoli di sicurezza incorporati, ma è possibile copiare il ruolo, apportare modifiche e quindi salvare tali modifiche come un nuovo ruolo di sicurezza personalizzato. È inoltre possibile importare ruoli di sicurezza esportati da un'altra gerarchia (ad esempio da una rete di prova). Esaminare i ruoli di sicurezza e le relative autorizzazioni per stabilire se usare i ruoli di sicurezza incorporati o se sia necessario crearne di personalizzati.  

 **Usare i seguenti passaggi per la pianificazione dei ruoli di sicurezza:**  

1.  Identificare le attività eseguite dagli utenti amministratori in Configuration Manager. Queste attività possono far riferimento a uno o più gruppi di attività di gestione, ad esempio distribuzione di pacchetti e applicazioni, distribuzione di sistemi operativi e impostazioni di conformità, configurazione di siti e protezione, controllo, computer con controllo remoto e raccolta di dati di inventario.  

2.  Eseguire il mapping di queste attività amministrative in uno o più ruoli di sicurezza incorporati.  

3.  Se alcuni utenti amministratori eseguono le attività di più ruoli di sicurezza, assegnare più ruoli di sicurezza a tali utenti amministratori invece di creare un nuovo ruolo di sicurezza che combini queste attività.  

4.  Se le attività identificate non eseguono il mapping ai ruoli di sicurezza incorporati, creare e testare nuovi ruoli di sicurezza.  

Per informazioni su come creare e configurare i ruoli di sicurezza per l'amministrazione basata su ruoli, vedere le sezioni relative alla [creazione di ruoli di sicurezza personalizzati](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole) e alla [configurazione dei ruoli di sicurezza](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole) nell'argomento [Configure role-based administration for System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md) (Configurare l'amministrazione basata su ruoli per System Center Configuration Manager).  

##  <a name="a-namebkmkplancola-collections"></a><a name="bkmk_planCol"></a> raccolte  
 Le raccolte specificano utente e risorse del computer che un utente amministratore può visualizzare o gestire. Ad esempio, per poter distribuire applicazioni o eseguire il controllo remoto, agli utenti amministratori deve essere assegnato un ruolo di sicurezza che consente l'accesso a una raccolta che include queste risorse. È possibile selezionare raccolte di utenti o dispositivi.  

 Per altre informazioni sulle raccolte, vedere [Introduzione alle raccolte in System Center Configuration Manager](../../core/clients/manage/collections/introduction-to-collections.md).  

 Prima di configurare l'amministrazione basata su ruoli, verificare se è necessario creare nuove raccolte per uno dei seguenti motivi:  

-   Organizzazione funzionale. Ad esempio, separare raccolte di server e workstation.  

-   Allineamento geografica. Ad esempio, separare raccolte per il Nord America e l' Europa.  

-   Requisiti di protezione e processi aziendali. Ad esempio, separare raccolte per produzione e computer di prova.  

-   Allineamento dell'organizzazione. Ad esempio, separare le raccolte per ogni Business Unit.  

Per informazioni su come configurare raccolte per l'amministrazione basata su ruoli, vedere la sezione relativa alla [configurazione di raccolte per la gestione della sicurezza](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl) nell'argomento [Configure role-based administration for System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md) (Configurare l'amministrazione basata su ruoli per System Center Configuration Manager).  

##  <a name="a-namebkmkplanscopea-security-scopes"></a><a name="bkmk_PlanScope"></a> ambiti di protezione  
 Usare gli ambiti di protezione per fornire agli utenti amministratori l'accesso a oggetti a protezione diretta. Gli ambiti di protezione sono una raccolta denominata di oggetti a protezione diretta che vengono assegnati agli utenti amministratori come gruppo. Tutti gli oggetti a protezione diretta devono essere assegnati a uno o più ambiti di protezione. Configuration Manager ha due ambiti di protezione predefiniti:  

-   **Tutto**: questo ambito di protezione incorporato consente l'accesso a tutti gli ambiti. Non è possibile assegnare gli oggetti a questo ambito di protezione.  

-   **Predefinito**: per impostazione predefinita, questo ambito di protezione incorporato viene usato per tutti gli oggetti. Quando si installa Configuration Manager per la prima volta, tutti gli oggetti vengono assegnati a questo ambito di protezione.  

Se si desidera limitare gli oggetti che gli utenti amministratori possono visualizzare e gestire, è necessario creare ed usare scopi di protezione personalizzati. Gli ambiti di protezione non supportano una struttura gerarchica e non possono essere nidificati. Gli ambiti di protezione possono contenere uno o più tipi di oggetto, tra cui:  

-   Sottoscrizioni di avvisi  

-   Applicazioni  

-   Immagini d'avvio  

-   Gruppi di limiti  

-   Elementi di configurazione  

-   Impostazioni client personalizzate  

-   Punti di distribuzione e gruppi di punti di distribuzione  

-   Pacchetti driver  

-   Condizioni globali  

-   Processi di migrazione  

-   Immagini del sistema operativo  

-   Pacchetti di installazione del sistema operativo  

-   Pacchetti  

-   Query  

-   Siti  

-   Regole di controllo software  

-   Gruppi di aggiornamenti software  

-   Pacchetti di aggiornamenti software  

-   Pacchetti di sequenze attività  

-   Pacchetti e elementi di impostazioni del dispositivo Windows CE  

Esistono inoltre alcuni oggetti che non è possibile includere negli ambiti di protezione poiché sono protetti solo dai ruoli di sicurezza. Il relativo accesso amministrativo non può essere limitato a un sottoinsieme degli oggetti disponibili. Ad esempio, potrebbe essere presente un utente amministratore che crea gruppi di limiti usati per un sito specifico. Poiché l'oggetto limite non supporta agli ambiti di protezione, non è possibile assegnare a questo utente un ambito di protezione che consente l'accesso solo ai limiti che potrebbero essere associati a tale sito. Poiché un oggetto limite non può essere associato a un ambito di protezione, quando si assegna a un utente un ruolo di sicurezza che include l'accesso a oggetti limite tale utente può accedere a ogni limite presente nella gerarchia.  

Tra gli oggetti non limitati dagli ambiti di protezione sono inclusi i seguenti:  

-   Foreste Active Directory  

-   Utenti amministratori  

-   Avvisi  

-   Criteri antimalware  

-   Limiti  

-   Associazioni di computer  

-   Impostazioni client predefinite  

-   Modelli di distribuzione  

-   Driver di dispositivo  

-   Connettore Exchange Server  

-   Mapping di migrazione da sito a sito  

-   Profili di registrazione dispositivo mobile  

-   Ruoli di sicurezza  

-   ambiti di protezione  

-   Indirizzi di siti  

-   Ruoli del sistema del sito  

-   Titoli software  

-   Aggiornamenti software  

-   Messaggi di stato  

-   Affinità utente dispositivo  

Creare ambiti di protezione quando è necessario limitare l'accesso per separare le istanze di oggetti. Ad esempio:  

-   Si dispone di un gruppo di utenti amministratori che deve essere in grado di visualizzare applicazioni di produzione e applicazioni di prova. Creare un ambito di protezione per le applicazioni di produzione e un altro per le applicazioni di prova.  

-   Diversi utenti amministratori richiedono un accesso diverso ad alcune istanze di un tipo di oggetto. Ad esempio, un gruppo di utenti amministratori richiede l'autorizzazione **Lettura** per gruppi di aggiornamenti software specifici e un altro gruppo di utenti amministratori richiede le autorizzazioni **Modifica** e **Elimina** per altri gruppi di aggiornamento software. Creare ambiti di protezione diversi per questi gruppi di aggiornamento software.  

Per informazioni su come configurare gli ambiti di protezione per l'amministrazione basata su ruoli, vedere la sezione relativa alla [configurazione degli ambiti di protezione per un oggetto](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope) nell'argomento [Configure role-based administration for System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md) (Configurare l'amministrazione basata su ruoli per System Center Configuration Manager).  



<!--HONumber=Dec16_HO3-->


