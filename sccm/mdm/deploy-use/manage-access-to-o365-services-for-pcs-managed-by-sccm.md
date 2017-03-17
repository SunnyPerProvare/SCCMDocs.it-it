---
title: Gestire l&quot;accesso ai servizi di Office&365; per computer gestiti | Microsoft Docs
description: Informazioni su come configurare l&quot;accesso condizionale per i PC gestiti da System Center Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 34024741-edfa-4088-8599-d6bafc331e62
caps.latest.revision: 15
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: b7c55ce5629565cb1e3aede6680ef1796f56cb20
ms.lasthandoff: 03/06/2017


---
# <a name="manage-access-to-o365-services-for-pcs-managed-by-system-center-configuration-manager"></a>Gestire l'accesso ai servizi di O365 per i PC gestiti da System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*



 A partire dalla versione 1602 di Configuration Manager è possibile configurare l'accesso condizionale per i PC gestiti da System Center Configuration Manager.  

> [!IMPORTANT]  
>  Si tratta di una funzionalità di versione non definitiva disponibile negli aggiornamenti 1602, 1606 e 1610. Le funzionalità di versioni non definitive sono incluse nel prodotto a scopo di test preliminare in un ambiente di produzione, ma non devono essere considerate pronte per l'ambiente di produzione. Per altre informazioni, vedere la sezione relativa all'[abilitazione delle funzionalità facoltative dagli aggiornamenti](../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).
> - Dopo aver installato l'aggiornamento 1602, il tipo di funzionalità viene visualizzato come rilasciato anche se si tratta di una funzionalità di versione non definitiva.
> - Se si esegue l'aggiornamento dalla versione 1602 alla versione 1606, il tipo di funzionalità viene visualizzato come rilasciato anche se rimane come funzionalità di versione non definita.
> - Se si esegue l'aggiornamento dalla versione 1511 direttamente alla versione 1606, il tipo di funzionalità viene visualizzato come funzionalità di versione non definitiva.

 Per informazioni su come configurare l'accesso condizionale per i dispositivi registrati e gestiti da Intune o per i PC appartenenti a un dominio e non valutati per verificarne la conformità, vedere [Gestire l'accesso ai servizi in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md).  


## <a name="supported-services"></a>Servizi supportati  

-   Exchange Online  

-   SharePoint Online  

## <a name="supported-pcs"></a>PC supportati  

-   Windows 7  

-   Windows 8.1  

-   Per Windows 10 non è ancora disponibile il supporto completo.  Se si prova a impostare l'accesso condizionale per i PC Windows 10, potrebbero verificarsi alcuni problemi.  Per altri dettagli vedere [Problemi noti](#bkmk_KnownIssues) .  

## <a name="configure-conditional-access"></a>Configurare l'accesso condizionale  
 Per configurare l'accesso condizionale, è prima di tutto necessario creare criteri di conformità e configurare criteri di accesso condizionale. Quando si configurano criteri di accesso condizionale per i PC, è possibile richiedere che i PC siano conformi ai criteri di conformità per accedere ai servizi Exchange Online e SharePoint Online.  

### <a name="prerequisites"></a>Prerequisiti  

-   ADFS Sync e un abbonamento a O365. L'abbonamento a Office&365; serve per la configurazione di Exchange Online e SharePoint Online.  

-   Sottoscrizione di Microsoft Intune. La sottoscrizione di Microsoft Intune deve essere configurata nella console di Configuration Manager. È necessario trovarsi in una distribuzione ibrida.  

 I PC devono soddisfare i requisiti seguenti:  

-   [Prerequisiti](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1) per la registrazione automatica dei dispositivi con Azure Active Directory  

     È possibile registrare i PC con Azure AD tramite i criteri di conformità.  

    -   Per i PC Windows 8.1 e Windows 10, è possibile usare un oggetto Criteri di gruppo di Active Directory per configurare i dispositivi per la registrazione automatica con Azure AD.  

    -   o   Per i PC Windows 7, è necessario distribuire il pacchetto software di registrazione dei dispositivi nel PC Windows 7 con System Center Configuration Manager. L'argomento [Registrazione automatica dei dispositivi con Azure Active Directory per i dispositivi Windows aggiunti a un dominio](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1) offre informazioni più dettagliate.  

-   I PC devono usare Office 2013 o Office 2016 con l'autenticazione moderna [abilitata](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a).  

 I passaggi descritti di seguito si applicano sia a Exchange Online sia a SharePoint Online  

### <a name="step-1-configure-compliance-policy"></a>Passaggio 1. Configurare i criteri di conformità  
 Nella console di Configuration Manager creare criteri di conformità con le regole seguenti:  

-   Richiedi registrazione in Azure Active Directory: questa regola controlla se il dispositivo dell'utente è aggiunto all'area di lavoro in Azure AD e, in caso contrario, il dispositivo viene registrato automaticamente in Azure AD. La registrazione automatica è supportata solo in Windows 8.1. Per i PC con Windows 7, distribuire un file MSI per eseguire la registrazione automatica. Per informazioni dettagliate, vedere [Registrazione automatica dei dispositivi con Azure Active Directory](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1)  

-   **Tutti gli aggiornamenti richiesti installati con una scadenza maggiore di X giorni:** questa regola controlla se il dispositivo dell'utente dispone di tutti gli aggiornamenti necessari (specificati nella regola Richiedi aggiornamenti automatici) entro la scadenza e il periodo di tolleranza specificati dall'utente e installa automaticamente eventuali aggiornamenti necessari in sospeso.  

