---
title: Gestire l'accesso a Internet usando criteri di Managed Browser | System Center Configuration Manager
description: Distribuire Intune Managed Browser per gestire e limitare l'accesso a Internet.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 735c45b8-a545-4805-84e5-46204fabd1a6
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e5efee7b94f5c61a610fd9f9fa278c992f9c64b8


---
# <a name="manage-internet-access-using-managed-browser-policies-with-system-center-configuration-manager"></a>Gestire l'accesso a Internet mediante criteri di Managed Browser con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager è possibile distribuire Intune Managed Browser, un'applicazione Web browser, e associare l'applicazione a un criterio di Managed Browser. Un criterio di Managed Browser consente di configurare un elenco Consenti o Blocca che limita i siti Web che gli utenti di Managed Browser possono visitare.  
  
 Poiché questa applicazione è un'applicazione gestita, è inoltre possibile applicare criteri di gestione delle applicazioni per dispositivi mobili per l'applicazione, ad esempio il controllo consente di acquisire l'utilizzo di Taglia, copia e Incolla, impedendo la schermata e inoltre garantire che i collegamenti al contenuto che gli utenti fanno clic solo aprire in altre gestito app. Per informazioni dettagliate, vedere [Proteggere le app usando i criteri di gestione delle applicazioni mobili](../../apps/deploy-use/protect-apps-using-mam-policies.md).  
  
> [!IMPORTANT]  
>  Se gli utenti installano il browser gestito autonomamente, non verrà gestito da alcun criterio specificato. Per assicurarsi che il browser sia gestito da Configuration Manager, è necessario disinstallare l'applicazione prima di poterla distribuire come applicazione gestita.  

 È possibile creare criteri di browser gestiti per i seguenti tipi di dispositivo:  

-   Dispositivi che eseguono Android 4 e versioni successive  

-   Dispositivi che eseguono iOS 7 e versioni successive  

> [!NOTE]  
>  Per altre informazioni e per scaricare l'app Intune Managed Browser, vedere [iTunes](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) per iOS e [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en) per Android.  
  
## <a name="create-a-managed-browser-policy"></a>Creare un criterio di browser gestiti  

1.  Nella console di Configuration Manager fare clic su **Raccolta software** > **Gestione applicazioni** > **Criteri di gestione delle applicazioni**.  

3.  Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea criteri di gestione delle applicazioni**.  

4.  Nella pagina **Generale** immettere il nome e la descrizione per il criterio e quindi fare clic su **Avanti**.  

5.  Nella pagina **Tipo di criterio** selezionare la piattaforma, selezionare **Managed Browser** per il tipo di criterio e quindi fare clic su **Avanti**.  

     Nella pagina **Managed Browser** selezionare una delle opzioni seguenti:  

    -   **Consentire al browser gestito aprire solo gli URL elencati di seguito** : specificare un elenco di URL che è possibile aprire il browser gestiti.  

    -   **Il blocco del browser gestito di aprire gli URL elencati di seguito** : specificare un elenco di URL che il browser gestito viene impedito di apertura.  

    > [!NOTE]  
    >  Non è possibile includere le URL consentiti e bloccati nello stesso criterio di browser gestiti.  

     Per altre informazioni sui formati di URL che è possibile specificare, vedere **Formato dell'URL per URL consentite e bloccate** in questo argomento.  

    > [!NOTE]  
    >  Il tipo di criteri **Generale** consente di modificare la funzionalità delle app distribuite per adeguarle ai criteri aziendali di conformità e di sicurezza. Ad esempio, è possibile limitare le operazioni taglia, copia e incolla in un'app con restrizioni. Per altre informazioni sul tipo di criteri Generale, vedere [Proteggere le app usando i criteri di gestione delle applicazioni mobili](../../apps/deploy-use/protect-apps-using-mam-policies.md).  

6.  Completare la procedura guidata.  

 Il nuovo criterio viene visualizzato nel nodo **Criteri di gestione delle applicazioni** dell'area di lavoro **Raccolta software** .  

## <a name="create-a-software-deployment-for-the-managed-browser-app"></a>Creare una distribuzione di software per l'applicazione di browser gestiti  
 Dopo aver creato il criterio di Managed Browser, è possibile creare un tipo di distribuzione di software per l'applicazione Managed Browser. È necessario associare un criterio Generale e un criterio Managed Browser per l'app Managed Browser.  
  
 Per altre informazioni, vedere [Create applications](../../apps/deploy-use/create-applications.md) (Creare le applicazioni).  
  
## <a name="security-and-privacy-for-the-managed-browser"></a>Sicurezza e privacy per lo strumento di wrapping delle app  

-   Sui dispositivi iOS, non è possibile aprire i siti web che gli utenti visitano che dispone di un certificato scaduto o non attendibile.  

-   Impostazioni apportate dall'utente per il browser predefinito sui dispositivi non vengono utilizzate dal browser gestiti. Infatti, il browser gestito non dispone dell'accesso a queste impostazioni.  

