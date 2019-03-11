---
title: Messaggi di stato
titleSuffix: Configuration Manager
description: Descrizioni dei messaggi di stato nelle versioni supportate di Configuration Manager.
ms.date: 02/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f04c0a71-57bc-4443-a47c-592373050d04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9e3a30211b95e483b30caf1507b74a7737d156bb
ms.sourcegitcommit: 223549003829fce7c6dc63959ee71e8b88542417
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/27/2019
ms.locfileid: "56951869"
---
# <a name="state-messages-in-configuration-manager"></a>Messaggi di stato in Configuration Manager 

*Si applica a: System Center Configuration Manager (Current Branch)*

I messaggi di stato contengono informazioni sintetiche sulle condizioni nel client di Configuration Manager. Il sistema di messaggistica di stato viene usato da componenti specifici di Configuration Manager, ad esempio aggiornamenti software e impostazioni di configurazione.

I client di Configuration Manager inviano messaggi di stato ai sistemi del sito del punto di stato di fallback o del punto di gestione per segnalare lo stato corrente delle operazioni. È possibile creare report per visualizzare i messaggi di stato inviati dai client di Configuration Manager.

Ogni funzionalità di Configuration Manager che usa i messaggi di stato viene identificata in base al tipo di argomento del messaggio di stato. I tipi di argomento del messaggio di stato elencati in questo articolo possono essere usati per definire la funzionalità di Configuration Manager a cui è correlato un messaggio di stato.

> [!NOTE]  
> Il valore zero (0) per un ID del messaggio di stato indica in genere che il tipo di argomento è in uno stato sconosciuto.

## <a name="300-statetopictypesumassignmentcompliance"></a>300 STATE_TOPICTYPE_SUM_ASSIGNMENT_COMPLIANCE

|      ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|       0   | Stato di conformità sconosciuto|
|   1   | conformi | 
|   2   | Non conformi | 

## <a name="301-statetopictypesumassignmentenforcement"></a>301 STATE_TOPICTYPE_SUM_ASSIGNMENT_ENFORCEMENT

|       ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   0    | Stato dell'applicazione sconosciuto |
|   1    | Installazione degli aggiornamenti        | 
|   2    | In attesa del riavvio              | 
|   3    | In attesa del completamento di un'altra installazione         | 
|   4    | Installazione dell'aggiornamento completata(2)             | 
|   5    | Riavvio del sistema in sospeso           | 
|   6    | Impossibile installare gli aggiornamenti          | 
|   7    | Download degli aggiornamenti in corso   | 
|   8    | Aggiornamenti scaricati    | 
|   9    | Impossibile scaricare gli aggiornamenti     | 
|   10   | In attesa della finestra di manutenzione prima dell'installazione         | 
|   11   | In attesa di orchestrazione            | 

## <a name="302-statetopictypesumassignmentevaluation"></a>302 STATE_TOPICTYPE_SUM_ASSIGNMENT_EVALUATION

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|      
|0|        Stato della valutazione sconosciuto|                 
|   1    |Valutazione attivata       |
|   2    |Valutazione riuscita      |
|   3    |Valutazione non riuscita         |


## <a name="400-statetopictypesumcidetection"></a>400 STATE_TOPICTYPE_SUM_CI_DETECTION

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 0  | Stato del rilevamento sconosciuto|
|   1|  Non richiesto      |
|   2|  Non rilevato          |
|   3|  Rilevato      |

## <a name="401-statetopictypesumcicompliance"></a>401 STATE_TOPICTYPE_SUM_CI_COMPLIANCE

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|0| Stato di conformità sconosciuto|
|   1   |conformi         |
|   2   |Non conformi         |
|   3   |Rilevato conflitto     |
|   4   |Errore             |
|   5   |Sconosciuto           |
|   6   |Conformità parziale   |
|   7   |Conformità non configurata     |