-   **Richiedi Crittografia unità BitLocker:** questo è un controllo per verificare se l'unità principale (ad esempio, C:\\) nel dispositivo è crittografata con BitLocker. Se la crittografia Bitlocker non è attivata nel dispositivo primario, l'accesso alla posta elettronica e ai servizi di SharePoint è bloccato.  

-   **Richiedi antimalware:** questo è un controllo per verificare se il software antimalware (System Center Endpoint Protection o solo Windows Defender) è abilitato e in esecuzione. Se non è abilitato, l'accesso alla posta elettronica e ai servizi di SharePoint è bloccato.  

### <a name="step-2-evaluate-the-effect-of-conditional-access"></a>Passaggio 2: Valutare l'effetto dell'accesso condizionale  
 Eseguire il report di conformità dell'accesso condizionale. Tale report si trova nella sezione Monitoraggio in Report > Gestione conformità e impostazioni. Il report indica lo stato di conformità di tutti i dispositivi.  Ai dispositivi segnalati come non conformi verrà impedito l'accesso a Exchange Online e SharePoint Online.  

 ![CA&#95;compliance&#95;report](media/CA_compliance_report.png)  

### <a name="configure-active-directory-security-groups"></a>Configurare i gruppi di sicurezza di Active Directory  
 I criteri di accesso condizionale sono destinati a diversi gruppi di utenti in base ai tipi di criteri. Questi gruppi contengono gli utenti a cui saranno destinati i criteri o che ne saranno esenti. Quando a un utente vengono destinati criteri, ogni dispositivo che egli usa deve essere conforme per poter accedere al servizio.  

 Gruppi di utenti di sicurezza di Active Directory. Questi gruppi di utenti devono essere sincronizzati con Azure Active Directory. È anche possibile configurare questi gruppi nell'interfaccia di amministrazione di Office 365 o nel portale per gli account di Intune.  

 È possibile specificare due tipi di gruppi in ogni criterio. :  

-   **Gruppi di destinazione**: gruppi di utenti a cui si applicano i criteri. Usare lo stesso gruppo per i criteri di conformità e di accesso condizionale.  

-   **Gruppi esentati**: gruppi di utenti che sono esentati dai criteri (facoltativo)  
    Se un utente si trova in entrambi i gruppi, sarà esentato dai criteri.  

     Solo i gruppi di destinazione dei criteri di accesso condizionale vengono valutati.  

### <a name="step-3--create-a-conditional-access-policy-for-exchange-online-and-sharepoint-online"></a>Passaggio 3.  Creare criteri di accesso condizionale per Exchange Online e SharePoint Online  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Per creare criteri per Exchange Online, selezionare **Abilita criteri di accesso condizionale per Exchange Online**.  

     Per creare criteri per SharePoint Online, selezionare **Abilita criteri di accesso condizionale per SharePoint Online**.  

3.  Nella scheda **Home** del gruppo **Collegamenti** fare clic su **Configura i criteri di accesso condizionale nella console di Intune**. Potrebbe essere necessario specificare il nome utente e la password dell'account usato per la connessione di Configuration Manager a Intune.  

     Verrà visualizzata la console di amministrazione di Intune.  

4.  Per Exchange Online, nella console di amministrazione di Microsoft Intune fare clic su **Criteri > Accesso condizionale > Criteri di Exchange Online**.  

     Per SharePoint Online, nella console di amministrazione di Microsoft Intune fare clic su **Criteri > Accesso condizionale > Criteri di SharePoint Online**.  

5.  Impostare il requisito per il PC Windows sull'opzione**I dispositivi devono essere conformi**.  

6.  In **Gruppi di destinazione**fare clic su **Modifica** per selezionare i gruppi di sicurezza di Azure Active Directory ai quali verranno applicati i criteri.  

    > [!NOTE]  
    >  È necessario usare lo stesso gruppo di utenti di sicurezza per la distribuzione dei criteri di conformità e il gruppo di destinazione per i criteri di accesso condizionale.  

     Facoltativamente, in **Gruppi esentati**fare clic su **Modifica** per selezionare i gruppi di sicurezza di Azure Active Directory esentati da questi criteri.  

7.  Fare clic su **Salva** per creare e salvare i criteri.  

 Gli utenti finali bloccati a causa della mancanza di conformità visualizzeranno le informazioni sulla conformità in Software Center di System Center Configuration Manager e verrà avviata una nuova valutazione dei criteri dopo la risoluzione dei problemi di conformità.  

##  <a name="bkmk_KnownIssues"></a> Problemi noti  
 Quando si usa questa funzionalità, potrebbero verificarsi i problemi seguenti:  

-   In questo aggiornamento 1602 non viene applicata la conformità di 5 giorni. Anche se il controllo di conformità nel dispositivo dell'utente finale è stato eseguito da più di 5 giorni, gli utenti possono comunque accedere a Office 365 e SharePoint Online.  

-   Quando un dispositivo non è conforme ai criteri di conformità, il motivo non viene visualizzato automaticamente. L'utente finale deve passare al nuovo Software Center per individuare il motivo della mancanza di conformità. Il motivo viene visualizzato nella sezione Conformità del dispositivo di Software Center.  

-   Gli utenti di Windows 10 potrebbero visualizzare più errori di accesso quando cercano di raggiungere le risorse di Office 365 e/o SharePoint Online. Si noti che Windows 10 non offre supporto completo per l'accesso condizionale.  

### <a name="see-also"></a>Vedere anche  
 [Proteggere i dati e l'infrastruttura del sito con System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)

