---
title: Definizioni malware di Endpoint Protection da una condivisione di rete
titleSuffix: Configuration Manager
description: Informazioni su come scaricare manualmente gli aggiornamenti delle definizioni più recenti da Microsoft e configurare i client per scaricare le definizioni.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 47c6a046dac7cd4b5d0d16f0342d7e95ba3cc2a0
ms.sourcegitcommit: 4f05517f7b284696a492a1b184cc5f25c5cda5e6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2018
ms.locfileid: "48891147"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-a-network-share-for-configuration-manager"></a>Abilitare le definizioni malware di Endpoint Protection da scaricare da una condivisione di rete per Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

 È possibile scaricare manualmente gli aggiornamenti delle definizioni più recenti da Microsoft e quindi configurare i client per scaricare le definizioni da una cartella condivisa in rete. Quando si usa questa origine degli aggiornamenti, gli utenti possono anche avviare gli aggiornamenti delle definizioni.

> [!NOTE]
>  Per poter scaricare gli aggiornamenti delle definizioni, i client devono avere accesso in lettura alla cartella condivisa.

 Per altre informazioni su come scaricare gli aggiornamenti del motore e delle definizioni per l'archiviazione nella condivisione file, vedere [Install the latest Microsoft antimalware and antispyware software](https://www.microsoft.com/wdsi/definitions) (Installare il software antimalware e antispyware di Microsoft più recente).

## <a name="to-configure-definition-downloads-from-a-file-share"></a>Per configurare i download delle definizioni da una condivisione file

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.

2.  Nell'area di lavoro **Asset e conformità** espandere **Endpoint Protection**e quindi fare clic su **Criteri antimalware**.

3.  Aprire la pagina delle proprietà relativa a **Criterio antimalware predefinito** o creare un nuovo criterio antimalware. Per altre informazioni su come creare criteri antimalware, vedere [Come creare e distribuire criteri antimalware per Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md).

4.  Nella sezione **Aggiornamenti delle definizioni** della finestra di dialogo delle proprietà antimalware fare clic su **Imposta origine**.

5.  Nella finestra di dialogo **Configura origini aggiornamenti definizioni** selezionare **Aggiornamenti dalle condivisioni file UNC**.

6.  Fare clic su **OK** per chiudere la finestra di dialogo **Configura origini aggiornamenti definizioni** .

7.  Fare clic su **Imposta percorsi**. Nella finestra di dialogo **Configurare percorsi UNC per l'aggiornamento di definizioni** aggiungere quindi uno o più percorsi UNC delle posizioni dei file degli aggiornamenti delle definizioni nella condivisione di rete.

8.  Fare clic su **OK** per chiudere la finestra di dialogo **Configurare percorsi UNC per l'aggiornamento di definizioni** .


> [!div class="button"]
[Passaggio successivo >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Indietro >](endpoint-configure-alerts.md)