## <a name="402-statetopictypesumcienforcement"></a>402 STATE_TOPICTYPE_SUM_CI_ENFORCEMENT

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 0 | Stato dell'applicazione sconosciuto|
|   1   |Applicazione avviata                   |
|   2   |Applicazione in attesa del contenuto               |
|   3   | In attesa del completamento di un'altra installazione         |
|   4   |In attesa della finestra di manutenzione prima dell'installazione              |
|   5   |Riavvio richiesto prima dell'installazione            |
|   6   |Errore generale           |
|   7   |Installazione in sospeso              |
|   8   |Installazione dell'aggiornamento                 |
|   9   |Riavvio del sistema in sospeso        |
|   10  |Installazione dell'aggiornamento completata             |
|   11  |Impossibile installare l'aggiornamento          |
|   12  |Download dell'aggiornamento in corso        |
|   13  | Aggiornamento scaricato        |
|   14  |Impossibile scaricare l'aggiornamento         |

## <a name="500-statetoptctypesumupdatedetection"></a>500 STATE_TOPTCTYPE_SUM_UPDATE_DETECTION

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|0 |Stato del rilevamento sconosciuto|
|   1   | Aggiornamento non richiesto     |
|   2   | Aggiornamento richiesto         |
|   3   | Aggiornamento installato    |

## <a name="501-statetopictypesumupdatesourcescan"></a>501 STATE_TOPICTYPE_SUM_UPDATE_SOURCE_SCAN

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|0 |Stato dell'analisi sconosciuto|
|   1   | Analisi in attesa di contenuto        |
|   2   | Analisi in corso            |
|   3   | Analisi completata          |
|   4   | Nuovo tentativo di analisi in sospeso      |
|   5   | Analisi non riuscita        |
|   6   | Analisi completata con errori |

## <a name="700-statetopictyperesyncstatemsg"></a>700 STATE_TOPICTYPE_RESYNC_STATE_MSG

    No State IDs.

## <a name="701-statetopictypesystemheartbeat"></a>701 STATE_TOPICTYPE_SYSTEM_HEARTBEAT

    No State IDs.

## <a name="702-statetopictypeckdupdate"></a>702 STATE_TOPICTYPE_CKD_UPDATE
 
    No State IDs.

## <a name="800-statetopictypeclientdeployment"></a>800 STATE_TOPICTYPE_CLIENT_DEPLOYMENT

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   100 |Distribuzione di client avviata             |          
|   101 |In attesa del download                  |          
|   102 |Distribuzione pianificata                  |          
|   103 | In attesa della finestra prima della distribuzione |
|   104 |Distribuzione ignorata                |          
|   301 |Errore di distribuzione client sconosciuto |          
|   302 |Non è stato possibile creare il servizio ccmsetup  |         
|   303 |Non è stato possibile eliminare il servizio ccmsetup |          
|   304 |Impossibile eseguire l'installazione sul sistema operativo integrato con il filtro di scrittura basato su file abilitato sull'unità di sistema |          
|   305 |La modalità di protezione nativa non è valida in Windows 2000  |         
|   306 |Non è stato possibile avviare il processo di download di ccmsetup  |         
|   307 |Riga di comando di ccmsetup non valida |        
|   308 |Non è stato possibile scaricare il file tramite WINHTTP all'indirizzo |        
|   309 |Non è stato possibile scaricare i file tramite BITS all'indirizzo |       
|   310 |Non è stato possibile installare la versione BITS |         
|   311 |Impossibile verificare se il file di prerequisiti è firmato MS  |          
|   312 |Non è stato possibile copiare il file perché il disco è pieno |       
|   313 |Installazione di Client.msi non riuscita con errore MSI |          
|   314 |Non è stato possibile caricare il file manifesto ccmsetup.xml |          
|   315 |Non è stato possibile ottenere il certificato client  |         
|   316 |Il file di prerequisiti non è firmato da MS |         
|   317 |Per completare l'installazione, è necessario riavviare il computer  |          
|   318 |Impossibile installare il client su MP. Le versioni client e MP non corrispondono |        
|   319 |Sistema operativo o Service Pack non supportato  |        
|   320 |La distribuzione non è supportata                  |          
|   321 |BITS mancante                      |          
|   322 |Cartella di origine non disponibile                  |          
|   323 |Appv non supportato                    |          
|   324 |Versione del sito non corretta                    |          
|   325 |Mancata corrispondenza hash dei prerequisiti                |          
|   326 |Annullamento della registrazione di MDM non riuscito             |          
|   327 |Rilevata registrazione MDM             |          
|   328 |Rilevato Intune                   |          
|   329 |Rete a consumo non consentita            |          
|   400 |Distribuzione client completata |  
|   401 |Distribuzione client riuscita. Richiesto riavvio.          |          
|   402 |Distribuzione riuscita. Il riavvio ha avuto esito positivo.         |
|   500 |Assegnazione client avviata|
|   601 |Errore di assegnazione client sconosciuto|
|   602 |Il codice del sito seguente non è valido|
|   603 |L'assegnazione al Management Pack non è riuscita|
|   604 |Non è stato possibile individuare il punto di gestione predefinito|
|   605 |Non è stato possibile scaricare il certificato di firma del sito|
|   606 |Non è stato possibile individuare automaticamente il codice del sito|
|   607 |Assegnazione del sito non riuscita. La versione del client è superiore alla versione del sito.|
|   608 |Non è stato possibile ottenere la versione del sito da Active Directory e SLP|
|   609 |Non è stato possibile ottenere la versione client|
|   700 |Assegnazione client completata|

