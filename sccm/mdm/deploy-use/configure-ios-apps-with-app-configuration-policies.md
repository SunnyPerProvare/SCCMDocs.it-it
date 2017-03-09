---
title: Configurare le app iOS con i criteri di configurazione delle app | Microsoft Docs
description: Questa operazione consente di evitare problemi di configurazione sui dispositivi che eseguono iOS 8 o versione successiva distribuendo i criteri di configurazione delle app agli utenti prima che gli utenti eseguano le app.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f0a78038-ea22-4826-9c07-1771b7dd2e8d
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 84f21f2e86212bc3fb6a505ff62c886e62b77d52
ms.lasthandoff: 03/06/2017

---
# <a name="apply-settings-to-ios-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Applicare le impostazioni alle app iOS con i criteri di configurazione app in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


È possibile usare i criteri di configurazione delle app in System Center Configuration Manager (Configuration Manager) per distribuire impostazioni che potrebbero essere necessarie quando un utente esegue un'app. Ad esempio, un'app potrebbe richiedere all'utente di specificare i seguenti dettagli:
- Un numero di porta personalizzato
- Impostazione della lingua
- Impostazioni di sicurezza
- Impostazioni di personalizzazione, ad esempio il logo aziendale

Se l'utente immette le impostazioni in modo errato, il carico di lavoro per la risoluzione ricade sul supporto tecnico e la distribuzione delle app risulta lenta.
Per evitare questi problemi, è possibile usare criteri di configurazione delle app per distribuire le impostazioni necessarie agli utenti prima che questi eseguano l'app. Le impostazioni vengono associate a un utente in modo automatico. L'utente non deve eseguire nessuna operazione.
Per usare un criterio di configurazione delle app in Configuration Manager, anziché distribuire i criteri di configurazione direttamente a utenti e dispositivi si associano i criterio a un tipo di distribuzione quando si distribuisce l'app. Le impostazioni dei criteri vengono applicate ogni volta che l'app ne esegue la ricerca (in genere, alla prima esecuzione dell'app stessa).

I criteri di configurazione delle app sono attualmente disponibili solo per i dispositivi che eseguono iOS 8 e versioni successive e per i tipi di applicazioni seguenti:

- **Pacchetto app iOS (file *.ipa)**
- **Pacchetto app iOS nell'App Store**

Per altre informazioni sui tipi di installazione delle app, vedere l'[introduzione alla gestione delle applicazioni](/sccm/apps/understand/introduction-to-application-management).

## <a name="create-an-app-configuration-policy"></a>Creare criteri di configurazione delle app

1. Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Criteri di configurazione dell'app**.
2. Nella scheda **Home**, nel gruppo **Criteri di configurazione dell'app** fare clic su **Creare nuovi criteri di configurazione dell'applicazione**.
3. Nella pagina **Generale** della Creazione guidata criteri di configurazione dell'app impostare le seguenti informazioni per i criteri:
  - **Nome**. Immettere un nome univoco per i criteri.
  - **Descrizione**. (Facoltativo) Per rendere più semplice l'identificazione dei criteri, è possibile aggiungere una descrizione.
  - **Categorie assegnate per migliorare la ricerca e i filtri**. (Facoltativo) Per creare e assegnare categorie ai criteri, scegliere **Categorie**. Con le categorie è più semplice trovare e ordinare gli elementi nella console di Configuration Manager.
4. Nella pagina **Criteri iOS** scegliere come impostare le informazioni sui criteri di configurazione:
  - **Specify name and value pairs** (Specifica coppie nome/valore). È possibile usare questa opzione per i file elenco di proprietà senza annidamento.

      *Per specificare una coppia nome/valore*
        1. Scegliere **Nuova** per aggiungere una nuova coppia.
        2. Nella finestra di dialogo **Aggiungere la coppia nome-valore** specificare quanto segue:
            - **Tipo**. Scegliere il tipo di valore da specificare nell'elenco.
            - **Nome**. Immettere il nome della chiave dell'elenco di proprietà per la quale si vuole specificare un valore.
            - **Valore**. Digitare il valore che verrà applicato alla chiave immessa.

  - **Browse to a property list file** (Passa a un file elenco di proprietà). Usare questa opzione se è già presente un file XML di configurazione app o per file più complessi con annidamento.

    *Per passare a un file elenco di proprietà*

      1.  Nel campo **Criteri di configurazione dell'app** immettere le informazioni sull'elenco di proprietà nel formato XML corretto.

      Per altre informazioni sugli elenchi di proprietà XML, vedere l'articolo relativo agli [elenchi di proprietà XML](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html) nella libreria degli sviluppatori iOS.

            The format of the XML property list varies depending on the app you are configuring. Contact the app supplier for details about the format to use.
            Intune supports the following data types in a property list:
            ```
            <integer>
            <real>
            <string>
            <array>
            <dict>
            <true /> or <false />
            ```
            For more information about data types, see [About Property Lists](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/PropertyLists/AboutPropertyLists/AboutPropertyLists.html) in the iOS Developer Library.
            Intune also supports the following token types in the property list:
            ```
            {{userprincipalname}} - (Example: John@contoso.com)
            {{mail}} - (Example: John@contoso.com)
            {{partialupn}} - (Example: John)
            {{accountid}} - (Example: fc0dc142-71d8-4b12-bbea-bae2a8514c81)
            {{deviceid}} - (Example: b9841cd9-9843-405f-be28-b2265c59ef97)
            {{userid}} - (Example: 3ec2c00f-b125-4519-acf0-302ac3761822)
            {{username}} - (Example: John Doe)
            {{serialnumber}} - (Example: F4KN99ZUG5V2) for iOS devices
            {{serialnumberlast4digits}} - (Example: G5V2) for iOS devices

            The {{ and }} characters are used by token types only and must not be used for other purposes.
            ```

      2.  Per importare un file XML creato in precedenza, scegliere **Seleziona file**.
6. Scegliere **Avanti**. Se sono presenti errori nel codice XML è necessario correggerli prima di continuare.
7. Completare i passaggi della procedura guidata.

I nuovi criteri di configurazione app vengono visualizzati nel nodo **Criteri di configurazione dell'app** dell'area di lavoro **Raccolta software**.

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>Associare un criterio di configurazione delle app a un'applicazione di Configuration Manager

Per associare criteri di configurazione delle app alla distribuzione di un'app per iOS, distribuire l'applicazione nel modo consueto con la procedura descritta nell'argomento [Distribuire applicazioni](/sccm/apps/deploy-use/deploy-applications).

Nella pagina **Criteri di configurazione dell'app** della Distribuzione guidata del software fare clic su **Nuovo**. Nella finestra di dialogo **Select App Configuration Policy** (Seleziona criteri di configurazione dell'app) scegliere un tipo di distribuzione dell'applicazione e i criteri di configurazione dell'app ai quali associarla.
Quando viene installato il tipo di distribuzione, le impostazioni dei criteri di configurazione dell'app vengono applicate automaticamente.

## <a name="example-format-for-the-mobile-app-configuration-xml-file"></a>Formato di esempio per il file XML di configurazione di app per dispositivi mobili

Quando si crea un file di configurazione di app per dispositivi mobili, è possibile usare questo formato per specificare uno o più dei seguenti valori:

```
<dict>
  <key>userprincipalname</key>
  <string>{{userprincipalname}}</string>
  <key>mail</key>
  <string>{{mail}}</string>
  <key>partialupn</key>
  <string>{{partialupn}}</string>
  <key>accountid</key>
  <string>{{accountid}}</string>
  <key>deviceid</key>
  <string>{{deviceid}}</string>
  <key>userid</key>
  <string>{{userid}}</string>
  <key>username</key>
  <string>{{username}}</string>
  <key>serialnumber</key>
  <string>{{serialnumber}}</string>
  <key>serialnumberlast4digits</key>
  <string>{{serialnumberlast4digits}}</string>
  <key>udidlast4digits</key>
  <string>{{udidlast4digits}}</string>
</dict>
```

