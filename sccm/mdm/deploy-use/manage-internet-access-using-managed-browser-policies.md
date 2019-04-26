---
title: Gestire l'accesso a Internet utilizzando criteri di browser gestiti
titleSuffix: Configuration Manager
description: Distribuire Intune Managed Browser per gestire e limitare l'accesso a Internet.
ms.date: 07/06/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 8e25e00c-c9a8-473f-bcb7-ea989f6ca3c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ede2563adbd517dbcda0a408fa5b9b166e8e3c12
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62255997"
---
# <a name="manage-internet-access-using-managed-browser-policies-with-system-center-configuration-manager"></a>Gestire l'accesso a Internet mediante criteri di Managed Browser con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager è possibile distribuire Intune Managed Browser, un'applicazione Web browser, e associare l'applicazione ai criteri di Managed Browser. I criteri di Managed Browser consentono di configurare un elenco Consenti o Blocca che limita i siti Web che gli utenti di Managed Browser possono visitare.  

 Poiché questa applicazione è un'applicazione gestita, è possibile anche applicare criteri di gestione delle applicazioni per dispositivi mobili, ad esempio il controllo dell'uso delle funzioni taglia, copia e incolla. Ciò impedisce l'acquisizione di schermate e garantisce anche che i collegamenti al contenuto vengano aperti solo in altre app gestite. Per informazioni dettagliate, vedere [Proteggere le app usando i criteri di gestione delle applicazioni mobili](protect-apps-using-mam-policies.md).  

> [!IMPORTANT]  
>  Se gli utenti installano il browser gestito autonomamente, non verrà gestito da alcun criterio specificato. Per assicurarsi che il browser sia gestito da Configuration Manager, è necessario disinstallare l'applicazione prima di poterla distribuire come applicazione gestita.  

 È possibile creare criteri di browser gestiti per i seguenti tipi di dispositivo:  

-   Dispositivi che eseguono Android 4 e versioni successive  

-   Dispositivi che eseguono iOS 7 e versioni successive  

> [!NOTE]  
>  Per altre informazioni e per scaricare l'app Intune Managed Browser, vedere [iTunes](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) per iOS e [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en) per Android.  

## <a name="create-a-managed-browser-policy"></a>Creare un criterio di browser gestiti  

1.  Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Criteri di gestione delle applicazioni**.  

3.  Nella scheda **Home** nel gruppo **Crea** scegliere **Crea criteri di gestione delle applicazioni**.  

4.  Nella pagina **Generale** immettere il nome e la descrizione per il criterio e quindi fare clic su **Avanti**.  

5.  Nella pagina **Tipo di criterio** selezionare la piattaforma, selezionare **Managed Browser** per il tipo di criterio e quindi fare clic su **Avanti**.  

     Nella pagina **Managed Browser** selezionare una delle opzioni seguenti:  

    -   **Consenti a Managed Browser di aprire solo gli URL elencati di seguito**: specificare un elenco di URL che potranno essere aperti da Managed Browser.  

    -   **Non consentire a Managed Browser di aprire gli URL elencati di seguito**: specificare un elenco di URL che non potranno essere aperti da Managed Browser.  

    > [!NOTE]  
    >  Non è possibile includere le URL consentiti e bloccati nello stesso criterio di browser gestiti.  

     Per altre informazioni sui formati URL che è possibile specificare, vedere la sezione relativa ai formati URL per gli URL consentiti e bloccati in questo articolo.  

    > [!NOTE]  
    >  Il tipo di criterio Generale consente di modificare la funzionalità delle app distribuite per adeguarle ai criteri aziendali di conformità e sicurezza. Ad esempio, è possibile limitare le operazioni taglia, copia e incolla in un'app con restrizioni. Per altre informazioni sul tipo di criterio Generale, vedere [Proteggere le app usando i criteri di gestione delle applicazioni mobili](protect-apps-using-mam-policies.md).  

6.  Completare la procedura guidata.  

Il nuovo criterio viene visualizzato nel nodo **Criteri di gestione delle applicazioni** dell'area di lavoro **Raccolta software** .  

## <a name="create-a-software-deployment-for-the-managed-browser-app"></a>Creare una distribuzione di software per l'applicazione di browser gestiti  
 Dopo aver creato il criterio di Managed Browser, è possibile creare un tipo di distribuzione di software per l'applicazione Managed Browser. È necessario associare un criterio generale e un criterio di Managed Browser per l'app Managed Browser.  

 Per altre informazioni, vedere [Create applications](create-applications.md) (Creare le applicazioni).  

## <a name="security-and-privacy-for-the-managed-browser"></a>Sicurezza e privacy per lo strumento di wrapping delle app  

-   Sui dispositivi iOS, non è possibile aprire i siti Web con certificati scaduti o non attendibili.  

-   Impostazioni apportate dall'utente per il browser predefinito sui dispositivi non vengono utilizzate dal browser gestiti. Managed Browser non ha infatti accesso a queste impostazioni.  

-   Se si configurano le opzioni **Richiedi PIN semplice per l'accesso** o **Richiedi credenziali aziendali per l'accesso** nei criteri di gestione per applicazioni mobili associati a Managed Browser, un utente può fare clic sul collegamento Guida nella pagina di autenticazione e quindi passare a qualsiasi sito, inclusi quelli aggiunti a un elenco di siti bloccati nei criteri di Managed Browser.  

