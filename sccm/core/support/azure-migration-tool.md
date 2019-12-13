---
title: Estendere ed eseguire la migrazione di un sito locale in Microsoft Azure
titleSuffix: Configuration Manager
description: Informazioni su come usare lo strumento di migrazione per creare a livello di codice macchine virtuali di Azure per Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1c975c5e-efd1-4d47-a315-39ccb32633dc
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2e40e20fab31a505e59941a786ee3c8e7b4db63c
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74813385"
---
# <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>Estendere ed eseguire la migrazione di un sito locale in Microsoft Azure

*Si applica a: Configuration Manager (Current Branch)*


Questo strumento, introdotto nella versione 1910, consente di creare a livello di codice macchine virtuali di Azure per Configuration Manager. <!--3556022--> Consente di installare con impostazioni predefinite ruoli del sito come un server del sito passivo, punti di gestione e punti di distribuzione. Dopo aver convalidato i nuovi ruoli, usarli come sistemi del sito aggiuntivi per ottenere una disponibilità elevata. È anche possibile rimuovere il ruolo del sistema del sito locale e mantenere solo il ruolo VM di Azure.

## <a name="prerequisites"></a>Prerequisiti

- Sottoscrizione di Azure

- Rete virtuale di Azure con gateway ExpressRoute

<!-- - A standalone primary site. A hierarchy with a central administration site isn't currently supported. can comment this out because TP only supports a standalone primary!-->

- È necessario che l'account utente sia un **amministratore completo** di Configuration Manager con diritti di amministratore per il server del sito primario.

- Per aggiungere un server passivo, il sito primario deve soddisfare i [requisiti di disponibilità elevata del server del sito](/sccm/core/servers/deploy/configure/site-server-high-availability#prerequisites). Ad esempio, richiede una [raccolta contenuto remota](/sccm/core/plan-design/hierarchy/the-content-library#bkmk_remote).

### <a name="required-azure-permissions"></a>Autorizzazioni di Azure necessarie

Quando si esegue lo strumento è necessario disporre delle autorizzazioni seguenti in Azure:
<!--5789222-->
Microsoft.Resources/subscriptions/resourceGroups/read <br>
Microsoft.Resources/subscriptions/resourceGroups/write <br>
Microsoft.Resources/deployments/read <br>
Microsoft.Resources/deployments/write <br>
Microsoft.Resources/deployments/validate/action <br>
Microsoft.Authorization/roleAssignments/read <br>
Microsoft.Authorization/roleAssignments/write <br>
Microsoft.Compute/virtualMachines/extensions/read <br>
Microsoft.Compute/virtualMachines/extensions/write <br>
Microsoft.Compute/virtualMachines/read <br>
Microsoft.Compute/virtualMachines/write <br>
Microsoft.Network/virtualNetworks/read <br>
Microsoft.Network/virtualNetworks/subnets/read <br>
Microsoft.Network/virtualNetworks/subnets/join/action <br>
Microsoft.Network/networkInterfaces/read <br>
Microsoft.Network/networkInterfaces/write <br>
Microsoft.Network/networkInterfaces/join/action <br>
Microsoft.Network/networkSecurityGroups/write <br>
Microsoft.Network/networkSecurityGroups/read <br>
Microsoft.Network/networkSecurityGroups/join/action <br>
Microsoft.Storage/storageAccounts/write <br>
Microsoft.Storage/storageAccounts/read <br>
Microsoft.Storage/storageAccounts/listkeys/action <br>
Microsoft.Storage/storageAccounts/listServiceSas/action <br>
Microsoft.Storage/storageAccounts/blobServices/containers/write <br>
Microsoft.Storage/storageAccounts/blobServices/containers/read <br>
Microsoft.KeyVault/vaults/deploy/action <br>
Microsoft.KeyVault/vaults/read <br>


Per altre informazioni sulle autorizzazioni e sull'assegnazione di ruoli, vedere [Gestire l'accesso alle risorse di Azure tramite il controllo degli accessi in base al ruolo](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal).

## <a name="run-the-tool"></a>Eseguire lo strumento

1. Accedere al server del sito primario ed eseguire lo strumento seguente nella directory di installazione di Configuration Manager: `Cd.Latest\SMSSETUP\TOOLS\ExtendMigrateToAzure\ExtendMigrateToAzure.exe`

