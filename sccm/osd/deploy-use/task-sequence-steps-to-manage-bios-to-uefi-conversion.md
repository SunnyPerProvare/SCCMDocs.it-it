---
title: "Passaggi della sequenza di attività per la gestione della conversione da BIOS a UEFI | Configuration Manager"
description: "Informazioni su come personalizzare una sequenza di attività di distribuzione del sistema operativo per preparare una partizione FAT32 per la transizione a UEFI."
ms.custom: na
ms.date: 11/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 54089ac8aa95154534d010bee8c7e2cbd70d1c7e
ms.openlocfilehash: 30838ed3ad045f781a748f96c874bf543ea05462


---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Passaggi della sequenza di attività per la gestione della conversione da BIOS a UEFI
A partire da Configuration Manager versione 1610 è possibile personalizzare una sequenza di attività di distribuzione del sistema operativo con una nuova variabile, TSUEFIDrive, in modo che il passaggio **Riavvia computer** prepari una partizione FAT32 sul disco rigido per la transizione a UEFI. La procedura seguente fornisce un esempio sulle modalità di creazione dei passaggi della sequenza di attività per preparare il disco rigido alla conversione da BIOS a UEFI.

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Per preparare la partizione FAT32 alla conversione a UEFI:
In una sequenza di attività esistente per installare un sistema operativo si aggiungerà un nuovo gruppo usando la procedura di conversione da BIOS a UEFI.

1. Creare un nuovo gruppo di sequenze di attività dopo aver eseguito la proceduta per acquisire file e impostazioni e prima della procedura di installazione del sistema operativo. Ad esempio, creare un gruppo dopo il gruppo **Acquisisci file e impostazioni** denominato **BIOS-to-UEFI** (Da BIOS a UEFI).
2. Nella scheda **Opzioni** del nuovo gruppo aggiungere una nuova variabile della sequenza di attività come condizione in cui **_SMSTSBootUEFI** sia **diverso** da **true**. Questa operazione blocca l'esecuzione dei passaggi nel gruppo quando il computer è già in modalità UEFI.
![Gruppo BIOS to UEFI](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. Nel nuovo gruppo aggiungere il passaggio della sequenza di attività **Riavvia il computer**. In **Specificare cosa eseguire dopo il riavvio:** selezionare **The boot image assigned to this task sequence is selected** (L'immagine di avvio assegnata a questa sequenza di attività è selezionata) per avviare il computer in Windows PE.  
4. Nella scheda **Opzioni** aggiungere una variabile della sequenza attività come condizione in cui **_SMSTSInWinPE sia uguale a false** Questa operazione blocca l'esecuzione di questo passaggio se il computer è già in Windows PE.

    ![Passaggio Riavvia il computer](../../core/get-started/media/restart-in-windows-pe.png)
5. Aggiungere un passaggio per avviare lo strumento OEM che convertirà il firmware da BIOS a UEFI. Si tratta in genere di un passaggio della sequenza di attività **Esegui riga di comando** con una riga di comando per avviare lo strumento OEM.
6.  Aggiungere il passaggio della sequenza attività Formato e disco partizione che partiziona e formatta il disco rigido. Nel passaggio, eseguire le operazioni seguenti:
    1.  Creare la partizione FAT32 che verrà convertita in UEFI prima di installare il sistema operativo. Scegliere **GPT** per **Tipo disco**.
    ![Passaggio Formato e disco partizione](../../core/get-started/media/format-and-partition-disk.png)
    2.  Accedere alle proprietà della partizione FAT32. Immettere **TSUEFIDrive** nel campo **Variabile**. Quando la sequenza di attività rileva questa variabile, si avvia la preparazione per la transizione di UEFI prima di riavviare il computer.
    ![Proprietà della partizione](../../core/get-started/media/partition-properties.png)
    3. Creare una partizione NTFS che il motore della sequenza di attività usa per il salvataggio dello stato e per archiviare i file di log.
6.  Aggiungere il passaggio della sequenza di attività **Riavvia il computer**. In **Specificare cosa eseguire dopo il riavvio:** selezionare **The boot image assigned to this task sequence is selected** (L'immagine di avvio assegnata a questa sequenza di attività è selezionata) per avviare il computer in Windows PE.  



<!--HONumber=Dec16_HO3-->