-   Se si configurano le opzioni **Richiedi PIN semplice per l'accesso** o **richiede credenziali aziendali per l'accesso** in un'applicazione per dispositivi mobili nei Criteri di gestione associato con il browser gestito e un utente fa clic sul collegamento Guida nella pagina autenticazione, è possibile passare tutti i siti Internet indipendentemente dal fatto che sono stati aggiunti a un elenco di blocco nei criteri di browser gestiti.  

-   Il Browser gestito può bloccare l'accesso ai siti solo quando vi si accede direttamente. È possibile bloccare l'accesso quando servizi intermedi (ad esempio, un servizio di traduzione) vengono utilizzati per accedere al sito.  

## <a name="reference-information"></a>Informazioni di riferimento  
  
###  <a name="url-format-for-allowed-and-blocked-urls"></a>Formato dell'URL per URL consentite e bloccate  

Utilizzare le seguenti informazioni per ulteriori informazioni sui formati consentiti e i caratteri jolly, che è possibile utilizzare quando si specificano le URL negli elenchi consentiti e bloccati.  

-   È possibile utilizzare il carattere jolly asterisco '**\***' secondo le regole nell'elenco di modelli consentiti sottostante.  

-   Assicurarsi che tutte le  URL abbiano con prefisso **http** o **https** quando immetterle nell'elenco.  

-   È possibile specificare numeri di porta nell'indirizzo. Se non si specifica un numero di porta, i valori utilizzati sono:  

    -   Porta 80 per http  

    -   Porta 443 per https  

     L'uso dei caratteri jolly per il numero di porta non è supportato, ad esempio **http://www.contoso.com:\*** e **http://www.contoso.com: /\***  

-   Per ulteriori informazioni sui modelli consentiti che è possibile utilizzare quando si specificano gli URL, utilizzare la tabella seguente:  

    |URL|Corrispondenze|Non corrisponde|  
    |---------|-------------|--------------------|  
    |http://www.contoso.com<br /><br /> Corrisponde a una singola pagina|www.contoso.com|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> contoso.com/|  
    |http://contoso.com<br /><br /> Corrisponde a una singola pagina|contoso.com/|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com|  
    |http://www.contoso.com/*<br /><br /> Corrisponde a tutte le URL a partire da www.contoso.com|www.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com/videos/tvshows|host.contoso.com<br /><br /> host.contoso.com/images|  
    |http://*.contoso.com/\*<br /><br /> Corrisponde a tutti i sottodomini in contoso.com|developer.contoso.com/resources<br /><br /> news.contoso.com/images<br /><br /> news.contoso.com/videos|contoso.host.com|  
    |http://www.contoso.com/images<br /><br /> Corrisponde a una singola cartella|www.contoso.com/images|www.contoso.com/images/dogs|  
    |http://www.contoso.com:80<br /><br /> Corrisponde a una singola pagina utilizzando un numero di porta|http://www.contoso.com:80||  
    |https://www.contoso.com<br /><br /> Corrisponde a una singola pagina protetta|https://www.contoso.com|http://www.contoso.com|  
    |http://www.contoso.com/Images/*<br /><br /> Corrisponde a una singola cartella e a tutte le sottocartelle|www.contoso.com/images/dogs<br /><br /> www.contoso.com/images/cats|www.contoso.com/videos|  

-   Di seguito sono riportati esempi di alcuni input che non è possibile specificare:  

    -   *.com  

    -   *.contoso/\*  

    -   www.contoso.com/*images  

    -   www.contoso.com/*images\*pigs  

    -   www.contoso.com/page*  

    -   Indirizzi IP  

    -   https://*  

    -   http://*  

    -   http://www.contoso.com :*  

    -   http://www.contoso.com:/*  

> [!NOTE]  
>  *.microsoft.com è sempre consentito.  
  
### <a name="how-conflicts-between-the-allow-and-block-list-are-resolved"></a>Come vengono risolti i conflitti tra l'elenco Consenti e blocca  
 Se distribuiti diversi criteri browser gestito a un dispositivo e si verifica un conflitto di impostazioni, sia per modalità (Consenti o blocca) e per elenchi di URL, che vengono poi valutati a livello di conflitti. In caso di conflitto si applica il comportamento seguente:  

-   Se le modalità disponibili in tutti i criteri sono uguali, ma gli elenchi di URL sono diversi, le URL non verranno applicate al dispositivo.  

-   Se le modalità disponibili in tutti i criteri sono diverse, ma gli elenchi di URL sono uguali,le URL non verranno applicate al dispositivo.  

-   Se un dispositivo riceve i criteri di browser gestiti per la prima volta ed il conflitto nei due criteri, le URL non verranno applicate al dispositivo Utilizzare il nodo **conflitti tra criteri** dei **criteri** nell’area di lavoro per visualizzare i conflitti.  

-   Se un dispositivo ha già ricevuto un criterio di browser gestiti e un secondo criterio è distribuito con le impostazioni in conflitto, le impostazioni originali rimangono sul dispositivo. Utilizzare il nodo **conflitti tra criteri** dei **criteri** nell’area di lavoro per visualizzare i conflitti.  



<!--HONumber=Nov16_HO1-->


