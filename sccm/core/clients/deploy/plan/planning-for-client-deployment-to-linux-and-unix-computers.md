---
title: Pianificazione della distribuzione client in computer Linux e UNIX | Microsoft Docs
description: Pianificazione della distribuzione del client in computer Linux e UNIX in System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 44153689-70e8-42ad-9ae8-17ae35f6a2e3
caps.latest.revision: 9
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: dad941d5984fc7e0b43954b14c3966bb2632ad05
ms.contentlocale: it-it
ms.lasthandoff: 12/16/2016


---
# <a name="planning-for-client-deployment-to-linux-and-unix-computers-in-system-center-configuration-manager"></a>Pianificazione della distribuzione del client in computer Linux e UNIX in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile installare il client di System Center Configuration Manager nei computer che eseguono Linux o UNIX. Questo client è progettato per i server che funzionano come computer di gruppi di lavoro e il client non supporta l'interazione con gli utenti connessi. Dopo aver installato il software client e dopo che il client ha stabilito la comunicazione con il sito di Configuration Manager, gestire il client usando la console e i report di Configuration Manager.  

> [!NOTE]  
>  Il client di Configuration Manager per computer Linux e UNIX non supporta le funzionalità di gestione seguenti:  
>   
>  -   Installazione push client  
> -   Distribuzione del sistema operativo  
> -   Distribuzione di applicazioni; in alternativa, distribuire il software usando pacchetti e programmi.  
> -   Inventario software  
> -   Aggiornamenti software  
> -   Impostazioni di conformità  
> -   Controllo remoto  
> -   Risparmio energia  
> -   Controllo e correzione client dello stato client  
> -   Gestione client basata su Internet  

 Per informazioni sulle distribuzioni Linux e UNIX e per l'hardware necessario per supportare il client per Linux e UNIX, vedere [Hardware consigliato per System Center Configuration Manager](../../../../core/plan-design/configs/recommended-hardware.md).  

 Usare le informazioni contenute in questo articolo per pianificare la distribuzione del client di Configuration Manager per Linux e UNIX.  

##  <a name="BKMK_ClientDeployPrereqforLnU"></a> Prerequisiti per la distribuzione del client ai server Linux e UNIX  
 Utilizzare le informazioni seguenti per determinare i prerequisiti, di che è necessario disporre correttamente in grado installare il client per Linux e UNIX.  

###  <a name="BKMK_ClientDeployExternalforLnU"></a> Dipendenze esterne a Configuration Manager:  
 Nella tabella seguente vengono descritti i sistemi UNIX e Linux e le dipendenze dei pacchetti necessari.  

 **Red Hat Enterprise Linux ES versione 4**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|glibc|Librerie standard C|2.3.4-2|  
|Openssl|Librerie OpenSSL; Secure Network Communications Protocol|0.9.7a-43.1|  
|PAM|Moduli di autenticazione plug-in|0.77-65.1|  

 **Red Hat Enterprise Linux Server versione 5.1 (Tikanga)**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|glibc|Librerie standard C|2.5-12|  
|Openssl|Librerie OpenSSL; Secure Network Communications Protocol|0.9.8b-8.3.el5|  
|PAM|Moduli di autenticazione plug-in|0.99.6.2-3.14.el5|  

 **Red Hat Enterprise Linux Server versione 6**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|glibc|Librerie standard C|2.12-1.7|  
|Openssl|Librerie OpenSSL; Secure Network Communications Protocol|1.0.0-4|  
|PAM|Moduli di autenticazione plug-in|1.1.1-4|  

 **Solaris 9 SPARC**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|Patch richiesta del sistema operativo|Problemi di memoria PAM|112960-48|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (sparc)|5.9, REV=2002.03.18|  
|SUNWlibms|Forte Developer Bundled Shared libm (sparc)|5.9, REV=2001.12.10|  
|Openssl|SMCosslg (sparc)<br /><br /> Sun non offre una versione di OpenSSL per Solaris 9 SPARC. È disponibile una versione di Sunfreeware.|0.9.7g|  
|PAM|Moduli di autenticazione plug-in<br /><br /> SUNWcsl, Core Solaris, (Shared Libs) (sparc)|11.9.0,REV=2002.04.06.15.27|  

 **Solaris 10 SPARC**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|Patch richiesta del sistema operativo|Problemi di memoria PAM|117463-05|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (sparc)|5.10, REV=2004.12.22|  