## <a name="801-statetopictypedeviceclientdeployment"></a>801 STATE_TOPICTYPE_DEVICE_CLIENT_DEPLOYMENT

    No State IDs.

## <a name="810-statetopictypeclientcomanagement"></a>810 STATE_TOPICTYPE_CLIENT_COMANAGEMENT

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   100 | Stato registrazione         |
|   101 | Registrazione pianificata          |
|   102 | Registrazione annullata           |
|   105 | Registrazione avviata            |
|   106 | Registrazione riuscita ma senza provisioning   
|   107 | Registrazione riuscita e provisioning eseguito   
|   108 | Registrazione - nessun utente attivo         |
|   110 | Registrazione non riuscita         |


## <a name="820--statetopictypeclientwufb"></a>820  STATE_TOPICTYPE_CLIENT_WUFB

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   1   | Stato client Windows Update per le aziende| 

## <a name="900-statetopictypebranchdp"></a>900 STATE_TOPICTYPE_BRANCH_DP

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   1   | Spazio su disco      | 

## <a name="901-statetopictyperemotedpmonitoring"></a>901 STATE_TOPICTYPE_REMOTE_DP_MONITORING

    No State IDs.

## <a name="902-statetopictypepulldpmonitoring"></a>902 STATE_TOPICTYPE_PULL_DP_MONITORING

    No State IDs.

## <a name="903-statetopictypedpusage"></a>903 STATE_TOPICTYPE_DP_USAGE

    No State IDs.

## <a name="1000--statetopictypeclientframeworkcomm"></a>1000  STATE_TOPICTYPE_CLIENT_FRAMEWORK_COMM

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   1      | Comunicazione del client con il punto di gestione riuscita |
|   2      | Impossibile per il client comunicare con il punto di gestione |

## <a name="1001-statetopictypeclientframeworklocal"></a>1001 STATE_TOPICTYPE_CLIENT_FRAMEWORK_LOCAL

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   1   |Recupero da parte del client di un certificato dall'archivio certificati locale riuscito       |
|   2   |Impossibile per il client recuperare un certificato dall'archivio certificati locale |

## <a name="1002-statetopictypedeviceclientframeworkcomm"></a>1002 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_COMM

    No State IDs.

## <a name="1003-statetopictypedeviceclientframeworklocal"></a>1003 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_LOCAL

    No State IDs.

## <a name="1004-statetopictypedeviceclientframeworkcertificate"></a>1004 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_CERTIFICATE

    No State IDs.

## <a name="1005-statetopictypedeviceclientwipe"></a>1005 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE

    No State IDs.

## <a name="1006-statetopictypedeviceclientretire"></a>1006 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE

    No State IDs.

## <a name="1007-statetopictypedeviceclientwipeintune"></a>1007 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE_INTUNE

    No State IDs.

## <a name="1008-statetopictypedeviceclientretireintune"></a>1008 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE_INTUNE

    No State IDs.

## <a name="1009-statetopictypedeviceclientdevicelock"></a>1009 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK

    No State IDs.

## <a name="1010-statetopictypedeviceclientdevicelockintune"></a>1010 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK_INTUNE

    No State IDs.

## <a name="1011-statetopictypedeviceclientdevicepinreset"></a>1011 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET

    No State IDs.

## <a name="1012-statetopictypedeviceclientdevicepinresetintune"></a>1012 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_INTUNE

    No State IDs.

