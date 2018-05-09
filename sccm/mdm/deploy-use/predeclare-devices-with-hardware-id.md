---
title: Predichiarare i dispositivi con i numeri di serie IMEI o iOS
titleSuffix: Configuration Manager
description: Predichiarare i dispositivi di proprietà dell'azienda con numero di serie IMEI o iOS.
ms.date: 09/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 86ef14c871f476df39923e01e47874702271a08d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Predichiarare i dispositivi con i numeri di serie IMEI o iOS

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile identificare i dispositivi di proprietà dell'azienda importando i relativi codici IMEI (International station Mobile Equipment Identity) o i numeri di serie iOS. È possibile caricare un file con valori delimitati da virgole (CSV) contenente i codici IMEI o immettere manualmente le informazioni relative ai dispositivi.  Le informazioni importate imposteranno la **Proprietà** dei dispositivi registrati come **Aziendale** negli elenchi di dispositivi. È tuttavia necessaria una licenza di Intune per ogni utente che accede al servizio.  

Se si caricano numeri di serie di dispositivi iOS di proprietà dell'azienda, è necessario che siano associati a un profilo di registrazione aziendale. Per fare in modo che risultino di proprietà dell'azienda, i dispositivi devono anche essere registrati tramite il programma di registrazione dispositivi di Apple o Apple Configurator.

>[!NOTE]
>I dispositivi Android, esclusi i dispositivi Samsung Knox Standard, devono essere associati a un numero di telefono per essere predichiarati e registrati come dispositivi di proprietà dell'azienda con un codice IMEI.

## <a name="how-to-predeclare-corporate-owned-devices"></a>Come predichiarare i dispositivi di proprietà dell'azienda

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Panoramica** > **Tutti i dispositivi di proprietà dell'azienda** > **Windows**Predeclared devices (Dispositivi predichiarati).

2.  Fare clic su **Create Predeclared Device** (Crea dispositivi predichiarati). Verrà avviata la procedura guidata per la creazione di dispositivi predichiarati.

3.  Specificare come si vogliono aggiungere le informazioni sul dispositivo:

     -  **Caricare un file CSV contenente numeri IMEI o numeri di serie e dettagli**

        Per questa opzione, fare clic su **Sfoglia** per specificare il file con estensione csv contenente le informazioni per predichiarare i dispositivi di proprietà dell'azienda. Il file con estensione csv deve essere formattato correttamente. Per altre informazioni, vedere [Formato per il caricamento di file con estensione csv](#format-for-uploading-csv-files).

     -  **Aggiungere manualmente i numeri IMEI o i numeri di serie e i dettagli**

        Per immettere manualmente le informazioni, digitare il codice IMEI o il numero di serie iOS e i dettagli per i dispositivi. Prima di continuare, correggere eventuali errori o avvisi.

    Fare clic su **Avanti**.

4. Se è stato caricato un file con estensione csv, esaminare i risultati dell'importazione del file. Se è stato importato in precedenza un numero di dispositivo, Configuration Manager visualizza i dispositivi e i **Dettagli** della sostituzione. Selezionare i dispositivi di cui si vuole sovrascrivere i dettagli. I dettagli del dispositivo possono essere modificati solo importando di nuovo l'identificazione del dispositivo o un numero di serie.

  Se si è scelto di immettere manualmente il numero, completare il modulo per i dispositivi da predichiarare.

  Fare clic su **Avanti** per continuare.

4. Se l'elenco include numeri di serie iOS, selezionare **Enrollment Profile to Assign** (Profilo di registrazione da assegnare) dall'elenco dei profili disponibili e fare clic su **Avanti**.

5. Fare clic su **Avanti** per esaminare i dettagli e quindi fare clic nuovamente su **Avanti** per caricare i dati.

6. Fare clic su **Chiudi** per completare la procedura.

## <a name="format-for-uploading-csv-files"></a>Formato per il caricamento di file con estensione csv

Il file con estensione csv da usare per identificare i dispositivi in base al codice IMEI o al numero di serie iOS deve essere nel formato seguente, esclusa la riga superiore che viene indicata unicamente a scopo informativo. Ogni riga deve contenere un numero ID, ovvero un numero IMEI o un numero di serie iOS. Per i dispositivi iOS è possibile includere entrambi i valori. I numeri IMEI possono essere usati per dispositivi Android, iOS e Windows. Questa tabella contiene dati di esempio:

| Numero IMEI  | Numero di serie iOS  | OS | Dettagli |
|------------ |---------------|-----|-----|
| 123456789012345    |   | WINDOWS | Dispositivo Windows di proprietà dell'azienda|
|   | A1B2C3D4E5C6 | IOS |  Dispositivo iOS di proprietà dell'azienda|
| 223456789012345 | E6D5C4B3A210 |   IOS |  Altro dispositivo iOS|
| 323456789012345 |        |   IOS |    Terzo dispositivo iOS|
| 123456789012346 |         |   ANDROID |   Dispositivo Android di proprietà dell'azienda|

Non includere una riga di intestazione nel file CSV. L'esempio seguente visualizza gli stessi dati di esempio in formato CSV:

```
123456789012345,,WINDOWS,Company-owned Windows device
,A1B2C3D4E5C6,IOS,Company-owned iOS device
223456789012345,E6D5C4B3A210,IOS,Another iOS device
323456789012345,,IOS,A third iOS device
123456789012346,,ANDROID,Company-owned Android device
```

Le colonne nel file con estensione csv accettano i valori seguenti:

| Colonna 1 | Colonna 2 | Colonna 3 | Colonna 4 |
|---|---|---|---|
|Codice IMEI senza spazi | Numero di serie iOS | IOS, WINDOWS o ANDROID | Dettagli dispositivo facoltativi (limite di 1024 caratteri) |
