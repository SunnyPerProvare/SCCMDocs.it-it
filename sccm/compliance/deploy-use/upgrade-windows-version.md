---
title: Aggiornare i dispositivi Windows a una versione diversa
titleSuffix: Configuration Manager
description: Aggiornare automaticamente i dispositivi che eseguono Windows 10 Desktop o Windows 10 Mobile a un'edizione differente con Configuration Manager.
ms.date: 01/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3cda70e7a5f1b2cf7dec079a7e933af48f0bf8ad
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128399"
---
# <a name="upgrade-windows-devices-with-the-edition-upgrade-policy-in-system-center-configuration-manager"></a>Aggiornare i dispositivi Windows con i criteri di aggiornamento edizione in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


I **criteri di aggiornamento edizione** consentono di aggiornare automaticamente i dispositivi che eseguono una delle versioni seguenti di Windows 10 a un'edizione diversa:

- Windows 10 Desktop
- Windows 10 Mobile

Sono supportati i percorsi di aggiornamento seguenti:

- Da Windows 10 Pro a Windows 10 Enterprise
- Da Windows 10 Home a Windows 10 Education
- Da Windows 10 Mobile a Windows 10 Mobile Enterprise

I dispositivi devono essere registrati in Microsoft Intune o eseguire il software client di Configuration Manager. Questo criterio non è attualmente compatibile con i PC gestiti mediante MDM locale.

## <a name="before-you-start"></a>Prima di iniziare  
 Prima di iniziare l'aggiornamento dei dispositivi alla versione più recente, esaminare i prerequisiti seguenti:  

-   Per le edizioni Desktop di Windows 10: un codice Product Key valido per la nuova versione di Windows in tutti i dispositivi a cui sono destinati i criteri. Questo codice Product Key può essere un codice ad attivazione multipla (MAK) o un codice generico di contratti multilicenza (GVLK). Un codice GVLK è anche definito codice di configurazione client del servizio di gestione delle chiavi (KMS). Per altre informazioni, vedere [Pianificare l'attivazione dei contratti multilicenza](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Per un elenco di codici di configurazione client KMS, vedere l'[Appendice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) della Guida di attivazione di Windows Server. <!--496871-->  

-   Per Windows 10 Mobile: un file di licenza XML del Centro servizi per contratti multilicenza (VLSC). Questo file contiene le informazioni sulle licenze per la nuova versione di Windows in tutti i dispositivi a cui sono destinati i criteri.

- Per gestire questo tipo di criteri, è necessario essere nel ruolo di sicurezza **Amministratore completo** di Configuration Manager.

## <a name="configure-the-edition-upgrade-policy"></a>Configurare i criteri di aggiornamento edizione  

1.  Nella console di Configuration Manager fare clic su **Assets e conformità** > **Impostazioni di conformità** > **Aggiornamento edizione di Windows 10**.  

3.  Nel gruppo **Crea** della scheda **Home** fare clic su **Crea criteri aggiornamento edizione**.  

4.  Fare clic su **Crea criterio**.  

5.  Nella pagina **Generale** della **Creazione guidata criteri aggiornamento edizione**specificare le informazioni seguenti:  

    -   **Nome** - Immettere un nome per i criteri di aggiornamento edizione  

    -   **Descrizione** (facoltativo) - Immettere facoltativamente una descrizione per i criteri che consenta di identificarli nella console di Intune  

    -   **SKU per aggiornare il dispositivo a** - Nell'elenco a discesa selezionare l'edizione di destinazione di Windows 10 Desktop o Windows 10 Mobile  

    -   **Informazioni di licenza** - Selezionare una delle opzioni seguenti:  

        -   **Codice Product Key** -Immettere un codice Product Key valido per l'edizione Windows 10 Desktop di destinazione  

            > [!NOTE]  
            >  Dopo aver creato criteri che contengono un codice Product Key, non è possibile modificare il codice Product Key in un secondo momento, Configuration Manager nasconde il codice per motivi di sicurezza. Per modificare il codice Product Key, è necessario immettere nuovamente l'intero codice.  

        -   **File di licenza** -Fare clic su **Sfoglia** per selezionare un file di licenza valido in formato XML. Configuration Manager usa questo file di licenza per aggiornare i dispositivi Windows 10 Mobile.  

6.  Completare la procedura guidata.  


## <a name="deploy-the-edition-upgrade-policy"></a>Distribuire i criteri di aggiornamento edizione  

1.  Nella console di Configuration Manager fare clic su **Assets e conformità** > **Impostazioni di conformità** > **Aggiornamento edizione di Windows 10**.  

3.  Selezionare i criteri di aggiornamento edizione Windows 10 da distribuire e quindi nel gruppo **Distribuzione** della scheda **Home** fare clic su **Distribuisci**.  

4.  Nella finestra di dialogo **Distribuisci criterio di aggiornamento edizione di Windows 10** scegliere prima la raccolta in cui si vuole distribuire il criterio. Selezionare la pianificazione in base alla quale il client valuta i criteri e quindi fare clic su **OK**. Per i PC gestiti con il client di Configuration Manager, è necessario distribuire i criteri a una raccolta di dispositivi. Per i PC registrati con Intune, è possibile distribuire i criteri a una raccolta di utenti o di dispositivi. 



## <a name="next-steps"></a>Passaggi successivi

Monitorare la distribuzione dal nodo **Distribuzioni** dell'area di lavoro **Monitoraggio**. Se vengono visualizzati errori che indicano che la distribuzione non è riuscita, ad esempio:
- **Non applicabile per questo dispositivo**
- **Conversione tipo di dati non riuscita**

Questi errori non indicano che la distribuzione non è riuscita. Verificare nel PC di destinazione che l'aggiornamento sia stato completato correttamente.

Dopo che il client ha valutato i criteri di destinazione, verrà riavviato entro due ore per applicare l'aggiornamento. Informare tutti gli utenti interessati dalla distribuzione dei criteri o pianificare la distribuzione dei criteri in ore non lavorative.

Se viene visualizzato l'errore seguente in **DcmWmiProvider.log** nel client, verificare di usare il codice corretto per lo scenario di attivazione. Per altre informazioni, vedere la sezione [Prima di iniziare](#before-you-start). Se si usa un servizio di gestione delle chiavi per l'attivazione, assicurarsi di usare un [codice di configurazione client KMS](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys).  <!-- 496871 -->   

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`