## <a name="1013-statetopictypedeviceclientdevicepinresetonprem"></a>1013 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_ONPREM

    No State IDs.

## <a name="1014-statetopictypedeviceclientdevicealbypass"></a>1014 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS

    No State IDs.

## <a name="1015-statetopictypedeviceclientdevicealbypassintune"></a>1015 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS_INTUNE

    No State IDs.

## <a name="1100-statetopictypeclientframeworkmodereadiness"></a>1100 STATE_TOPICTYPE_CLIENT_FRAMEWORK_MODEREADINESS

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   1   |Client non pronto per la modalità nativa  |
|   2   |Client pronto per la modalità nativa       |


## <a name="1300-statetopictypeclienthealth"></a>1300 STATE_TOPICTYPE_CLIENT_HEALTH

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   1   |   Operazione completata|    
|   2   |   Operazione non riuscita |    

## <a name="1401-statetopictypestatereport"></a>1401 STATE_TOPICTYPE_STATE_REPORT

    No State IDs.

## <a name="1500-statetopictypecaltrackut"></a>1500 STATE_TOPICTYPE_CAL_TRACK_UT

    No State IDs.

## <a name="1502-statetopictypecaltrackmt"></a>1502 STATE_TOPICTYPE_CAL_TRACK_MT

    No State IDs.

## <a name="1503-statetopictypecaltrackml"></a>1503 STATE_TOPICTYPE_CAL_TRACK_ML

    No State IDs.   

## <a name="1600-statetopictypeuseraffinity"></a>1600 STATE_TOPICTYPE_USER_AFFINITY

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   1   |Affinità utente impostata        |
|   2   |Affinità utente rimossa        |

## <a name="1700-statetopictypeappciscan"></a>1700 STATE_TOPICTYPE_APP_CI_SCAN

    No State IDs.

## <a name="1701-statetopictypeappcicompliance"></a>1701 STATE_TOPICTYPE_APP_CI_COMPLIANCE

    No State IDs.

## <a name="1702-statetopictypeappcienforcement"></a>1702 STATE_TOPICTYPE_APP_CI_ENFORCEMENT

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   1000    |Esito positivo dell'elemento di configurazione                      |
|   1001    |Esito positivo dell'elemento di configurazione - già installato            |
|   1002    |Esito positivo dell'elemento di configurazione - stato preliminare                |
|   1003    |Esito positivo stato rapido elemento di configurazione                  |
|   2000    |Elemento di configurazione in corso                    |
|   2001    |Elemento di configurazione in corso - in attesa del contenuto            |
|   2002    |Elemento di configurazione in corso - installazione                 |
|   2003    |Elemento di configurazione in corso - in attesa del riavvio             |
|   2004    |Elemento di configurazione in corso - in attesa della finestra di manutenzione         |
|   2005    |Elemento di configurazione in corso - in attesa della pianificazione               |
|   2006    |Elemento di configurazione in corso - download di contenuto dipendente     |
|   2007    |Elemento di configurazione in corso - installazione delle dipendenze        |
|   2008    |Elemento di configurazione in corso - riavvio in sospeso             |
|   2009    |Elemento di configurazione in corso - contenuto scaricato             |
|   2010    |Elemento di configurazione in corso - aggiornamento in sospeso             |
|   2011    |Elemento di configurazione in corso - in attesa della riconnessione dell'utente         |
|   2012    |Elemento di configurazione in corso - in attesa della disconnessione dell'utente              |
|   2013    |Elemento di configurazione in corso - in attesa dell'accesso dell'utente               |
|   2014    |Elemento di configurazione in corso - in attesa dell'installazione            |
|   2015    |Elemento di configurazione in corso - in attesa di ripetizione dei tentativi              |
|   2016    |Elemento di configurazione in corso - in attesa di presmode               |
|   2017    |Elemento di configurazione in corso - in attesa dell'orchestrazione          |
|   2018    |Elemento di configurazione in corso - in attesa della rete            |
|   2019    |Elemento di configurazione in corso - aggiornamento VE in sospeso              |
|   2020    |Elemento di configurazione in corso -aggiornamento VE in corso            |
|   3000    |Requisiti dell'elemento di configurazione non soddisfatti                       |
|   3001    |Requisiti dell'elemento di configurazione non soddisfatti - host non applicabile           |
|   4000    |Elemento di configurazione sconosciuto                    |
|   5000    |Errore dell'elemento di configurazione                          |
|   5001    |Errore dell'elemento di configurazione durante la valutazione                   |
|   5002    |Errore dell'elemento di configurazione durante l'installazione                   |
|   5003    |Errore dell'elemento di configurazione durante il recupero del contenuto               |
|   5004    |Errore dell'elemento di configurazione durante l'installazione delle dipendenze            |
|   5005    |Errore dell'elemento di configurazione durante il recupero delle dipendenze del contenuto        |
|   5006    |Errore dell'elemento di configurazione - conflitto delle regole                   |
|   5007    |Errore dell'elemento di configurazione - in attesa di un nuovo tentativo                |
|   5008    |Errore dell'elemento di configurazione - disinstallazione della sostituzione        |
|   5009    |Errore dell'elemento di configurazione - download sostituito               |
|   5010    |Errore dell'elemento di configurazione - aggiornamento VE                  |
|   5011    |Errore dell'elemento di configurazione - installazione della licenza               |
|   5012    |Errore dell'elemento di configurazione durante il recupero di tutte le app attendibili       |
|   5013    |Errore dell'elemento di configurazione - nessuna licenza disponibile            |
|   5014    |Errore dell'elemento di configurazione - sistema operativo non supportato                 |
|   6000    |Esito positivo dell'avvio dell'elemento di configurazione                           |
|   6010    |Errore di avvio dell'elemento di configurazione                           |
|   6020    |Avvio dell'elemento di configurazione sconosciuto|

