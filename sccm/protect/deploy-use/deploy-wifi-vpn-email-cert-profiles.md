---
title: Distribuire profili certificato, Wi-Fi, VPN e di posta elettronica
titleSuffix: Configuration Manager
description: Informazioni su come distribuire profili Wi-Fi, VPN, di posta elettronica e certificato in System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: faf8d48614bc3e27381d57d86fc24da9356aa3f0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347570"
---
# <a name="deploy-profiles-in-system-center-configuration-manager"></a>Distribuire profili in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I profili devono essere distribuiti a una o più raccolte prima di poter essere usati.  

 Usare la finestra di dialogo **Distribuisci profilo Wi-Fi**, **Distribuisci profilo VPN**, **Distribuisci profilo Exchange ActiveSync**, o **Distribuisci profilo certificato** per configurare la distribuzione di questi profili. Durante la configurazione si definisce la raccolta a cui deve essere distribuito il profilo e si specifica la frequenza della valutazione della conformità del profilo.  

> [!NOTE]  
>  Se si distribuiscono allo stesso utente più profili di accesso alle risorse aziendali, si verifica il seguente comportamento:  
>   
>  -   Se un'impostazione in conflitto contiene un valore facoltativo, il valore non verrà inviato al dispositivo.  
> -   Se un'impostazione in conflitto contiene un valore obbligatorio, al dispositivo verrà inviato il valore predefinito. Se non esiste alcun valore predefinito, l'intero profilo di accesso alle risorse aziendali genererà errori. Se, ad esempio, si distribuiscono due profili di posta elettronica allo stesso utente e i valori specificati per **Nome host di Exchange ActiveSync** o **Indirizzo di posta elettronica** sono diversi, entrambi i profili di posta elettronica genereranno errori perché sono impostazioni obbligatorie.  

> -   Prima di distribuire i profili certificato, configurare l'infrastruttura e creare i profili certificato. Per altre informazioni, vedere i seguenti argomenti:  
>   
>  -   [Configurazione dei profili certificato in System Center Configuration Manager](certificate-infrastructure.md)  
> -   [Come creare profili certificato in System Center Configuration Manager](create-certificate-profiles.md)    

> [!IMPORTANT]  
>  Quando si rimuove una distribuzione del profilo VPN, il profilo non viene rimosso dai dispositivi client. Se si desidera rimuovere il profilo dai dispositivi, è necessario procedere manualmente.
>   

## <a name="deploying--profiles"></a>Distribuzione di profili  


1.  Nella console di System Center Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** , espandere **Impostazioni di conformità**, **Accesso risorse aziendali** e scegliere il tipo di profilo appropriato, ad esempio **Profili Wi-Fi**.  

3.  Nell'elenco dei profili selezionare il profilo da distribuire e fare clic su **Distribuisci** nel gruppo **Distribuzione** della scheda **Home**.  

4.  Nella finestra di dialogo di distribuzione del profilo specificare le informazioni seguenti:  

    -   **Raccolta**: fare clic su **Sfoglia** per selezionare la raccolta in cui si vuole distribuire il profilo.  

    -   **Genera un avviso**: abilitare questa opzione per configurare un avviso che viene generato se la conformità del profilo è inferiore a una percentuale specificata in base a una data e un orario specifici. È inoltre possibile specificare se si desidera che un avviso venga inviato a System Center Operations Manager.  

    -   -   **Ritardo casuale (ore)**: (solo per i profili certificato che contengono le impostazioni Simple Certificate Enrollment Protocol) specifica una finestra di ritardo in modo da evitare un'elaborazione eccessiva nel servizio Registrazione dispositivi di rete. Il valore predefinito è **64** ore.  

    -   **Specificare la pianificazione per la valutazione della conformità per questo <type>profilo**: specificare la pianificazione in base alla quale il profilo distribuito viene valutato nei computer client. Può trattarsi di una pianificazione semplice o personalizzata.  

        > [!NOTE]  
        >  Il profilo viene valutato dai computer client quando l'utente effettua l'accesso.  

5.  Fare clic su **OK** per chiudere la finestra di dialogo e creare la distribuzione.

### <a name="see-also"></a>Vedere anche  

[How to monitor Wi-Fi, VPN, and email profiles in System Center Configuration Manager](monitor-wifi-email-vpn-profiles.md) (Come monitorare i profili Wi-Fi, VPN e di posta elettronica in System Center Configuration Manager)

[How to monitor certificate profiles in System Center Configuration Manager](monitor-certificate-profiles.md) (Come monitorare i profili certificato in System Center Configuration Manager)
