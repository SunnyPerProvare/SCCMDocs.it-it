---
title: Impostazioni di Windows Hello for Business
titleSuffix: Configuration Manager
description: Informazioni su come integrare Windows Hello per le aziende con System Center Configuration Manager.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 60dcf98b83fb4650a10e5503d42b9f49d3aba359
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32350086"
---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>Impostazioni di Windows Hello for Business in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

<!--1245704-->
System Center Configuration Manager consente l'integrazione con Windows Hello per le aziende (in precedenza Microsoft Passport per Windows), che rappresenta un metodo di accesso alternativo per i dispositivi Windows 10. Hello for Business usa Active Directory o un account di Azure Active Directory per sostituire una password, una smart card o una smart card virtuale.  

Hello for Business consente di eseguire l'accesso usando un **movimento dell'utente** anziché una password. Il movimento dell'utente può essere un semplice PIN, un'autenticazione biometrica o un dispositivo esterno come un lettore di impronte digitali.

Per altre informazioni, vedere [Windows Hello for Business](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification).


> [!Note]  
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Abilitare le funzionalità facoltative degli aggiornamenti](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


 Configuration Manager si integra con Windows Hello per le aziende in due modi:  

-   È possibile usare Configuration Manager per controllare i movimenti che gli utenti possono utilizzare o meno per l'accesso.  

-   È possibile archiviare i certificati di autenticazione nel provider di archiviazione chiavi (KSP) di Windows Hello for Business. Per altre informazioni, vedere i [profili certificato](introduction-to-certificate-profiles.md).  

- È possibile distribuire i criteri di Windows Hello per le aziende su dispositivi appartenenti a un dominio Windows 10 che eseguono il client di Configuration Manager. Questa configurazione è descritta nella sezione [Configurare Windows Hello per le aziende su dispositivi appartenenti a un dominio Windows 10](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices). Quando si usa Configuration Manager con Microsoft Intune (ambiente ibrido), è possibile configurare queste impostazioni nei dispositivi Windows 10 e Windows 10 Mobile. Per altre informazioni, vedere [Configurare le impostazioni di Windows Hello for Business (ibrido)](../../mdm/deploy-use/windows-hello-for-business-settings.md).

## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>Configurare Windows Hello per le aziende su dispositivi appartenenti a un dominio Windows 10
È possibile controllare le impostazioni di Windows Hello for Business nei dispositivi Windows 10 aggiunti a un dominio tramite la creazione e la distribuzione di un profilo di Windows Hello for Business. Questo approccio è consigliato.


Se si usa l'autenticazione basata su certificati, è anche necessario distribuire un profilo certificato, come descritto in [Configurare un profilo certificato](#configure-a-certificate-profile). Se invece si usa l'autenticazione basata su chiavi, non è necessario distribuire un profilo certificato.

## <a name="configure-a-windows-hello-for-business-profile"></a>Configurare un profilo Windows Hello for Business  

Nella console di Configuration Manager, in **Accesso risorse aziendali**, fare clic con il pulsante destro del mouse su **Profili Windows Hello for Business** e scegliere **Nuovo** per avviare la creazione guidata del profilo. Specificare le impostazioni richieste dalla procedura guidata, rivedere e confermare le impostazioni nell'ultima pagina, quindi scegliere **Chiudi**. Di seguito è riportato un esempio di come potrebbero essere le impostazioni:  

![Creazione guidata dei criteri di Windows Hello for Business, con l'elenco delle impostazioni disponibili](../media/Hello-for-Business-settings.png)

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Configurare un profilo certificato per registrare il certificato di registrazione di Windows Hello for Business in Configuration Manager  
 Se si vuole usare l'accesso basato sui certificati di Windows Hello for Business, configurare i componenti seguenti:  

-   Un profilo certificato in Configuration Manager.  

-   Nel profilo certificato selezionare un modello che usi l'utilizzo chiavi avanzato per l'accesso smart card.  

-   Se si vogliono archiviare i profili certificato nel contenitore chiave Windows Hello for Business e il profilo certificato usa l'EKU **Accesso smart card**, è necessario configurare le autorizzazioni seguenti per la registrazione delle chiavi per assicurarsi che il certificato venga convalidato correttamente.
È necessario aver prima creato il gruppo **Key Admins** e aggiunto tutti i computer del gruppo di gestione di Configuration Manager come membri del gruppo.

Alcune configurazioni potrebbero non richiedere di configurare le autorizzazioni o potrebbero richiedere ulteriori configurazioni. Per altre informazioni, vedere la tabella seguente:

|Versione client Windows|Configuration Manager 1602 o 1606|Configuration Manager 1610|Configuration Manager 1702 o versioni successive|
|-|-|-|-|
|Windows 10 Anniversary Update|Hotfix non richiesti<br><br>Autorizzazioni non richieste<br><br>Aggiornamenti dello schema di Windows non richiesti|Hotfix non richiesti (vedere **Avviso**)<br><br>Autorizzazioni non richieste<br><br>Aggiornamenti dello schema di Windows non richiesti|Configurare le autorizzazioni<br><br>Applicare lo schema di Windows Server 2016 ad Active Directory|
|Windows 10 Creators Update o versioni successive|Non supportato|Installare [questo hotfix](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v)<br><br>Configurare le autorizzazioni<br><br>Applicare lo schema di Windows Server 2016 ad Active Directory|Configurare le autorizzazioni<br><br>Applicare lo schema di Windows Server 2016 ad Active Directory|

> [!WARNING]
> Anche se l'[hotfix](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v) non è richiesto per Configuration Manager 1610 e l'Aggiornamento dell'anniversario di Windows 10, può essere installato.  Se l'hotfix è installato, è necessario configurare le autorizzazioni e applicare lo schema di Windows Server 2016 ad Active Directory.

## <a name="to-configure-permissions"></a>Per configurare le autorizzazioni

1.  Accedere a un controller di dominio o a workstation di gestione con le credenziali di amministratore di dominio o equivalenti.
2.  Aprire **Utenti e computer di Active Directory**.
3.  Nel riquadro di spostamento fare clic con il pulsante destro del mouse sul nome di dominio e scegliere **Proprietà**.
4.  Nella scheda**Sicurezza** della finestra di dialogo *<domain name>* **Proprietà** fare clic su **Avanzate**. Se la scheda **Sicurezza** non è visualizzata, attivare **Funzionalità avanzate** dal menu **Visualizza** di **Utenti e computer di Active Directory**.
5.  Fare clic su **Aggiungi**.
6.  Nella finestra di dialogo **Voci di autorizzazione per** *<domain name>* fare clic su **Selezionare un'entità**.
7.  Nella finestra di dialogo **Select User, Computer, Service Account, or Group** (Seleziona utente, computer, account di servizio o gruppo) digitare **Key Admins** nella casella di testo **Inserire il nome oggetto da selezionare**. Fare clic su **OK**.
8.  Dall'elenco **Si applica a** scegliere **Oggetti Utente discendenti**.
9.  Scorrere fino in fondo alla pagina e fare clic su **Cancella tutto**.
10. Nella sezione **Proprietà** selezionare **Leggi msDS-KeyCredentialLink**.
11. Fare clic tre volte su **OK** per completare l'attività.


## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere i [profili certificato](introduction-to-certificate-profiles.md).  