## <a name="1703-statetopictypeappciassignmentevaluatio"></a>1703 STATE_TOPICTYPE_APP_CI_ASSIGNMENT_EVALUATIO

    No State IDs.

## <a name="1704-statetopictypeappcilaunch"></a>1704 STATE_TOPICTYPE_APP_CI_LAUNCH

    No State IDs.

## <a name="1800-statetopictypeeventintrinsic"></a>1800 STATE_TOPICTYPE_EVENT_INTRINSIC

    No State IDs.

## <a name="1801-statetopictypeeventextrinsic"></a>1801 STATE_TOPICTYPE_EVENT_EXTRINSIC

    No State IDs.

## <a name="1900-statetopictypeepaminfection"></a>1900 STATE_TOPICTYPE_EP_AM_INFECTION

    No State IDs.

## <a name="1901-statetopictypeepamhealth"></a>1901 State_Topictype_Ep_Am_Health

    No State IDs.

## <a name="1902-statetopictypeepmalware"></a>1902 STATE_TOPICTYPE_EP_MALWARE

    No State IDs.

## <a name="1950-statetopictypeatphealthstatus"></a>1950 STATE_TOPICTYPE_ATP_HEALTH_STATUS

    No State IDs.

## <a name="2001-statetopictypeepclientdeployment"></a>2001 STATE_TOPICTYPE_EP_CLIENT_DEPLOYMENT

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   1   |Endpoint Protection non gestito       |
|   2   |Endpoint Protection in attesa di installazione  |
|   3   |Endpoint Protection gestito         |
|   4   |Installazione di Endpoint Protection non riuscita     |
|   5   |Riavvio in sospeso di Endpoint Protection  |
|   6   |Endpoint Protection non supportato       |
|   7   |Endpoint Protection co-gestito      |

## <a name="2002-statetopictypeepclientpolicyapplication"></a>2002 STATE_TOPICTYPE_EP_CLIENT_POLICYAPPLICATION

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   0   |Stato applicazione criteri di Endpoint Protection sconosciuto        |
|   1   |Applicazione criteri di Endpoint Protection riuscita         |
|   2   |Applicazione criteri di Endpoint Protection non riuscita        |

## <a name="2003-statetopictypeclientaction"></a>2003 STATE_TOPICTYPE_CLIENT_ACTION

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   0   |  Sconosciuto           |
|   1   |  Attivo            |
|   2   |  Inactive          |

