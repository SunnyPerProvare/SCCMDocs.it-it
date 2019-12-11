---
title: Crittografare i dati di ripristino
titleSuffix: Configuration Manager
description: ''
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 1ee6541a-e243-43ea-be16-d0349f7f0c6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9549186d8e04da2309eae8a5bd4baa8c3bb8042c
ms.sourcegitcommit: 4d3999de1e13d579dd128578cb5dcee46fe3b0d6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74855920"
---
# <a name="encrypt-recovery-data"></a>Crittografare i dati di ripristino

*Si applica a: Configuration Manager (Current Branch)*

<!--3601034-->

Quando si crea un criterio di gestione di BitLocker, Configuration Manager distribuisce il servizio di ripristino in un punto di gestione abilitato per HTTPS. Nella pagina **gestione client** dei criteri di gestione di BitLocker, quando si **configurano i servizi di Gestione BitLocker**, il client esegue il backup delle informazioni di recupero chiavi nel database del sito. Queste informazioni includono le chiavi di ripristino di BitLocker, i pacchetti di ripristino e gli hash delle password TPM.

Quando gli utenti sono bloccati dal dispositivo protetto, è possibile usare queste informazioni per ripristinare l'accesso al dispositivo. Considerata la natura sensibile di queste informazioni, è consigliabile crittografare i dati nel database del sito.

Questo articolo descrive come usare SQL Server crittografia a livello di cella con il proprio certificato.

Se non si desidera creare un certificato di crittografia di Gestione BitLocker, acconsentire esplicitamente all'archiviazione in testo normale dei dati di ripristino. Quando si crea un criterio di gestione di BitLocker, abilitare l'opzione per **consentire l'archiviazione delle informazioni di ripristino in testo normale**.

> [!NOTE]
> Un altro livello di sicurezza consiste nel crittografare l'intero database del sito. Se si Abilita la crittografia nel database, non sono presenti problemi funzionali in Configuration Manager.
>
> Applicare la crittografia con cautela, soprattutto in ambienti di grandi dimensioni. A seconda delle tabelle crittografate e della versione di SQL, è possibile riscontrare un calo delle prestazioni del 25%. Aggiornare i piani di backup e ripristino in modo da poter ripristinare correttamente i dati crittografati.

## <a name="certificate-requirements"></a>Requisiti del certificato

È possibile utilizzare il processo personalizzato per creare e distribuire il certificato di crittografia di Gestione BitLocker, purché soddisfi i requisiti seguenti:

- Il nome del certificato di crittografia di Gestione BitLocker deve essere `BitLockerManagement_CERT`.

- Crittografare il certificato con una chiave master del database.

- Per gli utenti SQL seguenti sono necessarie autorizzazioni di **controllo** per il certificato:
  - RecoveryAndHardwareCore
  - RecoveryAndHardwareRead
  - RecoveryAndHardwareWrite

- Distribuire lo stesso certificato in ogni database del sito nella gerarchia.

- Creare il certificato con la versione più recente di SQL Server nell'ambiente in uso. Ad esempio:
  - I certificati creati con SQL Server 2016 o versioni successive sono compatibili con SQL Server 2014 o versioni precedenti.
  - I certificati creati con SQL Server 2014 o versioni precedenti non sono compatibili con SQL Server 2016 o versioni successive.

## <a name="example-scripts"></a>Script di esempio

Questi script SQL sono esempi per la creazione e la distribuzione di un certificato di crittografia di Gestione BitLocker nel database del sito di Configuration Manager.

### <a name="create-certificate"></a>Crea il certificato

Questo script di esempio esegue le azioni seguenti:

- Crea un certificato
- Imposta le autorizzazioni
- Crea una chiave master del database

Prima di usare questo script in un ambiente di produzione, modificare i valori seguenti:

- Nome database sito (`CM_ABC`)
- Password per creare la chiave master (`MyMasterKeyPassword`)
- Data di scadenza certificato (`20391022`)

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = MyMasterKeyPassword
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN
    CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
    WITH SUBJECT = 'BitLocker Management',
    EXPIRY_DATE = '20391022'

    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="back-up-certificate"></a>Backup del certificato

Questo script di esempio esegue il backup di un certificato. Quando si salva il certificato in un file, è possibile [ripristinarlo](#restore-certificate) in altri database del sito nella gerarchia.

Prima di usare questo script in un ambiente di produzione, modificare i valori seguenti:

- Nome database sito (`CM_ABC`)
- Percorso file e nome (`C:\BitLockerManagement_CERT_KEY`)
- Password di esportazione chiave (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
BACKUP CERTIFICATE BitLockerManagement_CERT TO FILE = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        ENCRYPTION BY PASSWORD = MyExportKeyPassword)
```

> [!IMPORTANT]
> Archiviare il file di certificato esportato e la password associata in un luogo sicuro.

### <a name="restore-certificate"></a>Ripristina certificato

Questo script di esempio ripristina un certificato da un file. Usare questo processo per distribuire un certificato creato in un altro database del sito.

Prima di usare questo script in un ambiente di produzione, modificare i valori seguenti:

- Nome database sito (`CM_ABC`)
- Password della chiave master (`MyMasterKeyPassword`)
- Percorso file e nome (`C:\BitLockerManagement_CERT_KEY`)
- Password di esportazione chiave (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = MyMasterKeyPassword
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN

CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
FROM FILE  = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        DECRYPTION BY PASSWORD = MyExportKeyPassword)

GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="verify-certificate"></a>Verifica il certificato

Usare questo script SQL per verificare che SQL abbia creato correttamente il certificato con le autorizzazioni necessarie.

``` SQL
USE CM_ABC
declare @count int
select @count = count(distinct u.name) from sys.database_principals u
join sys.database_permissions p on p.grantee_principal_id = u.principal_id or p.grantor_principal_id = u.principal_id
join sys.certificates c on c.certificate_id = p.major_id
where u.name in('RecoveryAndHardwareCore', 'RecoveryAndHardwareRead', 'RecoveryAndHardwareWrite') and
c.name = 'BitLockerManagement_CERT' and p.permission_name like 'CONTROL'
if(@count >= 3) select 1
else select 0
```

Se il certificato è valido, lo script restituisce un valore `1`.

## <a name="see-also"></a>Vedere anche

Per ulteriori informazioni su questi comandi SQL, vedere gli articoli seguenti:

- [Chiavi di crittografia del database e di SQL Server](https://docs.microsoft.com/sql/relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine)
- [CREATE CERTIFICATE](https://docs.microsoft.com/sql/t-sql/statements/create-certificate-transact-sql)
- [BACKUP CERTIFICATE](https://docs.microsoft.com/sql/t-sql/statements/backup-certificate-transact-sql)
- [CREATE MASTER KEY](https://docs.microsoft.com/sql/t-sql/statements/create-master-key-transact-sql)
- [BACKUP MASTER KEY](https://docs.microsoft.com/sql/t-sql/statements/backup-master-key-transact-sql)
- [Concedere le autorizzazioni per i certificati](https://docs.microsoft.com/sql/t-sql/statements/grant-certificate-permissions-transact-sql)
