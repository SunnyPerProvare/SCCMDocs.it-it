---
title: Rischio per la compatibilità delle app di Windows
titleSuffix: Configuration Manager
description: Informazioni sui rischi di compatibilità per le app di Windows nel Desktop Analitica.
ms.date: 04/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: da0bde04e019fdf0fbb0a997be652860824270b1
ms.sourcegitcommit: 5ee9487c891c37916294bd34a10d04e398f111f7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59069399"
---
# <a name="compatibility-risk-for-windows-apps-in-desktop-analytics"></a>Rischi di compatibilità per le app di Windows nel Desktop Analitica

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Aggiornamento delle valutazioni in Analitica di Windows sono state generiche, ad esempio: Attenzione necessita o correzione disponibile. Non fornisce alcun indicatore visivo su come definire le priorità delle App con problemi o eseguire l'aggiornamento di insights. Desktop Analitica sostituisce questa funzionalità con **rischi relativi alla compatibilità**. Analitica desktop Mostra la valutazione del rischio di app per le app solo nella visualizzazione della distribuzione per uno scenario di pre-aggiornamento. Vengono suddivisi le app basate su informazioni dettagliate che ottiene Microsoft dai computer inclusi in un piano di distribuzione corrente.

Analitica desktop utilizza le seguenti categorie di rischio di compatibilità:

- **Bassa**: Trovare il servizio non segnali per mettere l'app a rischio per un Windows esegue l'aggiornamento. È probabile che funzionerà su sistema operativo di destinazione come-è.  

- **Medium**: Analitica indica che l'applicazione potrebbe avere compromesse la funzionalità, sebbene correzione è probabilmente possibile.  

- **Elevata**: L'applicazione è quasi sicuramente esito negativo durante o dopo l'aggiornamento. Potrebbe essere necessario un monitoraggio e aggiornamento.  

- **Sconosciuto**: L'app non è stata valutata dall'analizzatore dell'integrità di App. Non esistono, ad esempio nessun altro insights *problemi noti di MS* oppure *pronto per Windows*.  



## <a name="risk-assessment-engine"></a>Motore di valutazione dei rischi

Esistono varie fonti che analizzatore dell'integrità delle App Usa per generare il punteggio di rischio.