## <a name="2100-statetopictypewpclientdeployment"></a>2100 STATE_TOPICTYPE_WP_CLIENT_DEPLOYMENT

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   1   | Proxy di riattivazione non installato          |
|   2   | Proxy di riattivazione in attesa dell'installazione       |
|   3   | Proxy di riattivazione installato          |
|   4   | Installazione del proxy di riattivazione non riuscita       |
|   5   | Proxy di riattivazione in attesa del riavvio         |
|   6   | Proxy di riattivazione non è supportato in questo sistema operativo   |
|   7   | Rifiuto esplicito server proxy di riattivazione        |
|   8   | Disinstallazione di proxy di riattivazione non riuscita      |
|   9   | Runtime di proxy di riattivazione non supportato         |

## <a name="2200-statetopictypefdm"></a>2200 STATE_TOPICTYPE_FDM

    No State IDs.

## <a name="2201-statetopictypeccmcertbinding"></a>2201 STATE_TOPICTYPE_CCM_CERT_BINDING

    No State IDs.

## <a name="2202-statetopictypeserverstatistic"></a>2202 STATE_TOPICTYPE_SERVER_STATISTIC

    No State IDs.

## <a name="3000-statetopictypedmwnschannel"></a>3000 STATE_TOPICTYPE_DM_WNS_CHANNEL

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|0  | Set di canale del servizio notifica push di Windows|

## <a name="4000-statetopictypemdmdeviceproperty"></a>4000 STATE_TOPICTYPE_MDM_DEVICE_PROPERTY

    No State IDs.

## <a name="4002-statetopictypemdmclientidenitity"></a>4002 STATE_TOPICTYPE_MDM_CLIENT_IDENITITY

    No State IDs.

## <a name="4003-statetopictypemdmapplicationrequest"></a>4003 STATE_TOPICTYPE_MDM_APPLICATION_REQUEST

    No State IDs.

## <a name="4004-statetopictypemdmapplicationstate"></a>4004 STATE_TOPICTYPE_MDM_APPLICATION_STATE

    No State IDs.

## <a name="4005-statetopictypemdmlicensedevicerelation"></a>4005 STATE_TOPICTYPE_MDM_LICENSE_DEVICE_RELATION

    No State IDs.

## <a name="4006-statetopictypemdmlicensekeys"></a>4006 STATE_TOPICTYPE_MDM_LICENSE_KEYS

    No State IDs.

## <a name="4007-statetopictypemdmpolicyassignment"></a>4007 STATE_TOPICTYPE_MDM_POLICY_ASSIGNMENT

    No State IDs.

## <a name="4008-statetopictypemdmandroidcount"></a>4008 STATE_TOPICTYPE_MDM_ANDROID_COUNT

    No State IDs.

## <a name="4009-statetopictypemdmslkstatus"></a>4009 STATE_TOPICTYPE_MDM_SLK_STATUS

    No State IDs.

## <a name="4010-statetopictypemdmusercompanytermacceptance"></a>4010 STATE_TOPICTYPE_MDM_USER_COMPANY_TERM_ACCEPTANCE

    No State IDs.

## <a name="4022-statetopictypemdmdepsyncnowstatus"></a>4022 STATE_TOPICTYPE_MDM_DEP_SYNCNOW_STATUS

    No State IDs.

## <a name="4023-statetopictypemdmmamstoreappsync"></a>4023 STATE_TOPICTYPE_MDM_MAM_STORE_APP_SYNC

    No State IDs.

## <a name="5000-statetopictypecertificateenrollment"></a>5000 STATE_TOPICTYPE_CERTIFICATE_ENROLLMENT

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   1   |Richiesta di verifica rilasciata                    |
|   2   |Rilascio richiesta di verifica non riuscito              |
|   3   |La creazione della richiesta non è riuscita                 |
|   4   |Invio della richiesta non riuscito               |
|   5   |Convalida della richiesta di verifica riuscita          |
|   6   |Convalida della richiesta di verifica non riuscita             |
|   7   |Rilascio non riuscito                    |
|   8   |Rilascio in sospeso                   |
|   9   |Rilasciato                      |
|   10  |Elaborazione della risposta non riuscita          |
|   11  |Risposta in sospeso                    |
|   12  |Registrazione riuscita                    |
|   13  |Registrazione non richiesta                   |
|   14  |Revocato                         |
|   15  |Rimosso dalla raccolta                 |
|   16  |Rinnovo verificato                  |
|   17  |Installazione non riuscita              |
|   18  |Installato                   |
|   19  |Eliminazione non riuscita                   |
|   20  |Eliminato                     |
|   21  |Rinnovo richiesto               |


