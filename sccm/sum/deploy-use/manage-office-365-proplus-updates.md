---

title: Gestire gli aggiornamenti di Office 365 ProPlus | Configuration Manager
description: Configuration Manager sincronizza gli aggiornamenti del client di Office 365 dal catalogo di Windows Server Update Services nel server del sito per rendere disponibili gli aggiornamenti per la distribuzione ai client.
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 58a551425591332264592713fa3cc4e04d9939aa


---

# <a name="manage-office-365-proplus-updates-with-configuration-manager"></a>Gestire gli aggiornamenti di Office 365 ProPlus con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

A partire dalla versione 1602, Configuration Manager consente di gestire gli aggiornamenti del client di Office 365 usando il flusso di lavoro Gestione aggiornamenti software. Quando pubblica un nuovo aggiornamento del client di Office 365 nella rete per la distribuzione di contenuti (CDN) di Office, Microsoft pubblica anche un pacchetto di aggiornamento per Windows Server Update Services (WSUS). Dopo che Configuration Manager ha sincronizzato l'aggiornamento del client di Office 365 dal catalogo di Windows Server Update Services nel server del sito, l'aggiornamento è disponibile per la distribuzione ai client.

#### <a name="to-deploy-office-365-updates-with-configuration-manager"></a>Per distribuire gli aggiornamenti di Office 365 con Configuration Manager
Eseguire i passaggi seguenti per distribuire gli aggiornamenti di Office 365 con Configuration Manager:

1.  [Verificare i requisiti](https://technet.microsoft.com/library/mt628083.aspx) per l'uso di Configuration Manager per la gestione degli aggiornamenti del client di Office 365 nella sezione **Requisiti necessari per gestire gli aggiornamenti client di Office 365 utilizzando Configuration Manager** dell'argomento.  

2.  [Configurare i punti di aggiornamento software](../get-started/configure-classifications-and-products.md) per sincronizzare gli aggiornamenti del client di Office 365. Impostare gli **aggiornamenti** per la classificazione e selezionare il **client di Office 365** per il prodotto. Potrebbe essere necessario sincronizzare gli aggiornamenti software almeno una volta prima che il client di Office 365 sia disponibile per la selezione. È necessario sincronizzare gli aggiornamenti software dopo aver configurato i punti di aggiornamento software per l'uso della classificazione **Aggiornamenti**.  

3.  Abilitare i client di Office 365 per la ricezione di aggiornamenti da Configuration Manager. È possibile eseguire questa operazione usando le impostazioni client di Configuration Manager o i criteri di gruppo. Per abilitare il client usare uno dei metodi seguenti:  
    - Metodo 1: a partire dalla versione 1606 di Configuration Manager è possibile usare l'impostazione client di Configuration Manager per gestire l'agente client di Office 365. Dopo aver configurato questa impostazione e distribuito gli aggiornamenti di Office 365, l'agente client di Configuration Manager comunica con l'agente client di Office 365 al fine di scaricare gli aggiornamenti di Office 365 da un punto di distribuzione e installarli. Configuration Manager esegue l'inventario delle impostazioni client di Office 365 ProPlus.
      1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Panoramica** > **Impostazioni client**.  

      2.  Aprire le impostazioni del dispositivo appropriato per abilitare l'agente client. Per altre informazioni sulle impostazioni client predefinite e personalizzate, vedere [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) (Come configurare le impostazioni client in System Center Configuration Manager).  

      3.  Fare clic su **Aggiornamenti software** e selezionare **Sì** per l'impostazione **Abilita la gestione dell'agente client di Office 365**.  

    - Metodo 2: [Abilitare i client di Office 365 per la ricezione di aggiornamenti](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient) da Configuration Manager usando lo strumento di distribuzione di Office o i criteri di gruppo.  

4. [Distribuire gli aggiornamenti di Office 365](deploy-software-updates.md) ai client.  



<!--HONumber=Nov16_HO1-->


