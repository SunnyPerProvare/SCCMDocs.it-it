---
title: Usare l'editor delle sequenze di attività
titleSuffix: Configuration Manager
description: Informazioni su come usare l'editor della sequenza di attività nella console di Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: a4e8bb56-ee85-49fd-8b1c-c8f513cec671
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2c4053419fc45dce352d527a73a79b96416a5d02
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74662419"
---
# <a name="use-the-task-sequence-editor"></a>Usare l'editor delle sequenze di attività

*Si applica a: Configuration Manager (Current Branch)*

Modificare le sequenze di attività nella console di Configuration Manager usando l' **Editor della sequenza di attività**. Utilizzare l'editor per:  

- Aprire una visualizzazione di sola lettura della sequenza di attività

- Aggiungere o rimuovere passaggi della sequenza di attività  

- Modificare l'ordine dei passaggi della sequenza di attività  

- Aggiungere o rimuovere gruppi di passaggi  

- Copiare e incollare i passaggi tra le sequenze di attività

- Impostare le opzioni del passaggio, ad esempio se la sequenza di attività continua quando si verifica un errore  

- Aggiungere condizioni ai passaggi e ai gruppi di una sequenza di attività  

- Copiare e incollare le condizioni tra i passaggi in una sequenza di attività

- Eseguire una ricerca nella sequenza di attività per individuare rapidamente i passaggi

Prima di poter modificare una sequenza di attività, è necessario crearla. Per altre informazioni, vedere [gestire e creare sequenze di attività](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks).

## <a name="about-the-task-sequence-editor"></a>Informazioni sull'editor delle sequenze di attività

Nell'editor della sequenza di attività sono inclusi i componenti seguenti:

![Screenshot con annotazioni della finestra dell'editor della sequenza di attività di esempio](media/task-sequence-editor.png)

<!-- The following numbered steps correspond to annotations in the above screenshot. Don't change the step numbers without also revising the image! -->

1. Nome della sequenza di attività
2. Ricerca. Per altre informazioni, vedere [Cerca](#bkmk_search).
3. **Proprietà** del gruppo o del passaggio selezionato nella sequenza

    Per ulteriori informazioni sulle proprietà e sulle opzioni di un passaggio specifico, vedere [informazioni sui passaggi della sequenza di attività](/sccm/osd/understand/task-sequence-steps).

4. **Opzioni** per il gruppo o il passaggio selezionato nella sequenza

    Per ulteriori informazioni sulle opzioni generali in tutti i passaggi o sulle opzioni di un passaggio specifico, vedere [informazioni sui passaggi della sequenza di attività](/sccm/osd/understand/task-sequence-steps).

    Per altre informazioni su come configurare le condizioni, vedere [condizioni](#bkmk_conditions).

5. **Aggiungere** un gruppo o i passaggi
6. **Rimuovere** un gruppo o i passaggi
7. Comprimi tutti i gruppi o Espandi tutti i gruppi
8. Spostare la posizione di un gruppo o di un passaggio nella sequenza (sposta su, Sposta giù)
9. La sequenza di attività:
    - Vedere l'ordine dei passaggi e dei gruppi.
    - Espande o comprime un gruppo.
    - Quando si disabilita un passaggio o un gruppo sulle relative **Opzioni**, questo viene disattivato nella sequenza.
    - L'icona di un passaggio viene modificata in un errore rosso se si verifica un problema con il passaggio. Ad esempio, manca un valore obbligatorio.
10. **OK**: salvare e chiudere
11. **Annulla**: Chiudi senza salvare le modifiche
12. **Applica**: Salva modifiche e Mantieni aperto

È possibile ridimensionare l'editor della sequenza di attività usando i controlli Windows standard. Per ridimensionare le larghezze dei due riquadri principali, utilizzare il mouse per selezionare la barra tra la sequenza di attività e le proprietà del passaggio, quindi trascinarla verso sinistra o verso destra.

## <a name="bkmk_view"></a> Visualizzare una sequenza di attività

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e quindi selezionare il nodo **Sequenze di attività**.  

2. Nell'elenco **Sequenza di attività** selezionare la sequenza di attività da visualizzare.  

3. Nella scheda **Home** della barra multifunzione selezionare **Visualizza** nel gruppo **Sequenza di attività**.

    > [!TIP]
    > Questa azione è l'impostazione predefinita. Se si fa doppio clic su una sequenza di attività, **verrà visualizzata la sequenza di attività** .

Questa azione consente di aprire l'editor della sequenza di attività in modalità di sola lettura. In questa modalità è possibile eseguire le azioni seguenti:

- Visualizza tutti i gruppi, i passaggi, le proprietà e le opzioni
- Espandere e comprimere i gruppi
- Eseguire una ricerca nella sequenza di attività
- Ridimensionare la finestra dell'editor

In questa modalità di sola lettura non è possibile apportare modifiche, inclusa la copia di un passaggio o una condizione. Questa azione non blocca inoltre la sequenza di attività per la modifica. Per altre informazioni su questi blocchi, vedere [recuperare il blocco per la modifica delle sequenze di attività](#bkmk_sedo).

Per apportare modifiche a una sequenza di attività, chiudere l'editor della sequenza di attività aperta in modalità di sola lettura. [Modificare](#bkmk_edit) quindi la sequenza di attività.

> [!NOTE]  
> Quando si visualizza o modifica una sequenza di attività creata con la Creazione guidata della sequenza di attività, il nome del passaggio può indicare l'azione o il tipo di passaggio. Ad esempio, è possibile che venga visualizzato un passaggio denominato "Disco di partizione 0" che è l'azione per un passaggio di tipo [Formato e disco partizione](/sccm/osd/understand/task-sequence-steps#BKMK_FormatandPartitionDisk). Tutti i passaggi della sequenza di attività sono documentati in base al *tipo*, non necessariamente in base al nome del passaggio visualizzato dall'editor.  

## <a name="bkmk_edit"></a> Modificare una sequenza di attività

Usare la procedura seguente per modificare una sequenza di attività esistente:  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e quindi selezionare il nodo **Sequenze di attività**.  

2. Nell'elenco **Sequenza di attività** selezionare la sequenza di attività da modificare.  

3. Nella scheda **Home** della barra multifunzione selezionare **Modifica** nel gruppo **Sequenza di attività**. Eseguire quindi una delle operazioni seguenti:  

    - **Aggiungere un passaggio**: selezionare **Aggiungi**, selezionare una categoria e quindi selezionare il passaggio da aggiungere. Ad esempio, per aggiungere il passaggio [Esegui riga di comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine), selezionare **Aggiungi**, scegliere la categoria **Generale** e quindi selezionare **Esegui riga di comando**. Questa azione aggiunge il passaggio dopo il passaggio attualmente selezionato.

    - **Aggiungere un gruppo**: selezionare **Aggiungi**, quindi scegliere **nuovo gruppo**. Dopo aver aggiunto un gruppo, aggiungervi passaggi.  

    - **Modificare l'ordine**: selezionare il passaggio o il gruppo che si desidera riordinare. Usare quindi le icone **Sposta su** o **Sposta giù** . È possibile spostare solo un passaggio o un gruppo alla volta. Queste azioni sono disponibili anche quando si fa clic con il pulsante destro del mouse su un gruppo o un passaggio.

        È possibile tagliare, copiare e incollare un gruppo o un passaggio. Fare clic con il pulsante destro del mouse sull'elemento e selezionare l'azione. È anche possibile usare i tasti di scelta rapida standard per ogni azione:

        - Taglia: **CTRL** + **X**
        - Copia: **CTRL** + **C**
        - Incolla: **CTRL** + **V**

    - **Rimuovere un passaggio o un gruppo**: selezionare il passaggio o il gruppo e scegliere **Rimuovi**.  

4. Selezionare **OK** per salvare le modifiche e chiudere la finestra. Selezionare **Annulla** per annullare le modifiche e chiudere la finestra. Selezionare **Applica** per salvare le modifiche e mantenere aperto l'editor della sequenza di attività.  

Per un elenco dei passaggi della sequenza di attività disponibili, vedere [Passaggi della sequenza di attività](/sccm/osd/understand/task-sequence-steps).  

> [!IMPORTANT]  
> Se la sequenza di attività include riferimenti non associati a un oggetto come risultato della modifica, l'editor richiede di correggere il riferimento prima di chiudere. Le azioni possibili includono:  
>
> - Correggere il riferimento
> - Eliminare l'oggetto senza riferimenti dalla sequenza di attività  
> - Disabilitare temporaneamente il passaggio della sequenza di attività non riuscito fino alla correzione o rimozione del riferimento interrotto  

È possibile aprire più di un'istanza dell'editor della sequenza di attività nello stesso momento. Questo comportamento consente di confrontare più sequenze di attività o di copiare e incollare i passaggi tra di essi. È possibile **modificare** una sequenza di attività e **visualizzarne** un'altra, ma non è possibile eseguire entrambe le azioni nella stessa sequenza di attività.

## <a name="bkmk_conditions"></a> Condizioni

Utilizzare le condizioni per controllare il comportamento della sequenza di attività. Aggiungere condizioni a un singolo passaggio o a un gruppo di passaggi. La sequenza di attività valuta le condizioni prima di eseguire il passaggio sul dispositivo. Esegue il passaggio solo se le condizioni restituiscono true. Se una condizione restituisce false, la sequenza di attività ignora il gruppo o il passaggio.

Usare la scheda **Opzioni** per gestire le condizioni:

![Gestire le condizioni nella scheda Opzioni dell'editor della sequenza di attività](media/4621098-copy-paste-ts-condition.png)

Sono disponibili i seguenti tipi di condizioni:

- **Istruzione If**: usare un'istruzione *if* per raggruppare le condizioni. È possibile valutare **tutte le condizioni**, **qualsiasi condizione**o **Nessuna**.

- **Variabile della sequenza di attività**. Valutare il valore corrente di qualsiasi variabile predefinita della [sequenza di attività](/sccm/osd/understand/task-sequence-variables) , azione, personalizzata o di sola lettura nell'ambiente della sequenza di attività. Per altre informazioni, vedere [condizioni](/sccm/osd/understand/using-task-sequence-variables#bkmk_access-condition)per i passaggi.

    > [!NOTE]
    > In questa condizione è possibile usare una variabile di matrice, ma è necessario specificare il membro della matrice specifico. Ad esempio, `OSDAdapter0EnableDHCP` specifica se la *prima* scheda di rete Abilita DHCP. Per altre informazioni, vedere [Variabili di matrice](/sccm/osd/understand/using-task-sequence-variables#bkmk_array).

- **Versione del sistema operativo**: valutare la versione del sistema operativo del dispositivo in cui viene eseguita la sequenza di attività. Questo elenco è la versione generale del sistema operativo usata in Configuration Manager. Per valutare una versione del sistema operativo più dettagliata, ad esempio una versione specifica di Windows 10, usare la condizione **query WMI** .

- **Lingua del sistema operativo**: valutare la lingua del sistema operativo del dispositivo in cui viene eseguita la sequenza di attività. Questo elenco include le lingue 257 supportate da Windows.

- **Proprietà file**: consente di valutare la versione o il timestamp di qualsiasi file nel dispositivo in cui viene eseguita la sequenza di attività.

- **Proprietà cartella**: valutare il timestamp di qualsiasi cartella nel dispositivo in cui viene eseguita la sequenza di attività.

- **Impostazione del registro di sistema**: valutare qualsiasi valore della chiave del registro di sistema del dispositivo in cui viene eseguita la sequenza di attività.

- **Query WMI**: specificare lo spazio dei nomi e la query da valutare nel dispositivo in cui viene eseguita la sequenza di attività.

- **Software installato**: specificare un file di Windows Installer per caricare le informazioni sul prodotto in modo che corrispondano al dispositivo in cui viene eseguita la sequenza di attività. È possibile trovare una corrispondenza con un prodotto specifico o qualsiasi versione del prodotto.

### <a name="copy-and-paste-conditions"></a>Condizioni di copia e incolla

<!-- 4621098 -->

Per riutilizzare le condizioni da un passaggio a un altro, a partire dalla versione 1910 è ora possibile copiare e incollare le condizioni nell'editor della sequenza di attività. Selezionare una condizione per tagliarla o copiarla. Se una condizione include elementi figlio, viene copiato l'intero blocco. Se negli Appunti è presente una condizione, è possibile incollarla con le opzioni seguenti:

- Incolla prima
- Incolla dopo
- Incolla sotto (si applica solo alle condizioni annidate)

Usare i tasti di scelta rapida standard per copiare (**CTRL** + **C**) e tagliare (**CTRL** + **X**). Il tasto di scelta rapida standard **CTRL** + **V** esegue l'operazione **Incolla dopo**.

Sono anche disponibili nuove opzioni per spostare le condizioni verso l'alto o verso il basso nell'elenco.

> [!Note]  
> È possibile copiare e incollare le condizioni tra i passaggi in una sequenza di attività. Questa azione non è supportata tra sequenze di attività diverse.

## <a name="bkmk_sedo"></a>Recupera blocco per la modifica

<!--3699337-->
Se la console di Configuration Manager non risponde, può essere bloccata la possibilità di apportare ulteriori modifiche fino al termine del blocco, dopo 30 minuti. Questo blocco fa parte del sistema di Configuration Manager SEDO (modifica serializzata di Distributed Objects). Per altre informazioni, vedere [Configuration Manager SEDO](/sccm/develop/core/understand/sedo).

A partire dalla versione 1906, è possibile cancellare il blocco su una sequenza di attività. Questa azione si applica solo al proprio account utente che ha il blocco e allo stesso dispositivo da cui il sito ha concesso il blocco. Quando si tenta di accedere a una sequenza di attività bloccata, è ora possibile **rimuovere le modifiche**e continuare a modificare l'oggetto. Queste modifiche andrebbero perse comunque al termine del blocco.

> [!TIP]
> A partire dalla versione 1910, è possibile cancellare il blocco su qualsiasi oggetto nella console di Configuration Manager. Per altre informazioni, vedere [Uso della console di Configuration Manager](/configmgr/core/servers/manage/admin-console#bkmk_sedo).<!--4786915-->

## <a name="bkmk_search"></a> Ricerca

<!-- 4621085 -->

Se si ha una sequenza di attività di grandi dimensioni con molti gruppi e passaggi, può essere difficile individuare passaggi specifici. A partire dalla versione 1910, è ora possibile eseguire ricerche nell'editor della sequenza di attività. Questa azione consente di individuare più rapidamente i passaggi in una sequenza di attività.

![Ricerca nell'editor delle sequenze di attività](media/4621085-task-sequence-search.png)

Immettere un termine di ricerca da avviare. È possibile definire l'ambito della ricerca usando i tipi seguenti:

- Nome del passaggio
- Descrizione del passaggio
- Tipo del passaggio
- Nome del gruppo
- Descrizione del gruppo
- Nome della variabile
- Condizioni
- Altro contenuto, ad esempio stringhe quali valori di variabili o righe di comando

Per impostazione predefinita, tutti gli ambiti sono abilitati.

È anche possibile filtrare tutti i passaggi con gli attributi seguenti:

- Continua in caso di errore
- Presenza di condizioni

Non Abilita i filtri per impostazione predefinita.

Quando si esegue la ricerca, la finestra dell'editor evidenzia in giallo i passaggi che soddisfano i criteri di ricerca.

Accedere rapidamente ai campi di ricerca ed esplorare i risultati della ricerca con i tasti di scelta rapida seguenti:

- **CTRL** + **F**: immissione di una stringa di ricerca
- **CTRL** + **O**: selezione delle opzioni di ricerca per definire l'ambito dei risultati
- **F3** o **Invio**: avanzamento attraverso i risultati
- **MAIUSC** + **F3**: arretramento attraverso i risultati

## <a name="see-also"></a>Vedere anche

- [Gestire e creare le sequenze di attività](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks)

- [Informazioni sui passaggi della sequenza di attività](/sccm/osd/understand/task-sequence-steps)

- [Come usare le variabili della sequenza di attività](/sccm/osd/understand/using-task-sequence-variables)

- [Uso della console di Configuration Manager](/sccm/core/servers/manage/admin-console)