-   Il Browser gestito può bloccare l'accesso ai siti solo quando vi si accede direttamente. È possibile bloccare l'accesso quando servizi intermedi (ad esempio, un servizio di traduzione) vengono utilizzati per accedere al sito.  

## <a name="reference-information"></a>Informazioni di riferimento  

###  <a name="url-format-for-allowed-and-blocked-urls"></a>Formato dell'URL per URL consentite e bloccate  

Utilizzare le seguenti informazioni per ulteriori informazioni sui formati consentiti e i caratteri jolly, che è possibile utilizzare quando si specificano le URL negli elenchi consentiti e bloccati.  

- Usare il carattere jolly `*` (asterisco) secondo le regole nell'elenco di modelli consentiti sottostante.  

- Aggiungere il prefisso **http** o **https** a tutti gli URL durante l'immissione nell'elenco.  

- Specificare i numeri di porta nell'indirizzo. Se non si specifica un numero di porta, vengono usati i valori seguenti:  

  - Porta 80 per http  

  - Porta 443 per https  

    Non usare caratteri jolly per il numero di porta, perché non sono supportati. Ad esempio: `http://www.contoso.com:*`   

- Per ulteriori informazioni sui modelli consentiti che è possibile utilizzare quando si specificano gli URL, utilizzare la tabella seguente:  


  |                                           URL                                            |                                                    Corrispondenze                                                    |                                    Non corrisponde                                     |
  |------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
  |                `http://www.contoso.com`<br /><br /> Corrisponde a una singola pagina                |                                               `www.contoso.com`                                               |  `host.contoso.com`<br /><br /> `www.contoso.com/images`<br /><br /> `contoso.com/`   |
  |                  `http://contoso.com`<br /><br /> Corrisponde a una singola pagina                  |                                                 `contoso.com`                                                 | `host.contoso.com`<br /><br /> `www.contoso.com/images`<br /><br /> `www.contoso.com` |
  | `http://www.contoso.com/*`<br /><br /> Corrisponde a tutti gli URL che iniziano con `www.contoso.com` |      `www.contoso.com`<br /><br /> `www.contoso.com/images`<br /><br /> `www.contoso.com/videos/tvshows`      |               `host.contoso.com`<br /><br /> `host.contoso.com/images`                |
  |      `http://*.contoso.com/*`<br /><br /> Corrisponde a tutti i sottodomini in contoso.com      | `developer.contoso.com/resources`<br /><br /> `news.contoso.com/images`<br /><br /> `news.contoso.com/videos` |                                  `contoso.host.com`                                   |
  |           `http://www.contoso.com/images`<br /><br /> Corrisponde a una singola cartella            |                                           `www.contoso.com/images`                                            |                             `www.contoso.com/images/dogs`                             |
  |    `http://www.contoso.com:80`<br /><br /> Corrisponde a una singola pagina utilizzando un numero di porta    |                                          `http://www.contoso.com:80`                                          |                                                                                       |
  |           `https://www.contoso.com`<br /><br /> Corrisponde a una singola pagina protetta            |                                           `https://www.contoso.com`                                           |                               `http://www.contoso.com`                                |
  | `http://www.contoso.com/images/*`<br /><br /> Corrisponde a una singola cartella e a tutte le sottocartelle |                    `www.contoso.com/images/dogs`<br /><br /> `www.contoso.com/images/cats`                    |                               `www.contoso.com/videos`                                |


- Di seguito sono riportati esempi di alcuni input che non è possibile specificare:  

  -   `*.com`  

  -   `*.contoso/*`  

  -   `www.contoso.com/*images`  

  -   `www.contoso.com/*images*pigs`  

  -   `www.contoso.com/page*`  

  -   Indirizzi IP  

  -   `https://*`  

  -   `http://*`  

  -   `http://www.contoso.com:*`  

  -   `http://www.contoso.com: /*`  

> [!NOTE]  
>  `*.microsoft.com` è sempre consentito.  

### <a name="how-conflicts-between-the-allow-and-block-list-are-resolved"></a>Come vengono risolti i conflitti tra l'elenco Consenti e blocca  
 Se distribuiti diversi criteri browser gestito a un dispositivo e si verifica un conflitto di impostazioni, sia per modalità (Consenti o blocca) e per elenchi di URL, che vengono poi valutati a livello di conflitti. In caso di conflitto si applica il comportamento seguente:  

-   Se le modalità disponibili in ogni criterio sono uguali ma gli elenchi di URL sono diversi, gli URL non verranno applicati sul dispositivo.  

-   Se le modalità in ogni criterio sono diverse ma gli elenchi di URL sono uguali, gli URL non verranno applicati sul dispositivo.  

-   Se un dispositivo riceve i criteri di browser gestiti per la prima volta ed il conflitto nei due criteri, le URL non verranno applicate al dispositivo Utilizzare il nodo **conflitti tra criteri** dei **criteri** nell’area di lavoro per visualizzare i conflitti.  

-   Se un dispositivo ha già ricevuto un criterio di browser gestiti e un secondo criterio è distribuito con le impostazioni in conflitto, le impostazioni originali rimangono sul dispositivo. Utilizzare il nodo **conflitti tra criteri** dei **criteri** nell’area di lavoro per visualizzare i conflitti.  
