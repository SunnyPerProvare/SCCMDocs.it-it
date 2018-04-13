---
title: Panoramica dei certificati CNG
titleSuffix: Configuration Manager
description: Informazioni sul supporto dei certificati Cryptography Next Generation (CNG) per i clienti e i server Configuration Manager.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ''
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 271cc0e2753f1a65740187a4faf6875c1a018014
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2018
---
# <a name="cng-certificates-overview"></a>Panoramica dei certificati CNG
<!-- 1356191 --> 

Configuration Manager offre supporto limitato per la crittografia, ovvero solo per certificati CNG. I client di Configuration Manager possono usare certificati di autenticazione client con chiave privata nel provider di archiviazione chiavi (KSP) CNG. Con il supporto per i provider di archiviazione chiavi, i client di Configuration Manager supportano chiavi private basate sull'hardware, ad esempio TPM KSP per i certificati di autenticazione client PKI.

## <a name="supported-scenarios"></a>Scenari supportati
È possibile usare i modelli di certificato dell'[API di crittografia CNG (Cryptography Next Generation)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) per gli scenari seguenti:

- Registrazione e comunicazione dei client con un punto di gestione HTTPS   
- Distribuzione di software e applicazioni con un punto di distribuzione HTTPS   
- Distribuzione del sistema operativo  
- Client messaging SDK (con l'aggiornamento più recente) e proxy ISV   
- Configurazione di Cloud Management Gateway  

A partire dalla versione 1802, è possibile usare i certificati CNG per i ruoli del server abilitati per HTTPS seguenti: <!-- 1357314 -->   
- Punto di gestione
- Punto di distribuzione
- Punto di aggiornamento software
- Punto di migrazione stato     

> [!NOTE]
> CNG è compatibile con le versioni precedenti di Crypto API (CAPI). I certificati CAPI continuano a essere supportati anche quando nel client è abilitato il supporto per CNG.

## <a name="unsupported-scenarios"></a>Scenari non supportati

Attualmente non sono supportati gli scenari seguenti:

- I ruoli del server seguenti non sono operativi se installati in modalità HTTPS con un certificato CNG associato al sito Web in Internet Information Services (IIS): 
    - Servizio Web del Catalogo applicazioni
    - Sito Web del Catalogo applicazioni
    - Punto di registrazione  
    - Punto proxy di registrazione  

- Software Center non visualizza come disponibili le applicazioni e i pacchetti distribuiti in raccolte di utenti o di gruppi di utenti.

- Uso di certificati CNG per creare un punto di distribuzione cloud.

- Se il modulo criteri NDES usa un certificato CNG per l'autenticazione client, la comunicazione con il punto di registrazione certificati non riesce.

- Se si specifica un certificato CNG durante la creazione dei supporti della sequenza di attività, la procedura guidata non riesce a creare supporti di avvio.

## <a name="to-use-cng-certificates"></a>Per usare certificati CNG

Per usare i certificati CNG, l'autorità di certificazione (CA) deve fornire i modelli di certificato CNG per i computer di destinazione. I dettagli dei modelli variano in base allo scenario. Le proprietà seguenti, tuttavia, sono obbligatorie:

- Scheda **Compatibilità**

    - L'**autorità di certificazione** deve essere Windows Server 2008 o versione successiva. È consigliabile usare Windows Server 2012.

    - Il **destinatario del certificato** deve essere Windows Vista/Windows Server 2008 o versione successiva. È consigliabile usare Windows 8/Windows Server 2012.

- Scheda **Crittografia**

    - **Categoria provider** deve corrispondere a **Provider di archiviazione chiavi**. (obbligatorio).

> [!NOTE]
> I requisiti per l'ambiente o l'organizzazione possono essere diversi. Contattare l'esperto di PKI. L'aspetto importante da considerare è che un modello di certificato deve usare un provider di archiviazione chiavi per trarre vantaggio da CNG.

Per ottenere risultati ottimali, è consigliabile creare il nome soggetto da informazioni di Active Directory. Usare il nome DNS per **Formato del nome soggetto** e includere il nome DNS nel nome soggetto alternativo. In caso contrario, è necessario fornire queste informazioni durante la registrazione del dispositivo nel profilo del certificato.