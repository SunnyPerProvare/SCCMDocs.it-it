1.  Nella console di Configuration Manager passare a **Raccolta software** > **Aggiornamenti software**.  

2.  Scegliere l'aggiornamento software da scaricare usando uno dei seguenti metodi:  

    -   Selezionare uno o più gruppi di aggiornamenti software da **Gruppi di aggiornamenti software**e quindi nella scheda **Home** del **Gruppo di aggiornamento** fare clic su **Scarica**.  

    -   Selezionare uno o più aggiornamenti software da **Tutti gli aggiornamenti software**e quindi nella scheda **Home** del **Gruppo di aggiornamento** fare clic su **Scarica**.  

        > [!NOTE]  
        >  Nel nodo **Tutti gli aggiornamenti software** Configuration Manager visualizza solo gli aggiornamenti software con classificazione **Critico** e **Sicurezza** rilasciati negli ultimi 30 giorni.  

        > [!TIP]  
        >  Fare clic su **Aggiungi criteri** per filtrare gli aggiornamenti software visualizzati nel nodo **Tutti gli aggiornamenti software** , salvare i criteri di ricerca usati di frequenza e quindi gestire le ricerche salvate nella scheda **Cerca** .  

         Viene visualizzato il **Download guidato degli aggiornamenti software** .  

3.  Nella pagina **Pacchetto di distribuzione** , configurare le seguenti impostazioni:  

    1.  **Seleziona pacchetto di distribuzione**: scegliere questa impostazione per selezionare un pacchetto di distribuzione esistente per gli aggiornamenti software nella distribuzione.  

        > [!NOTE]  
        >  Gli aggiornamenti software già scaricati nel pacchetto di distribuzione selezionato non verranno scaricati nuovamente.  

    2.  **Creare un nuovo pacchetto di distribuzione**: selezionare questa impostazione per creare un nuovo pacchetto di distribuzione per gli aggiornamenti software nella distribuzione. Configurare le seguenti impostazioni:  

        -   **Nome**: specifica il nome del pacchetto di distribuzione. Il pacchetto deve avere un nome univoco che descrive brevemente il contenuto del pacchetto.  Deve essere lungo massimo 50 caratteri.  

        -   **Descrizione**: specifica la descrizione del pacchetto di distribuzione. La descrizione del pacchetto fornisce informazioni sui contenuti del pacchetto e deve essere lunga massimo 127 caratteri.  

        -   **Origine pacchetto**: specifica il percorso dei file di origine dell'aggiornamento software. Digitare un percorso di rete per il percorso di origine, ad esempio **\\\server\nomecondivisione\percorso**oppure fare clic su **Sfoglia** per trovare il percorso di rete. Prima di procedere alla pagina successiva, è necessario creare la cartella condivisa per i file di origine del pacchetto di distribuzione.  

            > [!NOTE]  
            >  Il percorso di origine del pacchetto di distribuzione specificato non può essere usato da un altro pacchetto di distribuzione software.  

            > [!IMPORTANT]  
            >  L'account computer del provider SMS e l'utente che esegue la procedura guidata per scaricare gli aggiornamenti software devono disporre entrambi delle autorizzazioni NTFS di **Scrittura** nel percorso download. È necessario limitare con attenzione l'accesso al percorso download per ridurre il rischio di manomissioni da parte di utenti malintenzionati dei file origine degli aggiornamenti software.  

            > [!IMPORTANT]  
            >  È possibile modificare il percorso di origine del pacchetto nelle proprietà del pacchetto di distribuzione dopo che Configuration Manager ha creato il pacchetto di distribuzione. Ma in tal caso, è prima necessario copiare il contenuto dall'origine del pacchetto originale nel nuovo percorso di origine del pacchetto.  

     Fare clic su **Avanti**.  

4.  Nella pagina **Punti di distribuzione** specificare i punti di distribuzione o i gruppi di punti di distribuzione che ospiteranno i file di aggiornamento software e fare clic su **Avanti**. Per altre informazioni sui punti di distribuzione, vedere [Configurazioni dei punti di distribuzione](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!NOTE]  
    >  La pagina Punti di distribuzione è disponibile solo quando si crea un nuovo pacchetto di distribuzione degli aggiornamenti software.  