![Diagramma delle aree di motore della valutazione dei rischi analizzatore dell'integrità di App](media/aha-risk-assessment-engine.png)


### <a name="ms-known-issues"></a>Problemi noti MS

L'analizzatore dell'integrità di App è simile a livello di database di compatibilità delle app di Microsoft per problemi noti. Usa questo database per determinare eventuali blocchi di compatibilità esistenti per le applicazioni disponibili pubblicamente da Microsoft o altri server di pubblicazione. Questo controllo si applica solo al sistema operativo di destinazione per il piano di distribuzione selezionato.


### <a name="ready-for-windows"></a>Pronto per Windows

L'archivio dati pronti per Windows verifica per i blocchi di compatibilità su un dispositivo. Correla inoltre i dati da altri clienti segnalazione App simili. Microsoft Usa i dati provenienti da altri dispositivi simili in cui questa app ha segnalato alcun problema.


### <a name="app-health-analyzer-signals-for-compatibility-assessment"></a>Segnala analizzatore dell'integrità di App per la valutazione della compatibilità

Usare il toolkit di analizzatore dell'integrità di App per raccogliere altri segnali per la compatibilità dell'applicazione. Per altre informazioni, vedere [analizzatore dell'integrità App](/sccm/desktop-analytics/app-health-analyzer).

I segnali seguenti sono attualmente disponibili:

#### <a name="adopted-version-available"></a>Versione adottata disponibile

È disponibile un'altra versione dell'app che è ampiamente adottate da altri clienti. Questo segnale utilizza i dati di pronto per Windows. Se sono presenti eventuali blocchi di aggiornamento con la versione corrente, è possibile distribuire la versione alternativa invece.

#### <a name="16-bit"></a>16 bit

Rimuovere tutti i componenti di 16 bit da applicazioni e sostituire con gli equivalenti a 32 o 64 bit. Per altre informazioni, vedere [The Windows Vista e articoli per gli sviluppatori di Windows Server 2008: Indicazioni sulla compatibilità delle applicazioni](https://msdn.microsoft.com/library/aa480152.aspx).

L'altra opzione consiste nell'abilitare NT Virtual DOS Machine (NTVDM) per il supporto in Windows 10.

#### <a name="requires-admin-privileges"></a>Richiede privilegi di amministratore

L'app richiede all'utente di disporre dell'accesso amministrativo al dispositivo. Usare un manifesto dell'app per le app che richiedono le autorizzazioni di amministratore. Per altre informazioni, vedere [crea e incorporare un manifesto dell'applicazione](https://msdn.microsoft.com/library/bb756929.aspx).
<!--Is this a better, more current link? https://docs.microsoft.com/windows/desktop/sbscs/application-manifests-->

Desktop Analitica consiglia l'app per attività di test. Dovrebbe funzionare correttamente per la fase pilota, ma sono disponibili eventuali regressioni.

#### <a name="java-dependency"></a>Dipendenza Java

Molte applicazioni Java si basano su installato separatamente Java Runtime Environment (JRE). Mentre le versioni JRE precedenti continuino a funzionare in Windows 10, Oracle supporta solo le ultime versioni JRE. Uso un JRE meno recenti non supportate può produrre vulnerabilità di sicurezza. Verificare che l'applicazione viene eseguita su versioni JRE più recenti.

#### <a name="not-dpi-aware"></a>Non-DPI del

L'app potrebbe causare problemi di visualizzazione con risoluzioni dello schermo avanzate Windows 10. Usare un manifesto dell'applicazione per evitare eventuali problemi con risoluzioni DPI elevate. Per altre informazioni, vedere [manifesti dell'applicazione](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests).

Desktop Analitica consiglia l'app per attività di test. Dovrebbe funzionare correttamente per la fase pilota, ma sono disponibili eventuali regressioni.

#### <a name="visual-basic-version-6-vb6"></a>Visual Basic versione 6 (VB6).

Desktop Analitica consiglia l'app per attività di test. Le applicazioni VB6 spesso sono compatibili. Se l'app regresses durante la fase pilota a causa di eventuali dipendenze aggiuntive o widget, quindi è necessario aggiornare l'app a Visual Basic .NET

#### <a name="os-version-dependency"></a>Dipendenza della versione del sistema operativo

È consigliabile sviluppare l'applicazione a usare l'API di helper, o manifesto di applicazione di destinazione Windows 10.

Desktop Analitica consiglia l'app per attività di test. Dovrebbe funzionare correttamente per la fase pilota, ma sono disponibili eventuali regressioni.

#### <a name="silverlight-framework"></a>Framework Silverlight

È consigliabile che le app non basate su browser non usano Silverlight. Data di fine supporto per Silverlight 5 è 2021 ottobre.

I browser web più recenti non supportano Silverlight.

| Browser | Supporto |
|---------|---------|
| Google Chrome | Fine del supporto: Mese di settembre 2015 |
| Firefox | Fine del supporto: Marzo 2017 |
| Microsoft Edge | Nessun plug-in disponibili |

Desktop Analitica consiglia l'app per attività di test. Dovrebbe funzionare correttamente per la fase pilota, ma sono disponibili eventuali regressioni.

#### <a name="net-framework-1011"></a>.NET framework 1.0/1.1

.NET framework versione 1.0 non è supportata in Windows 10. Versione 1.1 non è compatibile in Windows 10. Se l'app è di un editore di terze parti, contattare il fornitore per richiedere una versione compatibile con Windows 10. Sviluppare in caso contrario, l'applicazione a usare una versione supportata di .NET.

#### <a name="net-framework-2030"></a>.NET framework 2.0/3.0

.NET 2.0 e 3.5 Framework sono supportati in Windows 10. Potrebbe essere necessario abilitare la funzionalità di Windows. Per altre informazioni, vedere [installare .NET Framework 3.5 in Windows 10](https://docs.microsoft.com/dotnet/framework/install/dotnet-35-windows-10).

#### <a name="ui-access"></a>Accesso all'interfaccia utente

Le applicazioni con accesso all'interfaccia utente possono ignorare i livelli di controllo di interfaccia utente per l'unità di windows di input a quelli superiori dei privilegi sul desktop. Utilizzare questa impostazione solo per le applicazioni di tecnologia per l'accessibilità dell'interfaccia utente.

Se non si usa funzionalità di accessibilità nell'app, impostare il flag di accesso dell'interfaccia utente nel manifesto dell'app su false. Per altre informazioni, vedere [crea e incorporare un manifesto dell'applicazione](https://msdn.microsoft.com/library/bb756929.aspx).

#### <a name="driver-dependency"></a>Dipendenze di driver

L'app è dipendente da un driver. Desktop Analitica consiglia l'app per attività di test. Dovrebbe funzionare correttamente per la fase pilota, ma sono disponibili eventuali regressioni. Se si verificano problemi, contattare l'editore per richiedere una versione compatibile con Windows 10.



## <a name="app-confidence-simulation-for-a-sample-population"></a>Simulazione di tutta sicurezza App per un campione della popolazione

I grafici seguenti provengono da un case study di esempio. Questi dati evidenzia l'uso dell'analizzatore dell'integrità di App con Desktop Analitica per adottare un approccio basato sui dati per la convalida di app. Questo approccio può aiutare a ridurre il tempo e sforzi per il testing delle applicazioni durante l'aggiornamento a Windows 10.

Questi dati mostrano le metriche di confidenza per i 60 dispositivi 899 applicazioni, incluse le app line-of-business.

![Prima e dopo i grafici che mostrano la fiducia di app](media/aha-app-confidence-simulation.png)


## <a name="see-also"></a>Vedere anche

FastTrack Center Benefit per Windows 10 consente di accedervi **garantire App Desktop**. Questo vantaggio è un nuovo servizio progettato per risolvere i problemi con Windows 10 e Office 365 ProPlus compatibilità dell'applicazione. Per altre informazioni, vedere [garantire App Desktop](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