## <a name="5001-statetopictypecertificatecrp"></a>5001 STATE_TOPICTYPE_CERTIFICATE_CRP

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   1   |Richiesta di verifica rilasciata                       |
|   2   |Rilascio richiesta di verifica non riuscito                 |
|   3   |La creazione della richiesta non è riuscita                    |
|   4   |Invio della richiesta non riuscito                  |
|   5   |Convalida della richiesta di verifica riuscita             |
|   6   |Convalida della richiesta di verifica non riuscita                |
|   7   |Rilascio non riuscito                       |
|   8   |Rilascio in sospeso                      |
|   9   |Rilasciato                         |
|   10  |Elaborazione della risposta non riuscita             |
|   11  |Risposta in sospeso                       |
|   12  |Registrazione riuscita                       |
|   13  |Registrazione non richiesta                      |
|   14  |Revocato                            |
|   15  |Rimosso dalla raccolta                    |
|   16  |Rinnovo verificato                     |
|   17  |Installazione non riuscita                 |
|   18  |Installato                      |
|   19  |Eliminazione non riuscita                      |
|   20  |Eliminato                        |
|   21  |Rinnovo richiesto                  |

## <a name="5200-statetopictyperesourceaccessstatus"></a>5200 STATE_TOPICTYPE_RESOURCE_ACCESS_STATUS

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   1   | Configurazione del pin di stato riuscita                   |
|   2   | Configurazione del pin di stato non riuscita                  |
|   3   | Configurazione del pin di stato non supportata               |
|   4   | Configurazione del pin di stato in corso             |

## <a name="6000-statetopictyperemoteappsubscriptionstatus"></a>6000 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_STATUS

    No State IDs.

## <a name="6001-statetopictyperemoteappsubscriptionsyncstatus"></a>6001 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_SYNC_STATUS

    No State IDs.

## <a name="6002-statetopictyperemoteappauthcookiessyncstatus"></a>6002 STATE_TOPICTYPE_REMOTEAPP_AUTHCOOKIES_SYNC_STATUS

    No State IDs.

## <a name="6003-statetopictyperemoteapplicationssyncstatus"></a>6003 STATE_TOPICTYPE_REMOTEAPPLICATIONS_SYNC_STATUS

    No State IDs.

## <a name="6004-statetopictyperemoteapplockresult"></a>6004 STATE_TOPICTYPE_REMOTEAPP_LOCK_RESULT

    No State IDs.

## <a name="7000-statetopictypeusercompanytermacceptance"></a>7000 STATE_TOPICTYPE_USER_COMPANY_TERM_ACCEPTANCE

    No State IDs.

## <a name="7001-statetopictypepfxcertificate"></a>7001 STATE_TOPICTYPE_PFX_CERTIFICATE

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   1   |Richiesta di verifica rilasciata               |
|   2   |Rilascio richiesta di verifica non riuscito         |
|   3   |La creazione della richiesta non è riuscita            |
|   4   |Invio della richiesta non riuscito          |
|   5   |Convalida della richiesta di verifica riuscita     |
|   6   |Convalida della richiesta di verifica non riuscita        |
|   7   |Rilascio non riuscito               |
|   8   |Rilascio in sospeso              |
|   9   |Rilasciato                 |
|   10  |Elaborazione della risposta non riuscita     |
|   11  |Risposta in sospeso               |
|   12  |Registrazione riuscita               |
|   13  |Registrazione non richiesta              |
|   14  |Revocato                    |
|   15  |Rimosso dalla raccolta            |
|   16  |Rinnovo verificato             |
|   17  |Installazione non riuscita         |
|   18  |Installato              |
|   19  |Eliminazione non riuscita              |
|   20  |Eliminato                |
|   21  |Rinnovo richiesto          |

## <a name="7010-statetopictypeconditionalaccesscompliance"></a>7010 STATE_TOPICTYPE_CONDITIONAL_ACCESS_COMPLIANCE

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
||  1   | Conformità corretta             |
|   2   | Errore di conformità nel Management Pack      |
|   3   | Errore di conformità nel client      |
|   4   | Errore di conformità in Intune      |
|   5   | Errore di conformità in AAD         |
|   6   | Co-gestione conformità Intune       |