1. Esaminare le informazioni nella scheda **Generale** e quindi passare alla scheda delle **informazioni su Azure**.

1. Nelle **informazioni su Azure** scegliere l'**ambiente Azure** e quindi **Accedi**.

    > [!TIP]
    > Per eseguire correttamente l'accesso, può essere necessario aggiungere `https://*.microsoft.com` all'elenco di siti Web attendibili.

    [ ![Scheda delle informazioni su Azure nello strumento di estensione e migrazione](./media/3556022-azure-information-tab.png)](./media/3556022-azure-information-tab.png#lightbox)

1. Dopo aver eseguito l'accesso selezionare l'**ID sottoscrizione** e la **rete virtuale**. Lo strumento elenca solo le reti con un gateway ExpressRoute.

## <a name="site-server-high-availability"></a>Disponibilità elevata del server del sito

1. Nella scheda **Disponibilità elevata del server del sito** selezionare **Controlla** per valutare l'idoneità del sito.

    Se uno dei controlli ha esito negativo, selezionare **Altri dettagli** per determinare come correggere il problema. Per altre informazioni su questi prerequisiti, vedere [Disponibilità elevata del server del sito](/sccm/core/servers/deploy/configure/site-server-high-availability#prerequisites).

2. Se si vuole estendere o eseguire la migrazione del server del sito in Azure, selezionare **Create a site server in Azure** (Crea un sito del server in Azure). Compilare i campi seguenti:

    |Name|Descrizione|
    |---|---|
    |**Sottoscrizione**|Sola lettura. Indica il nome e l'ID della sottoscrizione.|
    |**Gruppo di risorse**| Elenca i gruppi di risorse disponibili. Se è necessario creare un nuovo gruppo di risorse, usare il [portale di Azure](https://portal.azure.com) e quindi eseguire di nuovo lo strumento.|
    |**Percorso**| Sola lettura. Determinato dalla posizione della rete virtuale|
    |**Dimensioni macchina virtuale**|Scegliere una dimensione che sia adatta al carico di lavoro. Microsoft consiglia **Standard_DS3_v2**.|
    |**Sistema operativo**|Sola lettura. Lo strumento usa Windows Server 2019.|
    |**Tipo di disco**|Sola lettura. Lo strumento usa SSD Premium per ottenere prestazioni ottimali.|
    |**Rete virtuale**|Sola lettura.|
    |**Subnet**|Selezionare la subnet da usare. Se è necessario creare una nuova subnet, usare il [portale di Azure](https://portal.azure.com).|
    |**Nome computer**|Immettere il nome della macchina virtuale del server del sito passivo in Azure. Si tratta dello stesso nome visualizzato nel [portale di Azure](https://portal.azure.com).|
    |**Local admin username** (Nome utente amministratore locale)|Immettere il nome dell'utente amministratore locale creato dalla macchina virtuale di Azure prima dell'aggiunta al dominio.|
    |**Password dell'amministratore locale**|La password dell'utente amministratore locale. Per proteggere la password durante la distribuzione di Azure, archiviarla come segreto in [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-overview). Usare quindi il riferimento qui. Se necessario, crearne una nuova dal [portale di Azure](https://portal.azure.com).|
    |**FQDN dominio**|Il nome di dominio completo (FQDN) del dominio Active Directory da usare per l'aggiunta. Per impostazione predefinita, lo strumento ricava questo valore dal computer in uso.|
    |**Nome utente di dominio**|Nome dell'utente del dominio a cui è consentita l'aggiunta al dominio. Per impostazione predefinita, lo strumento usa il nome dell'utente attualmente connesso.|
    |**Password del dominio**|La password dell'utente del dominio usata per l'aggiunta al dominio. Lo strumento la verifica dopo aver selezionato **Avvio**. Per proteggere la password durante la distribuzione di Azure, archiviarla come segreto in [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-overview). Usare quindi il riferimento qui. Se necessario, crearne una nuova dal [portale di Azure](https://portal.azure.com).|
    |**Domain DNS IP** (IP DNS dominio)|Usato per l'aggiunta al dominio. Per impostazione predefinita, lo strumento usa il DNS del computer in uso.|
    |**Tipo**|Sola lettura. Visualizza *Server del sito passivo* come tipo.|
    
1. Per avviare il provisioning della macchina virtuale di Azure, selezionare **Avvio**. Per monitorare lo stato della distribuzione, passare alla scheda delle **distribuzioni in Azure** nello strumento. Per ottenere lo stato più recente, selezionare **Refresh Deployment Status** (Aggiorna stato distribuzione).

    > [!TIP]
    > È anche possibile usare il [portale di Azure](https://portal.azure.com) per verificare lo stato, individuare gli errori e determinare le possibili correzioni.

1. Al termine della distribuzione, passare a SQL Server e concedere le autorizzazioni per la nuova macchina virtuale di Azure. Per altre informazioni, vedere [Disponibilità elevata del server del sito - Prerequisiti](/sccm/core/servers/deploy/configure/site-server-high-availability#prerequisites).

1. Per aggiungere la macchina virtuale di Azure come server del sito in modalità passiva, selezionare **Add site server in passive mode** (Aggiungi il server del sito in modalità passiva).

1. Dopo che il sito ha aggiunto il server del sito in modalità passiva, nella scheda **Disponibilità elevata del server del sito**.

   [![Server del sito passivo aggiunto alla scheda Disponibilità elevata del server del sito](./media/3556022-site-server-passive-mode.png)](./media/3556022-site-server-passive-mode.png#lightbox)

1. Passare quindi alla scheda delle [distribuzioni in Azure](#bkmk_deploy-azure) per completare la distribuzione.

## <a name="site-database"></a>Database del sito

Lo strumento attualmente non offre attività per la migrazione del database da locale ad Azure. È possibile scegliere di spostare il database da un'istanza di SQL Server locale a una VM di SQL Server di Azure. Lo strumento elenca gli articoli seguenti nella scheda **Database del sito** per:

- [Eseguire backup e ripristino del database](/sccm/core/servers/manage/backup-and-recovery)
- [Configurare SQL Always On e consentire la replica dei dati](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-backup)
- [Eseguire la migrazione di un database SQL a una VM di SQL Server di Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)

## <a name="site-system-roles"></a>Ruoli del sistema del sito

1. Passare alla scheda **Ruoli sistema del sito**. Per eseguire il provisioning di un nuovo ruolo del sistema del sito con le impostazioni predefinite, selezionare **Crea nuovo**. Il provisioning può essere eseguito dei ruoli punto di gestione, punto di distribuzione e punto di aggiornamento software. Non tutti i ruoli sono attualmente disponibili nello strumento.

    [![Scheda dei ruoli del sistema del sito nello strumento di estensione e migrazione](./media/3556022-site-system-roles-tab.png)](./media/3556022-site-system-roles-tab.png#lightbox)

1. Nella finestra di provisioning compilare i campi per eseguire il provisioning della macchina virtuale del ruolo del sito in Azure. Questi dettagli sono simili all'elenco precedente per il server del sito.

1. Per avviare il provisioning della macchina virtuale di Azure, selezionare **Avvio**. Per monitorare lo stato della distribuzione, passare alla scheda delle **distribuzioni in Azure** nello strumento. Per ottenere lo stato più recente, selezionare **Refresh Deployment Status** (Aggiorna stato distribuzione).

    > [!TIP]
    > È anche possibile usare il [portale di Azure](https://portal.azure.com) per verificare lo stato, individuare gli errori e determinare le possibili correzioni.

1. Ripetere questa procedura per aggiungere altri ruoli del sistema del sito.

1. Passare quindi alla scheda delle [distribuzioni in Azure](#bkmk_deploy-azure) per completare la distribuzione.

1. Al termine della distribuzione, passare alla console di Configuration Manager per apportare ulteriori modifiche al ruolo del sito.

## <a name="bkmk_deploy-azure"></a> Distribuzioni in Azure

1. Quando Azure crea la macchina virtuale, passare alla scheda delle **distribuzioni in Azure** nello strumento. Selezionare **Distribuisci** per configurare il ruolo con le impostazioni predefinite.

1. Selezionare **Esegui** per avviare lo script di PowerShell.

    [![Distribuire i ruoli del sito eseguendo lo script di PowerShell generato](./media/3556022-run-powershell-script-deployment.png)](./media/3556022-run-powershell-script-deployment.png#lightbox)

1. Ripetere questa procedura per configurare altri ruoli.

## <a name="next-steps"></a>Passaggi successivi

Esaminare le modifiche nel [portale di Azure](https://portal.azure.com)
