---
title: Ottenere informazioni
titleSuffix: Configuration Manager
description: Trovare risorse per altre informazioni su Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e6be541a1b26961684f0577f2540132b81f50b7a
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385474"
---
# <a name="find-help-for-using-configuration-manager"></a>Reperire informazioni sull'uso di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo include le sezioni seguenti con diverse risorse per reperire informazioni sull'uso di Configuration Manager:  

- [Documentazione del prodotto](#bkmk_Info)  

- [Condivisione di commenti e suggerimenti sul prodotto](#product-feedback)  

- [Seguire il blog del team di Configuration Manager](#BKMK_ProductGroupBlog)  

- [Opzioni di supporto e risorse per la community](#BKMK_SupportOptions)  

Per informazioni sull'accessibilità, vedere [Funzionalità di accessibilità](/sccm/core/understand/accessibility-features).  



##  <a name="bkmk_Info"></a> Documentazione del prodotto  

Per accedere alla documentazione più recente del prodotto, iniziare dall'[indice](https://docs.microsoft.com/sccm/).  

<a name="BKMK_SearchTips"></a>  

Per suggerimenti sulle ricerche, l'invio di commenti e suggerimenti e altre informazioni sull'uso della documentazione del prodotto, vedere [Come usare la documentazione](/sccm/core/understand/use-docs).  



<a name="product-feedback"></a>  

## <a name="BKMK_1806Feedback"></a> Commenti e suggerimenti sul prodotto a partire dalla versione 1806

A partire da Configuration Manager versione 1806, è possibile inviare commenti e suggerimenti sul prodotto direttamente dalla console. Se è necessario allegare log, usare [Hub di Feedback](#BKMK_FeedbackHub). È possibile eseguire le operazioni seguenti. <!--1357542-->

  - **Invia smile**: inviare commenti e suggerimenti su ciò che si è apprezzato.
  - **Invia faccia imbronciata**: inviare commenti e suggerimenti su ciò che non si è apprezzato.
  - **Invia un suggerimento**: consente di accedere al [sito Web UserVoice](https://configurationmanager.uservoice.com/) per condividere la propria opinione.

![Inviare commenti e suggerimenti in Configuration Manager 1806](media/1806-send-a-smile.png)


### <a name="send-a-smile"></a>Inviare uno smile

Per inviare commenti e suggerimenti su elementi che si sono apprezzati, seguire queste istruzioni: 
1. Nell'angolo superiore destro della console fare clic sullo smile. 
2. Nel menu a discesa selezionare **Invia smile**.
3. Usare la casella di testo per illustrare ciò che si è apprezzato. 
4. Scegliere se si vuole condividere il proprio indirizzo di posta elettronica e uno screenshot. 
5. Fare clic su **Invia commenti e suggerimenti**.
     - Se non è disponibile una connessione Internet, fare clic su **Salva** in basso. Per l'invio a Microsoft, seguire le istruzioni riportate nella sezione [Inviare in seguito commenti e suggerimenti salvati a tale scopo](#BKMK_NoInternet). 

![Modulo per l'invio di commenti e suggerimenti in Configuration Manager 1806](media/1806-feedback-form.png)


### <a name="send-a-frown"></a>Inviare una faccia imbronciata

Per inviare commenti e suggerimenti su elementi che non si sono apprezzati, seguire queste istruzioni:

1. Nell'angolo superiore destro della console fare clic sullo smile. 
2. Nel menu a discesa selezionare **Invia faccia imbronciata**.
3. Usare la casella di testo per illustrare ciò che non si è apprezzato. 
4. Scegliere se si vuole condividere il proprio indirizzo di posta elettronica e uno screenshot. 
5. Fare clic su **Invia commenti e suggerimenti**.
     - Se non è disponibile una connessione Internet, fare clic su **Salva** in basso. Per l'invio a Microsoft, seguire le istruzioni riportate nella sezione [Inviare in seguito commenti e suggerimenti salvati a tale scopo](#BKMK_NoInternet).  


### <a name="information-sent-with-feedback"></a>Informazioni inviate con commenti e suggerimenti
 
   - Informazioni sulla build del sistema operativo
   - ID della gerarchia di Configuration Manager
   - Informazioni sulla build del prodotto
   - Informazioni sulla lingua
   - Identificatore del dispositivo 
       - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQMClient:MachineId


### <a name="BKMK_NoInternet"></a> Inviare in seguito commenti e suggerimenti salvati a tale scopo

1. Fare clic su **Salva** nella parte inferiore della finestra **Commenti e suggerimenti**. 
2. Salvare il file ZIP. Se il computer locale non ha accesso a Internet, copiare il file in un computer connesso a Internet. 
3. Se necessario, copiare UploadOfflineFeedback.exe, disponibile in `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe`
    - Per altre informazioni sulla cartella CD.Latest, vedere [Cartella CD.Latest](../servers/manage/the-cd.latest-folder.md)

4. In un computer connesso a Internet aprire il prompt dei comandi. 
5. Eseguire il comando seguente: `UploadOfflineFeedback.exe -f c:\folder\location_of.zip`
    
    - Facoltativamente, è possibile specificare quanto segue.
        -  `-t, --timeout`: timeout in secondi per l'invio dei dati. 0 corrisponde a senza limiti. Il valore predefinito è 30.
        - `-s --silent`: nessuna registrazione nella console (non è combinabile con --verbose)
        - `-v, --verbose`: registrazione dettagliata dell'output nella console (non è combinabile con --silent)
        - `--help`: visualizza la schermata della Guida



##  <a name="BKMK_FeedbackHub"></a> Commenti e suggerimenti sul prodotto per la versione 1802 e precedenti

Per segnalare errori del prodotto potenziali è possibile usare l'[app Hub di Feedback](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) incorporata in Windows 10. Quando si sceglie **Aggiungi nuovo feedback**, assicurarsi di selezionare la categoria **Enterprise Management** e di scegliere una delle sottocategorie seguenti:
 - Configuration Manager Client
 - Console di Configuration Manager
 - Distribuzione del sistema operativo di Configuration Manager
 - Server di Configuration Manager

Continuare a usare la [pagina UserVoice](https://configurationmanager.uservoice.com/) per votare nuove idee per le funzionalità di Configuration Manager.


##  <a name="BKMK_ProductGroupBlog"></a> Blog del team di Configuration Manager  

I team di progettazione e i team associati di Configuration Manager usano il blog [Enterprise Mobility + Security](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager) per offrire informazioni tecniche e altre notizie su Configuration Manager e le relative tecnologie. I post di questo blog integrano le informazioni di supporto e la documentazione relativa al prodotto.  


##  <a name="BKMK_SupportOptions"></a> Opzioni di supporto e risorse per la community  

I seguenti collegamenti forniscono informazioni sulle opzioni di supporto e sulle risorse per la community:  

-   [Supporto tecnico Microsoft](https://aka.ms/cmcbsupport)  

-   [Community di Configuration Manager: System Center Configuration Manager (Current Branch) Survival Guide](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx ) (Guida essenziale di System Center Configuration Manager Current Branch)  

-   [Pagina dei forum di Configuration Manager](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->