---
title:
- Titolo dell'articolo in 35 caratteri o meno
titleSuffix: Configuration Manager
description: ''
ms.date: mm/dd/yyyy
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid:
- GET ONE FROM guidgenerator.com
author:
- GITHUB USERNAME
ms.author:
- ALIAS
manager:
- ALIAS
ms.openlocfilehash: bb0a23b8870d31136967b1bc594580bcc2cd0cd9
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="metadata-and-markdown-template"></a>Modello di markdown e metadati

Questo modello di Microsoft Docs contiene esempi della sintassi di markdown e indicazioni su come impostare i metadati. È disponibile nella directory radice di ogni repository EM Pilot, ad esempio ~/Azure-RMSDocs-pr /template.md, e deve essere letto come un file markdown, anche se è possibile fare riferimento alla [versione pubblicata](https://stage.docs.microsoft.com/en-us/rights-management/template) per visualizzare il rendering degli esempi di markdown.

Quando si crea un file markdown, è necessario copiare il modello in un nuovo file, specificare i metadati come indicato sotto, impostare l'intestazione H1 precedente sul titolo dell'articolo ed eliminare il contenuto.


## <a name="metadata"></a>Metadati

L'intero blocco di metadati è disponibile sopra, diviso in campi obbligatori e facoltativi. Per altre informazioni, vedere il [foglio informativo sui metadati OPS](https://ppe.msdn.microsoft.com/en-us/ce-csi-docs/ops/ops-onboarding/managing-content/content-meta-data). Ecco alcuni punti importanti:

- **Deve** essere presente uno spazio tra i due punti (:) e il valore di un elemento dei metadati.
- Se un elemento dei metadati facoltativo non presenta un valore, impostare l'elemento come commento con un simbolo # (non lasciarlo vuoto e non usare "nd"). Se si aggiunge un valore a un elemento impostato come commento, assicurarsi di rimuovere il simbolo #.
- I due punti in un valore, ad esempio un titolo, causano interruzioni nel parser dei metadati. Sostituirli con la codifica HTML &#58;, ad esempio "title: Azure Rights Management&#58; nozioni di base | Azure RMS".
- **title**: questo titolo verrà visualizzato nei risultati dei motori di ricerca. Il titolo deve terminare con una barra verticale (|) seguita dal nome del servizio (vedere sopra). Il titolo non deve essere identico al titolo presente nell'intestazione H1. La lunghezza non deve superare 65 caratteri (incluso | NOME SERVIZIO)
- **author**, **manager**, **reviewer**: il campo dell'autore deve contenere il **nome utente Github** dell'autore e non l'alias.  I campi "manager" e "reviewer" devono invece contenere alias. ms.reviewer indica il nome del PM associato all'articolo o al servizio.
- **ms.assetid**: GUID dell'articolo generato dal sistema CAPS. Quando si crea un nuovo file markdown, ottenere un GUID da [https://www.guidgenerator.com](https://www.guidgenerator.com).
- **ms.prod**, **ms.service**, **ms.technology**, **ms.devlang**, **ms.topic**, **ms.tgt_pltfrm**: i valori possibili per questi elementi sono disponibili [qui](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default).

## <a name="basic-markdown-and-gfm"></a>Markdown di base e GFM (GitHub Flavored Markdown)

È supportato tutto il markdown di base e GFM. Per altre informazioni su questi argomenti, vedere:

- [Sintassi markdown di base](https://daringfireball.net/projects/markdown/syntax)
- [Documentazione per GFM GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown)

## <a name="headings"></a>Intestazioni

Sopra sono riportati esempi di intestazioni di primo e secondo livello.

L'argomento **deve** includere una sola intestazione di primo livello che verrà visualizzata come titolo della pagina.  

Le intestazioni di secondo livello genereranno il sommario della pagina visualizzato nella sezione "In questo articolo" sotto il titolo della pagina.

### <a name="third-level-heading"></a>Intestazione di terzo livello
#### <a name="fourth-level-heading"></a>Intestazione di quarto livello
##### <a name="fifth-level-heading"></a>Intestazione di quinto livello
###### <a name="sixth-level-heading"></a>Intestazione di sesto livello

## <a name="text-styling"></a>Stile del testo

*Corsivo*

**Grassetto**

~~Barrato~~



## <a name="links"></a>Collegamenti

Per stabilire un collegamento a un file markdown nello stesso repository, usare [collegamenti relativi](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2).

- Esempio: [Informazioni su Microsoft Azure Rights Management](./understand-explore/what-is-azure-rights-management.md)

Per stabilire un collegamento a un'intestazione nello stesso file markdown, visualizzare l'origine dell'articolo pubblicato, trovare l'ID dell'intestazione, ad esempio `id="blockquote"`, e creare il collegamento usando # + ID, ad esempio `#blockquote`.

- Esempio: [Blockquotes](#blockquote)

Per creare un collegamento a un'intestazione in un file markdown nello stesso repository, usare collegamenti relativi e collegamenti con hashtag.

- Esempio: [Panoramica tecnica del processo di iscrizione](./understand-explore/rms-for-individuals-user-signup.md#technical-overview-of-the-sign-up-process)

Per creare un collegamento a un file esterno, usare l'URL completo come collegamento.

- Esempio: [Github](http://www.github.com)

Se in un file markdown viene visualizzato un URL, questo verrà trasformato in un collegamento selezionabile.

- Esempio: http://www.github.com

## <a name="lists"></a>Elenchi

### <a name="ordered-lists"></a>Elenchi ordinati

1. Questo
1. è
1. un
1. elenco
1. Elenco  


#### <a name="ordered-list-with-an-embedded-list"></a>Elenco ordinato con elenco incorporato

1. Ecco
1. qui
1. un
1. elenco
    1. Miss Scarlett
    1. Professor Plum
1. ordinato
1. elenco


### <a name="unordered-lists"></a>Elenchi non ordinati

- Questo
- è impostata su
- a
- elenco
- elenco


##### <a name="unordered-list-with-an-embedded-lists"></a>Elenco non ordinato con elenco incorporato

- Questo
- elenco
- elenco
    - Mrs. Peacock
    - Mr. Green
- contiene  
- altri
    1. Colonel Mustard
    1. Mrs. White
- elenchi


## <a name="horizontal-rule"></a>Riga orizzontale

---

## <a name="tables"></a>Tables

| Tables        | sono           | fantastiche  |
| ------------- |:-------------:| -----:|
| Colonna 3      | allineata a destra | $ 1600 |
| Colonna 2      | allineata al centro      |   $ 12 |
| Colonna 1 predefinita | allineata a sinistra     |    $ 1 |


## <a name="code"></a>Codice

### <a name="codeblock"></a>Blocco di codice

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### <a name="in-line-code"></a>Codice inline

Esempio di `in-line code`.

## <a name="blockquotes"></a>Citazioni

> La siccità si protraeva ormai da dieci milioni di anni, e il regno delle terribili lucertole era finito da molto tempo. Lì, sull'Equatore, nel continente che un giorno sarebbe stato chiamato Africa, la lotta per la vita aveva raggiunto un nuovo diapason di ferocia, e il vincitore ancora non si intravedeva. In quella terra sterile e arida soltanto le creature piccole o fulminee o feroci potevano prosperare, o appena sperare di sopravvivere.

## <a name="images"></a>Immagini

### <a name="static-image"></a>Immagine statica

![questo è il testo alternativo](./media/AzRMS_elements.png)

### <a name="linked-image"></a>Immagine collegata

[![testo alternativo per l'immagine collegata](./media/AzRMS_elements.png)](https://azure.microsoft.com)

### <a name="animated-gif"></a>GIF animata

![GIF animata](./media/hololens.gif)

## <a name="alerts"></a>Avvisi

### <a name="note"></a>Nota

> [!NOTE]
> Questa è una NOTA

### <a name="warning"></a>Avviso

> [!WARNING]
> Questo è un AVVISO

### <a name="tip"></a>Suggerimento

> [!TIP]
> Questo è un SUGGERIMENTO

### <a name="important"></a>Importante

> [!IMPORTANT]
> Questo è IMPORTANTE

## <a name="videos"></a>Video

### <a name="channel-9"></a>Channel 9

<iframe src="http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>


### <a name="youtube"></a>YouTube

<iframe width="420" height="315" src="https://www.youtube.com/embed/R6_eWWfNB54" frameborder="0" allowfullscreen></iframe>

## <a name="docsms-extentions"></a>Estensioni di Microsoft Docs

### <a name="button"></a>Pulsante

> [!div class="button"]
[collegamenti ai pulsanti](/rights-management)

### <a name="selector"></a>Selettore

> [!div class="op_single_selector"]
- [foo](/rights-management/template.md)
- [bar](/rights-management/scratch.md)

### <a name="step-by-step"></a>Passo passo

>[!div class="step-by-step"]
[Indietro](https://www.example.com)
[Avanti](https://www.example.com)