6.  Nella pagina **Impostazioni distribuzione** specificare le impostazioni seguenti:  

    -   **Priorità di distribuzione**: usare questa impostazione per specificare la priorità di distribuzione per il pacchetto di distribuzione. La priorità di distribuzione si applica quando il pacchetto di distribuzione viene inviato ai punti di distribuzione nei siti figlio. I pacchetti di distribuzione vengono inviati in ordine di priorità: **Alta**, **Media**o **Bassa**. I pacchetti con priorità identiche vengono inviati nell'ordine in cui sono stati creati. Se non esiste nessun backlog, il pacchetto eseguirà l'elaborazione immediatamente indipendentemente dalla relativa priorità. Per impostazione predefinita, i pacchetti vengono inviati usando la priorità **Media** .  

    -   **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti**: usare questa impostazione per attivare la distribuzione del contenuto su richiesta nei punti di distribuzione preferiti. Quando è abilitata questa impostazione, il punto di gestione crea un trigger affinché Distribution Manager distribuisca il contenuto in tutti i punti di distribuzione preferiti quando un client richiede il contenuto per il pacchetto e il contenuto non è disponibile in nessuno dei punti di distribuzione preferiti. Per altre informazioni sui punti di distribuzione preferiti e sul contenuto su richiesta, vedere [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

    -   **Impostazioni punto di distribuzione pre-installazione**: usare questa impostazione per specificare come distribuire il contenuto nei punti di distribuzione pre-installati. Scegliere una delle seguenti opzioni:  

        -   **Scarica automaticamente il contenuto quando i pacchetti sono assegnati ai punti di distribuzione**: usare questa impostazione per ignorare le impostazioni di pre-installazione e distribuire il contenuto nel punto di distribuzione.  

        -   **Scarica solo le modifiche di contenuto nel punto di distribuzione**: usare questa impostazione per pre-installare il contenuto iniziale nel punto di distribuzione, quindi distribuire le modifiche di contenuto nel punto di distribuzione.  

        -   **Copia manualmente il contenuto del pacchetto nel punto di distribuzione**: usare questa impostazione per pre-installare sempre il contenuto nel punto di distribuzione. Questa è l'impostazione predefinita.  

         Per altre informazioni sulla pre-installazione di contenuto nei punti di distribuzione, vedere [Use Prestaged content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage) (Usare contenuti in versione di preproduzione).  

     Fare clic su **Avanti**.  

6.  Nella pagina **Percorso download** specificare il percorso che verrà usato da Configuration Manager per scaricare i file di origine degli aggiornamenti software. Se necessario, usare le seguenti opzioni:  

    -   **Scarica aggiornamenti software da Internet**: selezionare questa impostazione per scaricare gli aggiornamenti software dal percorso su Internet. Questa è l'impostazione predefinita.  

    -   **Scarica aggiornamenti software da un percorso sulla rete locale**: selezionare questa impostazione per scaricare gli aggiornamenti software da una cartella locale o una cartella di rete condivisa. Usare questa impostazione quando il computer che esegue la procedura guidata non dispone di accesso a Internet.  

        > [!NOTE]  
        >  Quando si usa questa impostazione, scaricare gli aggiornamenti software da un computer qualsiasi con accesso Internet, quindi copiare gli aggiornamenti software in un percorso nella rete locale che sia accessibile dal computer che esegue la procedura guidata.  

     Fare clic su **Avanti**.  

7.  Nella pagina **Selezione lingua** specificare le lingue per cui vengono scaricati gli aggiornamenti software selezionati e fare clic su **Avanti**. Configuration Manager scarica gli aggiornamenti software solo se sono disponibili nelle lingue selezionate. Gli aggiornamenti software non specifici per la lingua vengono sempre scaricati.  

8. Nella pagina **Riepilogo** verificare le impostazioni selezionate nella procedura guidata e fare clic su **Avanti** per scaricare gli aggiornamenti software.  

9. Nella pagina **Completamento** verificare che gli aggiornamenti software siano stati scaricati correttamente e fare clic su **Chiudi**.  


<!--HONumber=Nov16_HO1-->


