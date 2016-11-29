---
title: Predichiarare dispositivi con i numeri di serie IMEI o iOS
description: "Predichiarare i dispositivi di proprietà dell'azienda con numero di serie IMEI o iOS."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
caps.latest.revision: 3
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6cd640085e90b2945326e3fa942ae9bd7b8f7e24
ms.openlocfilehash: 2550fef062b5ef508e4c0492a5a9c63ffcb9084a

---
# <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Predichiarare dispositivi con i numeri di serie IMEI o iOS

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile identificare i dispositivi di proprietà dell'azienda importando i relativi codici IMEI (International station Mobile Equipment Identity) o i numeri di serie iOS. È possibile caricare un file con valori separati da virgola (CSV) contenente i codici IMEI o immettere manualmente le informazioni relative ai dispositivi.  Le informazioni importate imposteranno la **proprietà** dei dispositivi registrati come "**Corporate**" negli elenchi di dispositivi. È tuttavia necessaria una licenza di Intune per ogni utente che accede al servizio.  

## <a name="predeclare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>Predichiarare dispositivi di proprietà dell'azienda con codici IMEI o numeri seriali iOS

1.  Nella console di Configuration Manager passare a Asset e conformità > Panoramica > Tutti i dispositivi aziendali > Dispositivi predichiarati > e fare clic su Aggiungi dispositivi predichiarati. Verrà avviata la procedura guidata per dispositivi predichiarati.
2.  Specificare il modo in cui si vogliono aggiungere le informazioni sul dispositivo:
     -  Caricare un file CSV che contiene i codici IMEI e i dettagli
     -  Aggiungere manualmente i codici IMEI e i dettagli. Per immettere manualmente le informazioni, digitare il codice IMEI o il numero di serie iOS e i dettagli per i dispositivi.

      Per i file caricati, individuare il file CSV contenente le informazioni per predichiarare i dispositivi aziendali. Il file deve avere il formato seguente, senza la prima riga specificata a scopo informativo. Ogni riga deve contenere un codice IMEI o numero di serie iOS. Solo i numeri di serie dei dispositivi iOS possono essere predichiarati; usare i codici IMEI per i dispositivi di altre piattaforme. Questa tabella contiene dati di esempio:
      | IMEI #  | Numero di serie iOS #  | OS | Dettagli |
      | :------------ |:---------------|:-----|:-----|
      | 123456789012345    |   | WINDOWS | Dispositivo Windows di proprietà dell'azienda|
      |       | A1B2C3D4E5C6 |   iOS |  Dispositivo iOS di proprietà dell'azienda|
      | 223456789012345 | E6D5C4B3A210 |   iOS |    Altro dispositivo iOS|
      | 323456789012345 |        |   iOS |  Terzo dispositivo iOS|
      | 123456789012346 |         |   Android |     Dispositivo Android dell'azienda|

    Non includere una riga di intestazione nel file CSV. L'esempio precedente include un'intestazione a scopo informativo.

    **Le colonne accettano i valori seguenti:**    
      - Colonna 1: codice IMEI senza spazi
      - Colonna 2: numero di serie iOS
      - Colonna 3: sistema operativo del dispositivo:
         - IOS: tutti i dispositivi iOS
         - WINDOWS: include Windows Phone, Windows 10 per dispositivi mobili e PC Windows
         - ANDROID: tutti i dispositivi Android
      - Colonna 4: dettagli (facoltativi). Informazioni aggiuntive sul dispositivo che vengono visualizzate nella console di Configuration Manager. Limite di 1024 caratteri.

    Fare clic su **Avanti**.

3. Verificare i risultati dell'importazione del file. Se un numero di dispositivo è stato importato in precedenza, Configuration Manager visualizza i dispositivi e i **dettagli** di sostituzione. Selezionare i dispositivi di cui si vuole sovrascrivere i dettagli. I dettagli del dispositivo possono essere modificati solo importando di nuovo l'identificazione del dispositivo o un numero di serie. Fare clic su **Avanti** per continuare o **Indietro** per mantenere aggiornati i dettagli e completare la procedura guidata.

4. Se l'importazione include i numeri di serie iOS, è necessario assegnare i dispositivi a un profilo di registrazione. Selezionare **Profilo di registrazione da assegnare** dall'elenco dei profili disponibili e fare clic su **Avanti**.

5. Fare clic su **Avanti** per visualizzare un riepilogo e completare la procedura guidata.



<!--HONumber=Nov16_HO1-->


