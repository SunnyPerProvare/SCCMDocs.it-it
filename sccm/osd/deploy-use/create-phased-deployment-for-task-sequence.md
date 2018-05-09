---
title: Creare una distribuzione in più fasi per una sequenza di attività
titleSuffix: Configuration Manager
description: Creare distribuzioni in più fasi per le sequenze di attività
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2bda41cfd01e5ef90771350e650f68a27c3af6ed
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="create-phased-deployments-for-a-task-sequence-with-system-center-configuration-manager"></a>Creare distribuzioni in più fasi per una sequenza di attività con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le distribuzioni in più fasi automatizzano un'implementazione coordinata e in sequenza di una sequenza di attività in più raccolte. È possibile creare distribuzioni in più fasi con l'impostazione predefinita di due fasi oppure configurare manualmente più fasi. La distribuzione in più fasi delle sequenze di attività non supporta l'installazione di PXE o di supporti. 

>[!NOTE]
> Le distribuzioni in più fasi sono una funzionalità di versione non definitiva introdotta in Configuration Manager 1802. <!--1356837-->

## <a name="security-scope-and-log-file-information"></a>Informazioni sull'ambito di protezione e sui file di log

**Ambito di protezione**:</br>
Le distribuzioni create da distribuzioni in più fasi sono visualizzabili solo per gli utenti che hanno ambito di protezione **Tutto**.

**File di log**: </br>
SMS_PhasedDeployment.log

## <a name="create-a-default-two-phased-deployment-for-a-task-sequence"></a>Creare una distribuzione in due fasi predefinita per una sequenza di attività

Usare le istruzioni seguenti per creare una distribuzione in più fasi. 

1. Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi** e selezionare **Sequenze di attività**.

2. Fare clic con il pulsante destro del mouse su una sequenza di attività esistente e selezionare **Create Phased Deployment** (Crea distribuzione in fasi). 

3. Nella scheda **Generale** assegnare alla distribuzione in più fasi un nome e una descrizione (facoltativa), quindi selezionare **Crea automaticamente una distribuzione predefinita in due fasi**. 

4. Popolare i campi **Prima raccolta** e **Seconda raccolta**. Selezionare **Avanti**.

5. Nella scheda **Impostazioni** scegliere un'opzione per ogni impostazione di pianificazione. Al termine, selezionare **Avanti**. 
    - **Criteri per l'esito positivo della prima fase.** 
        - **Percentuale di esiti positivi della distribuzione**: specificare la percentuale di dispositivi che devono completare la distribuzione con esito positivo. 
    - **Condizioni per l'inizio della seconda fase della distribuzione dopo l'esito positivo della prima fase** (scegliere un'opzione):
        - **Inizia automaticamente questa fase dopo un periodo di differimento (in giorni)**: scegliere il numero di giorni di attesa prima di iniziare la seconda fase dopo l'esito positivo della prima. 
        - **Inizia manualmente la seconda fase della distribuzione**: non avviare la seconda fase automaticamente dopo l'esito positivo della prima. Richiedere che venga avviata manualmente. 
    - **Dopo avere incluso un dispositivo, installare il software** (scegliere un'opzione):
        - **Appena possibile**: imposta come scadenza per l'installazione nel dispositivo il momento in cui il dispositivo viene incluso.
        - **Ora della scadenza (rispetto all'ora in cui il dispositivo viene incluso)**: imposta come scadenza per l'installazione un determinato numero di giorni dopo che il dispositivo è stato incluso. 

6. Nella scheda **Fasi** fare clic sulla prima fase e quindi su **Modifica**.  Specificare **Esperienza utente**, ad esempio **Notifiche utente** o **Gestione filtri di scrittura per dispositivi con Windows Embedded**. Fare clic su **Apply**.

7. Specificare l'impostazione **Punti di distribuzione** per la fase nella scheda **Punti di distribuzione**. Fare clic su **Applica** e su **OK**.        

8. Nella scheda **Fasi** modificare la seconda fase per **Esperienza utente** e **Punti di distribuzione**. Fare clic su **Applica** e su **OK**.

9. Confermare le selezioni nella scheda **Riepilogo** e quindi fare clic su **Avanti** per continuare nella procedura guidata.

>[!WARNING]
>Le distribuzioni in più fasi non notificano all'utente se la distribuzione di una sequenza di attività è [ad alto rischio](/sccm/protect/understand/settings-to-manage-high-risk-deployments.md). 


## <a name="suspend-and-resume-phases-or-move-to-the-next-phase"></a>Sospendere e riprendere una fase o passare alla fase successiva
In alcuni casi, può essere necessario sospendere manualmente una distribuzione in più fasi, riprendere una distribuzione in più fasi sospesa o passare alla fase successiva. 

### <a name="move-to-the-next-phase"></a>Passare alla fase successiva
Se si seleziona l'impostazione **Inizia manualmente la seconda fase della distribuzione**, è necessario avviare la seconda fase. Usare le istruzioni seguenti per passare alla seconda fase: 

1. Nella console di Configuration Manager selezionare **Raccolta software**, espandere **Sistemi operativi** e fare clic su **Sequenze di attività**.
2. Evidenziare la sequenza di attività.
3. Fare clic sulla scheda **Distribuzione in più fasi** nella parte inferiore della console. 
4. Fare clic con il pulsante destro del mouse sulla distribuzione in più fasi e selezionare **Move to next phase** (Passa alla fase successiva).
![Sospendere, riprendere o passare alla fase successiva](media/Suspend-phased-deployment.PNG)

### <a name="suspend-or-resume-a-phased-deployment"></a>Sospendere o riprendere una distribuzione in più fasi
1. Nella console di Configuration Manager selezionare **Raccolta software**, espandere **Sistemi operativi** e fare clic su **Sequenze di attività**.
2. Evidenziare la sequenza di attività e fare clic sulla scheda **Distribuzione in più fasi** nella parte inferiore della console. 
3. Selezionare la distribuzione in più fasi e fare clic su **Sospendi** o su **Riprendi** sulla barra multifunzione.

## <a name="next-steps"></a>Passaggi successivi
[Creare una sequenza di attività personalizzata](create-a-custom-task-sequence.md) </br>
[Creare una sequenza di attività per distribuzioni non di sistema operativo](create-a-task-sequence-for-non-operating-system-deployments.md). 








