---
title: Configurare le app iOS con i criteri di configurazione delle app | System Center Configuration Manager
description: Questa operazione consente di evitare problemi di configurazione sui dispositivi che eseguono iOS 8 o versione successiva distribuendo i criteri di configurazione delle app agli utenti prima che gli utenti eseguano le app.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-app
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 74d5d776-e37d-45de-bdba-43541b03d12c
caps.latest.revision: 10
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9cbf28afbbe69f9a027ffad2a699b9d6b625e690


---
# <a name="configure-ios-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Configure iOS apps with app configuration policies in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


Usare i criteri di configurazione delle app in System Center Configuration Manager per specificare le impostazioni che potrebbero essere necessarie quando l'utente esegue un'app. Ad esempio, un'app potrebbe richiedere all'utente di specificare:
- Un numero di porta personalizzato
- Impostazione della lingua
- Impostazioni di sicurezza
- Impostazioni di personalizzazione, ad esempio il logo aziendale

Se queste impostazioni vengono immesse in modo non corretto dall'utente, si può avere un aumento del carico dell'help desk rallentando inoltre l'adozione di nuove app.
I criteri di configurazione delle app permettono di evitare questi problemi consentendo di distribuire tali impostazioni agli utenti in un criterio prima dell'esecuzione dell'app. Le impostazioni vengono quindi specificate automaticamente e l'utente non deve intraprendere alcuna azione.
Questi criteri non vengono distribuiti direttamente agli utenti e ai dispositivi, ma vengono associati a un tipo di distribuzione al momento della distribuzione dell'applicazione. Le impostazioni dei criteri vengono usate ogni volta che l'app ne esegue la ricerca (in genere, alla prima esecuzione).

I criteri di configurazione delle app sono attualmente disponibili solo per i dispositivi che eseguono iOS 8 e versioni successive e supportano i tipi di applicazioni seguenti:

- **Pacchetto app per iOS (file *.ipa)**
- **Pacchetto app per iOS nell'App Store**

Per altre informazioni sui tipi di installazione di app, vedere [Introduction to application management](/sccm/apps/understand/introduction-to-application-management) (Introduzione alla gestione delle applicazioni).

## <a name="create-an-app-configuration-policy"></a>Creare criteri di configurazione delle app

1. Nella console di Configuration Manager fare clic su **Raccolta software** > **Gestione applicazioni** > **Criteri di configurazione dell'app**.
3. Nel gruppo **Criteri di configurazione dell'app** della scheda **Home** fare clic su **Creare nuovi criteri di configurazione dell'applicazione**.
4. Nel pagina **Generale** della **Creazione guidata criteri di configurazione dell'app** specificare le informazioni seguenti:
    - **Nome**: specificare un nome univoco per il criterio.
    - **Descrizione**: facoltativamente specificare una descrizione identificativa per il criterio.
    - **Categorie assegnate per migliorare la ricerca e i filtri**: facoltativamente fare clic su **Categorie** per creare e assegnare le categorie al criterio. In questo modo è più semplice ordinare e trovare gli elementi nella console di Configuration Manager.
5. Nella pagina **Criteri iOS** scegliere come specificare le informazioni sui criteri di configurazione:
    - **Specificare le coppie di nome e valore**: è possibile usare questa opzione per i file di elenco di proprietà senza annidamento.
    Per specificare le coppie di nome/valore
        - Fare clic su **Nuova** per aggiungere una nuova coppia.
        - Nella finestra di dialogo **Aggiungere la coppia nome-valore** specificare quanto segue:
            - **Tipo**: scegliere il tipo di valore da specificare nell'elenco.
            - **Nome**: immettere il nome della chiave dell'elenco di proprietà per cui si vuole specificare un valore.
            - **Valore**: immettere il valore che verrà applicato alla chiave immessa.
        - Selezionare un file di elenco di proprietà: usare questa opzione se si dispone già di un file XML di configurazione app o per file più complessi con annidamento.
        Per passare a un file di elenco di proprietà
            - Nel campo **Criteri di configurazione dell'app** immettere le informazioni sull'elenco di proprietà nel formato XML corretto.
            Per altre informazioni sugli elenchi di proprietà XML, vedere l'articolo relativo agli [elenchi di proprietà XML](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html) nella libreria degli sviluppatori iOS.
            Il formato dell'elenco di proprietà XML varia a seconda dell'app da configurare. Per altre informazioni sul formato esatto da usare, contattare il fornitore dell'app.
            Intune supporta i tipi di dati seguenti in un elenco di proprietà:
            ```
            <integer>
            <real>
            <string>
            <array>
            <dict>
            <true /> or <false />
            ```
            Per altre informazioni sui tipi di dati, vedere l'articolo relativo agli [elenchi di proprietà](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/PropertyLists/AboutPropertyLists/AboutPropertyLists.html) nella libreria degli sviluppatori iOS.
            Inoltre, Intune supporta i tipi di token seguenti nell'elenco di proprietà:
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
            È possibile anche fare clic su **Seleziona file** per importare un file XML creato in precedenza.
6. Fare clic su **Avanti**. È necessario correggere eventuali errori nel codice XML prima di continuare.
6. Completare la procedura guidata.

Il nuovo criterio di configurazione delle app viene visualizzato nel nodo **Criteri di configurazione dell'app** dell'area di lavoro **Raccolta software**.

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>Associare un criterio di configurazione delle app a un'applicazione di Configuration Manager

Per associare un criterio di configurazione dell'app alla distribuzione di un'app per iOS, distribuire l'applicazione nel modo usuale tramite la procedura descritta nell'argomento [Distribuire applicazioni](/sccm/apps/deploy-use/deploy-applications).
Nella pagina **Criteri di configurazione dell'app** della **Distribuzione guidata del software** fare clic su **Nuovo**. Nella finestra di dialogo **Seleziona criteri di configurazione dell'app** scegliere un tipo di distribuzione dell'applicazione e un criterio di configurazione dell'app da associare.
Quando viene installato il tipo di distribuzione, le impostazioni dei criteri di configurazione dell'app verranno applicate automaticamente.

## <a name="example-format-for-the-mobile-app-configuration-xml-file"></a>Formato di esempio per il file XML di configurazione di app per dispositivi mobili

Quando si crea un file di configurazione di app per dispositivi mobili, è possibile specificare uno o più dei valori seguenti usando il formato:

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



<!--HONumber=Nov16_HO1-->