## <a name="7200-statetopictypesuperpeerupdatecachemap"></a>7200 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CACHE_MAP

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   1   |Origine di peer cache aggiunta                |
|   2   |Origine di peer cache rimossa          |

## <a name="7201-statetopictypesuperpeerupdateconfig"></a>7201 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CONFIG

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   1   |Origine di peer cache disattivata              |
|   2   |Origine di peer cache attiva                |

## <a name="7202-statetopictypedownloadaggregatedata"></a>7202 STATE_TOPICTYPE_DOWNLOAD_AGGREGATE_DATA
|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   1   |Caricamento dati aggregati scaricati       |

## <a name="7203-statetopictypepeersourcereqrejectionstats"></a>7203 STATE_TOPICTYPE_PEERSOURCE_REQ_REJECTION_STATS

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   1   |Caricamento dati rifiuto origine peer     |

## <a name="7300-statetopictypeproxytraffic"></a>7300 STATE_TOPICTYPE_PROXY_TRAFFIC

    No State IDs.

## <a name="7301-statetopictypeproxyconnection"></a>7301 STATE_TOPICTYPE_PROXY_CONNECTION

    No State IDs.

## <a name="7302-statetopictypesrsusagedata"></a>7302 STATE_TOPICTYPE_SRS_USAGE_DATA

    No State IDs.

## <a name="7303-statetopictypeproxytrafficidentity"></a>7303 STATE_TOPICTYPE_PROXY_TRAFFIC_IDENTITY

    No State IDs.

## <a name="8001-statetopictypehasreport"></a>8001 STATE_TOPICTYPE_HAS_REPORT

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|   1   |Attestazione dell'integrità supportata         |
|   2   |Attestazione dell'integrità non supportata         |

## <a name="statetopictypedeviceclientedplog"></a>STATE_TOPICTYPE_DEVICE_CLIENT_EDPLOG

    No State IDs.

## <a name="8003-statetopictypeenablelostmode"></a>8003 STATE_TOPICTYPE_ENABLE_LOSTMODE

    No State IDs.

## <a name="8004-statetopictypedisablelostmode"></a>8004 STATE_TOPICTYPE_DISABLE_LOSTMODE

    No State IDs.

## <a name="8005-statetopictypelocatedevice"></a>8005 STATE_TOPICTYPE_LOCATE_DEVICE

    No State IDs.

## <a name="8006-statetopictyperebootdevice"></a>8006 STATE_TOPICTYPE_REBOOT_DEVICE

    No State IDs.

## <a name="8007-statetopictypelogoutuser"></a>8007 STATE_TOPICTYPE_LOGOUTUSER

    No State IDs.

## <a name="8008-statetopictypeuserslist"></a>8008 STATE_TOPICTYPE_USERSLIST

    No State IDs.

## <a name="8009-statetopictypedeleteuser"></a>8009 STATE_TOPICTYPE_DELETEUSER

    No State IDs.

## <a name="8010-statetopictypecleanpcretaininguserdata"></a>8010 STATE_TOPICTYPE_CLEANPCRETAININGUSERDATA

    No State IDs.

## <a name="8011-statetopictypecleanpcwithoutretaininguserdata"></a>8011 STATE_TOPICTYPE_CLEANPCWITHOUTRETAININGUSERDATA

    No State IDs.

## <a name="8012-statetopictypesetdevicename"></a>8012 STATE_TOPICTYPE_SETDEVICENAME

    No State IDs.

## <a name="9000-statetopictypebookcicompliance"></a>9000 STATE_TOPICTYPE_BOOK_CI_COMPLIANCE

    No State IDs.

## <a name="9001-statetopictypebookcienforcement"></a>9001 STATE_TOPICTYPE_BOOK_CI_ENFORCEMENT

    No State IDs.

## <a name="next-steps"></a>Passaggi successivi

- [Descrizione della messaggistica di stato in Configuration Manager](https://support.microsoft.com/help/4459394/description-of-state-messaging-in-system-center-configuration-manager)
- [White paper sulla gestione degli aggiornamenti software per Configuration Manager](https://www.microsoft.com/download/details.aspx?id=44578)