|SUNWlibms|Math & Microtasking Libraries (Usr) (sparc)|5.10, REV=2004.11.23|  
|SUNWlibmsr|Math & Microtasking Libraries (Root) (sparc)|5.10, REV=2004.11.23|  
|SUNWcslr|Core Solaris Libraries (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|SUNWcsl|Core Solaris Libraries (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|Openssl|SUNopenssl-librararies (Usr)<br /><br /> Sun fornisce le librerie OpenSSL per Solaris 10 SPARC, che vengono aggregate al sistema operativo.|11.10.0,REV=2005.01.21.15.53|  
|PAM|Moduli di autenticazione plug-in<br /><br /> SUNWcsr, Core Solaris, (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  

 **Solaris 10 x86**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|Patch richiesta del sistema operativo|Problemi di memoria PAM|117464-04|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (i386)|5.10, REV=2004.12.20|  
|SUNWlibmsr|Math & Microtasking Libraries (Root) (i386)|5.10, REV=2004.12.18|  
|SUNWcsl|Core Solaris, (Shared Libs) (i386)|11.10.0, REV=2005.01.21.16.34|  
|SUNWcslr|Core Solaris Libraries (Root) (i386)|11.10.0, REV=2005.01.21.16.34|  
|Openssl|SUNWopenssl-libraries; OpenSSL Libraries (Usr) (i386)|11.10.0, REV=2005.01.21.16.34|  
|PAM|Moduli di autenticazione plug-in<br /><br /> SUNWcsr Core Solaris, (Root)(i386)|11.10.0, REV=2005.01.21.16.34|  

 **Solaris 11 SPARC**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math & Microtasking Libraries (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris Libraries (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Shared Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (Root)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|OpenSSL Libraries (Usr)|11.11.0, REV=2010.05.25.01.00|  

 **Solaris 11 x86**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------|-----------|---------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math & Microtasking Libraries (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris Libraries (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Shared Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (Root)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|OpenSSL Libraries (Usr)|11.11.0, REV=2010.05.25.01.00|  

 **SUSE Linux Enterprise Server 9 (i586)**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|Service Pack 4|SUSE Linux Enterprise Server 9||  
|OS Patch lib gcc-41.rpm|Libreria condivisa standard|41-4.1.2_20070115-0.6|  
|OS Patch lib stdc++-41.rpm|Libreria condivisa standard|41-4.1.2_20070115-0.6|  
|Openssl|Librerie OpenSSL; Secure Network Communications Protocol|0.9.7d-15.35|  
|PAM|Moduli di autenticazione plug-in|0.77-221-11|  

 **SUSE Linux Enterprise Server 10 SP1 (i586)**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|glibc-2,4-31,30|Libreria condivisa standard C|2.4-31.30|  
|OpenSSL|Librerie OpenSSL; Secure Network Communications Protocol|0.9.8a-18.15|  
|PAM|Moduli di autenticazione plug-in|0.99.6.3-28.8|  

 **SUSE Linux Enterprise Server 11 (i586)**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|glibc-2.9-13.2|Libreria condivisa standard C|2.9-13.2|  
|PAM|Moduli di autenticazione plug-in|pam-1.0.2-20.1|  

 **Universal Linux (pacchetto Debian) Debian, Ubuntu Server**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|libc6|Libreria condivisa standard C|2.3.6|  
|Openssl|Librerie OpenSSL; Secure Network Communications Protocol|0.9.8 o 1.0|  
|PAM|Moduli di autenticazione plug-in|0.79-3|  

 **Universal Linux (pacchetto RPM) CentOS, Oracle Linux**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|glibc|Libreria condivisa standard C|2.5-12|  
|Openssl|Librerie OpenSSL; Secure Network Communications Protocol|0.9.8 o 1.0|  
|PAM|Moduli di autenticazione plug-in|0.99.6.2-3.14|  

 **IBM AIX 5L 5.3**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|Versione del sistema operativo|Versione del sistema operativo|AIX 5.3, Technology Level 6, Service Pack 5|  
|xlC.rte|XL C/C++ Runtime|9.0.0.2|  
|openssl.base|Librerie OpenSSL; Secure Network Communications Protocol|0.9.8.4|  

 **IBM AIX 6.1**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|Versione del sistema operativo|Versione del sistema operativo|AIX 6.1, qualsiasi Technology Level e Service Pack|  
|xlC.rte|XL C/C++ Runtime|9.0.0.5|  
|OpenSSL/openssl.base|Librerie OpenSSL; Secure Network Communications Protocol|0.9.8.4|  

 **IBM AIX 7.1 (Power)**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|Versione del sistema operativo|Versione del sistema operativo|AIX 7.1, qualsiasi Technology Level e Service Pack|  
|xlC.rte|XL C/C++ Runtime||  
|OpenSSL/openssl.base|Librerie OpenSSL; Secure Network Communications Protocol||  

 **HP-UX 11i v2 IA 64**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|HPUXBaseOS|Sistema operativo di base|B.11.23|  
|HPUXBaseAux|HP-UX Base OS Auxiliary|B.11.23.0706|  
|HPUXBaseAux.openssl|Librerie OpenSSL; Secure Network Communications Protocol|A.00.09.07l.003|  
|PAM|Moduli di autenticazione plug-in|PAM fa parte dei componenti principali del sistema operativo di HP-UX. Non ci sono altre dipendenze.|  

 **HP-UX 11i v2 PA-RISC**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|HP-UX Foundation Operating Environment|B.11.23.0706|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|Librerie compatibili con gli strumenti di sviluppo|B.11.23|  
|HPUXBaseAux|HP-UX Base OS Auxiliary|B.11.23.0706|  
|HPUXBaseAux.openssl|Librerie OpenSSL; Secure Network Communications Protocol|A.00.09.071.003|  
|PAM|Moduli di autenticazione plug-in|PAM fa parte dei componenti principali del sistema operativo di HP-UX. Non ci sono altre dipendenze.|  

 **HP-UX 11i v3 PA-RISC**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|HP-UX Foundation Operating Environment|B.11.31.0709|  
|OS-Core.MinimumRuntime.CORE2-SHLIBS|Librerie emulatore specifico IA|B.11.31|  
|openssl/Openssl.openssl|Librerie OpenSSL; Secure Network Communications Protocol|A.00.09.08d.002|  
|PAM|Moduli di autenticazione plug-in|PAM fa parte dei componenti principali del sistema operativo di HP-UX. Non ci sono altre dipendenze.|  

 **HP-UX 11i v3 IA64**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|HP-UX Foundation Operating Environment|B.11.31.0709 |  
|OS-Core.MinimumRuntime.CORE-SHLIBS|Librerie di sviluppo specifico IA|B.11.31|  
|SysMgmtMin|Strumenti minimi di distribuzione software|B.11.31.0709|  
|SysMgmtMin.openssl|Librerie OpenSSL; Secure Network Communications Protocol|A.00.09.08d.002|  
|PAM|Moduli di autenticazione plug-in|PAM fa parte dei componenti principali del sistema operativo di HP-UX. Non ci sono altre dipendenze.|  

 **Dipendenze di Configuration Manager:** la tabella seguente elenca i ruoli di sistema del sito che supportano client Linux e UNIX. Per altre informazioni su questi ruoli del sistema del sito, vedere [Determinare i ruoli del sistema del sito per System Center Configuration Manager](../../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

|Sistema del sito di Configuration Manager|Altre informazioni|  
|---------------------------------------|----------------------|  
|Punto di gestione|Anche se non è necessario un punto di gestione per installare un client di Configuration Manager per Linux e UNIX, è invece necessario un punto di gestione per trasferire informazioni tra i computer client e i server di Configuration Manager. Senza un punto di gestione, non è possibile gestire i computer client.|  
|Punto di distribuzione|Il punto di distribuzione non è necessario per installare un client di Configuration Manager per Linux e UNIX. Tuttavia, il ruolo del sistema del sito è necessario se si distribuisce software per server Linux e UNIX.<br /><br /> Poiché il client di Configuration Manager per Linux e UNIX non supporta le comunicazioni che usano SMB, i punti di distribuzione usati con il client devono supportare la comunicazione HTTP o HTTPS.|  
|Punto di stato di fallback|Il punto dello stato di fallback non è necessario per installare un client di Configuration Manager per Linux e UNIX. Il punto di stato di fallback consente tuttavia ai computer nel sito di Configuration Manager di inviare messaggi di stato quando non possono comunicare con un punto di gestione. Client può inoltre inviare lo stato dell'installazione per il punto di stato di fallback.|  

 **Firewall requisiti**: Assicurarsi che i firewall non blocchino le comunicazioni attraverso le porte specificate come porte di richiesta client. Il client per Linux e UNIX comunica direttamente con i punti di gestione, i punti di distribuzione e i punti di stato di fallback.  

 Per informazioni sulle comunicazioni client e sulle porte di richiesta, vedere  [Configurare il Client per Linux e UNIX individuare i punti di gestione](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigClientMP).  

##  <a name="BKMK_PlanningforCommunicationsforLnU"></a> Pianificazione delle comunicazioni attraverso trust tra foreste per server Linux e UNIX  
 I server Linux e UNIX gestiti con Configuration Manager funzionano come client di un gruppo di lavoro e richiedono configurazioni simili ai client basati su Windows che si trovano in un gruppo di lavoro. Per informazioni sulle comunicazioni da computer che si trovano in gruppi di lavoro, vedere la sezione [Comunicazioni tra foreste Active Directory](../../../../core/plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest) nell'argomento [Comunicazioni tra gli endpoint in System Center Configuration Manager](../../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

###  <a name="BKMK_ServiceLocationforLnU"></a> Posizione del servizio dal client per Linux e UNIX  
 L'attività di individuazione di un server di sistema del sito che offre servizi ai client viene considerato come percorso del servizio. A differenza di un client basato su Windows, il client per Linux e UNIX non utilizza Active Directory per la posizione del servizio. Il client di Configuration Manager per Linux e UNIX non supporta una proprietà client che specifica il suffisso del dominio di un punto di gestione. Al contrario, il client conosciuti da server del sistema del sito aggiuntivi che forniscono servizi ai client da un punto di gestione noti che viene assegnato quando si installa il software client.  

 Per altre informazioni sulla posizione del servizio, vedere la sezione [Posizione del servizio e modo in cui i client determinano il relativo punto di gestione assegnato](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location) in [Informazioni su come i client trovano i servizi e le risorse del sito per System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

##  <a name="BKMK_SecurityforLnU"></a> Pianificazione di sicurezza e certificati per server Linux e UNIX  
 Per comunicazioni autenticate e protette con i siti di Configuration Manager, il client di Configuration Manager per Linux e UNIX usa lo stesso modello per la comunicazione del client di Configuration Manager per Windows.  

 Quando si installa il client Linux e UNIX, è possibile assegnare il client di un certificato PKI che consente di usare HTTPS per comunicare con i siti di Configuration Manager. Se non si assegna un certificato PKI, il client crea un certificato autofirmato e comunica solo tramite HTTP.  

 I client a cui viene fornito un certificato PKI durante l'installazione usano HTTPS per comunicare con i punti di gestione. Se un client non riesce a rilevare un punto di gestione che supporta HTTPS, tornerà a usare HTTP con il certificato PKI fornito.  

 Quando un client Linux o UNIX utilizza un certificato PKI non è necessario approvarli. Se un client usa un certificato autofirmato, verificare le impostazioni di gerarchia per l'approvazione client nella console di Configuration Manager. Se non è il metodo di approvazione client **approvare automaticamente tutti i computer (scelta non consigliati)**, è necessario approvare manualmente il client.  

 Per altre informazioni su come approvare manualmente il client, vedere la sezione [Gestire i client dal nodo Dispositivi](../../../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode) in [Come gestire i client in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

 Per informazioni sull'uso dei certificati in Configuration Manager, vedere [Requisiti dei certificati PKI per System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

###  <a name="BKMK_AboutCertsforLnU"></a> Informazioni sui certificati per l'uso da server Linux e UNIX  
 Il client di Configuration Manager per Linux e UNIX usa un certificato autofirmato o un certificato x. 509 PKI come i client basati su Windows. Non ci sono modifiche ai requisiti di infrastruttura a chiave pubblica (PKI) per i sistemi del sito di Configuration Manager quando si gestiscono client Linux e UNIX.  

 I certificati usati per i client Linux e UNIX che comunicano con i sistemi del sito di Configuration Manager devono essere in formato Public Key Certificate Standard (PKCS #12) e la password deve essere nota, in modo che sia possibile specificarla al client quando si specifica il certificato PKI.  

 Il client di Configuration Manager per Linux e UNIX supporta un solo certificato PKI. Pertanto, i criteri di selezione del certificato da configurare per un sito di Configuration Manager non sono validi.  

###  <a name="BKMK_ConfigCertsforLnU"></a> Configurazione dei certificati per server Linux e UNIX  
 Per configurare un client di Configuration Manager per i server Linux e UNIX per usare le comunicazioni HTTPS, è necessario configurare il client per usare un certificato PKI quando si installa il client. Impossibile effettuare il provisioning di un certificato prima dell'installazione del software client.  

 Quando si installa un client che utilizza un certificato PKI, si utilizza il parametro della riga di comando **- /usepkicert** per specificare il percorso e nome di un file PKCS #12 che contiene il certificato PKI. È inoltre necessario utilizzare il parametro della riga di comando **- certpw** per specificare la password per il certificato.  

 Se non si specifica **- /usepkicert**, il client genera un certificato autofirmato e tenta di comunicare al server del sistema del sito solo tramite HTTP.  

##  <a name="BKMK_NoSHA-256"></a> Informazioni sui sistemi operativi Linux e UNIX che non supportano SHA-256  
 I sistemi operativi Linux e UNIX seguenti supportati come client per Configuration Manager sono stati rilasciati con le versioni di OpenSSL che non supportano SHA-256:  

-   Red Hat Enterprise Linux versione 4 (x86/x64)  

-   Solaris versione 9 (SPARC) e Solaris versione 10 (SPARC/x86)  

-   SUSE Linux Enterprise Server versione 9 (x86)  

-   Versione di HP-UX 11iv2 (PA-SIRIACO/IA64)  

 Per gestire questi sistemi operativi con Configuration Manager, è necessario installare il client di Configuration Manager per Linux e UNIX con un'opzione della riga di comando che indichi al client di ignorare la convalida di SHA-256. I client di Configuration Manager eseguiti in queste versioni del sistema operativo operano in una modalità meno sicura rispetto ai client che supportano SHA-256. Questa modalità meno sicura dell'operazione presenta il seguente comportamento:  

-   I client non convalidano la firma del server del sito associata ai criteri che richiedono da un punto di gestione.  

-   I client non convalidano l'hash per i pacchetti scaricati da un punto di distribuzione.  

> [!IMPORTANT]  
>  Il **ignoreSHA256validation** opzione consente di eseguire il client per computer Linux e UNIX in una modalità meno sicura. Questo deve essere utilizzato su piattaforme precedenti che non include il supporto per SHA-256. È un override di sicurezza e non è consigliato da Microsoft, ma è supportato l'utilizzo in un ambiente sicuro e attendibile datacenter.  

 Quando si installa il client di Configuration Manager per Linux e UNIX, lo script di installazione verifica la versione del sistema operativo. Per impostazione predefinita, se la versione del sistema operativo viene identificata come rilasciata senza una versione di OpenSSL che supporta SHA-256, l'installazione del client di Configuration Manager non riesce.  

 Per installare il client di Configuration Manager nei sistemi operativi Linux e UNIX che non sono stati rilasciati con una versione di OpenSSL che supporta SHA-256, è necessario usare l'opzione della riga di comando di installazione **ignoreSHA256validation**. Quando si usa questa opzione della riga di comando in un sistema operativo Linux o UNIX applicabile, il client di Configuration Manager ignora la convalida di SHA-256 e dopo l'installazione, il client non userà SHA-256 per firmare i dati inviati ai sistemi operativi tramite HTTP. Per informazioni sulla configurazione dei client Linux e UNIX per usare i certificati, vedere [Planning for Security and Certificates for Linux and UNIX Servers](#BKMK_SecurityforLnU) in questo argomento. Per informazioni sulle richieste di SHA-256, vedere [Configurare la firma e la crittografia](../../../../core/plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption) nell'argomento [Configurare la sicurezza in System Center Configuration Manager](../../../../core/plan-design/security/configure-security.md).  

> [!NOTE]  
>  L'opzione della riga di comando **ignoreSHA256validation** viene ignorato nei computer che eseguono una versione di Linux e UNIX che rilasciato con le versioni di OpenSSL che supportano SHA-256.  

