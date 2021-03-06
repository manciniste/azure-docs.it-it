---
title: Ottimizzare la distribuzione del contenuto di Azure per lo scenario in uso
description: Come ottimizzare la distribuzione di contenuto per scenari specifici
services: cdn
documentationcenter: 
author: dksimpson
manager: 
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2018
ms.author: rli
ms.openlocfilehash: fa4cf306eeb1a8372da5b2a86ac73fbba2832666
ms.sourcegitcommit: 99d29d0aa8ec15ec96b3b057629d00c70d30cfec
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="optimize-azure-content-delivery-for-your-scenario"></a>Ottimizzare la distribuzione del contenuto di Azure per lo scenario in uso

Quando si distribuisce il contenuto a un pubblico globale ampio, è fondamentale garantirne la distribuzione ottimizzata. La rete per la distribuzione di contenuti di Azure può ottimizzare l'esperienza di distribuzione in base al tipo di contenuto disponibile. Il contenuto può essere un sito Web, uno streaming live, un video o un file di grandi dimensioni per il download. Quando si crea un endpoint della rete per la distribuzione di contenuti, specificare uno scenario nell'opzione **Optimized for** (Ottimizzato per). La scelta determina quale ottimizzazione verrà applicata al contenuto distribuito dall'endpoint della rete per la distribuzione di contenuti.

Le opzioni di ottimizzazione sono progettate per usare i comportamenti basati sulle procedure consigliate per migliorare le prestazioni a livello di distribuzione di contenuti e l'offload dell'origine. Le scelte dello scenario influiranno sulle prestazioni modificando le configurazioni per la memorizzazione nella cache parziale, la suddivisione in blocchi di oggetti e i criteri di ripetizione in caso di errore dell'origine. 

Questo articolo offre una panoramica delle varie funzionalità di ottimizzazione e dello scenario in cui usarle. Per altre informazioni sulle funzionalità e le limitazioni, vedere la documentazione specifica per ogni singolo tipo di ottimizzazione.

> [!NOTE]
> Le opzioni **Optimized for** (Ottimizzato per) possono variare in base al provider selezionato. I provider di rete CDN applicano il miglioramento in modi diversi, a seconda dello scenario. 

## <a name="provider-options"></a>Opzioni del provider

La **rete per la distribuzione di contenuti di Azure da Akamai** supporta le ottimizzazioni seguenti:

* [Distribuzione Web generale](#general-web-delivery) 

* [Streaming multimediale generale](#general-media-streaming)

* [Streaming multimediale di video on demand](#video-on-demand-media-streaming)

* [Download di file di grandi dimensioni](#large-file-download)

* [Accelerazione sito dinamico](#dynamic-site-acceleration) 

La **rete per la distribuzione di contenuti di Azure da Verizon** supporta le ottimizzazioni seguenti:

* [Distribuzione Web generale](#general-web-delivery) (può essere usata anche per lo streaming multimediale e il contenuto dei download di file di grandi dimensioni)

* [Accelerazione sito dinamico](#dynamic-site-acceleration) 

Per selezionare il provider ottimale per la propria distribuzione, è consigliabile testare le prestazioni offerte dai diversi provider.

## <a name="select-and-configure-optimization-types"></a>Selezionare e configurare i tipi di ottimizzazione

Per creare un nuovo endpoint, selezionare un tipo di ottimizzazione che meglio corrisponde allo scenario e al tipo di contenuto che si desidera distribuire tramite l'endpoint. La selezione predefinita è **Distribuzione Web generale**. Per gli endpoint della **rete per la distribuzione di contenuti di Azure da Akamai** esistenti, è possibile aggiornare l'opzione di ottimizzazione in qualsiasi momento. Questa modifica non interrompe la distribuzione dalla rete per la distribuzione di contenuti. 

1. In un profilo della **rete per la distribuzione di contenuti di Azure da Akamai** selezionare un endpoint.

    ![Selezione dell'endpoint ](./media/cdn-optimization-overview/01_Akamai.png)

2. In **IMPOSTAZIONI** selezionare **Ottimizzazione**. Quindi selezionare un tipo dall'elenco a discesa **Ottimizzato per**.

    ![Selezione dell'ottimizzazione e del tipo](./media/cdn-optimization-overview/02_Select.png)

## <a name="optimization-for-specific-scenarios"></a>Ottimizzazione per scenari specifici

È possibile ottimizzare l'endpoint della rete CDN per uno di questi scenari. 

### <a name="general-web-delivery"></a>Distribuzione Web generale

La distribuzione Web generale è l'opzione di ottimizzazione più comune. È mirata per l'ottimizzazione di contenuto Web generale, ad esempio pagine Web e applicazioni Web. Può essere usata anche per i download di file e video.

Un sito Web tipico contiene contenuto statico e dinamico. Il contenuto statico include immagini, librerie JavaScript e fogli di stile, che possono essere memorizzati nella cache e distribuiti a utenti diversi. Il contenuto dinamico è personalizzato per un singolo utente, ad esempio notizie personalizzate in base al profilo di un utente. Il contenuto dinamico non viene memorizzato nella cache perché è univoco per ogni utente, ad esempio il contenuto di un carrello della spesa. La distribuzione Web generale consente di ottimizzare l'intero sito Web. 

> [!NOTE]
> Se si usa la **rete per la distribuzione di contenuti di Azure da Akamai**, è possibile scegliere questa ottimizzazione quando le dimensioni medie del file sono inferiori a 10 MB. Se le dimensioni medie dei file sono maggiori di 10 MB, selezionare **Download di file di grandi dimensioni** dall'elenco a discesa **Optimized for** (Ottimizzato per).

### <a name="general-media-streaming"></a>Streaming multimediale generale

Lo streaming multimediale generale è consigliabile se è necessario usare l'endpoint sia per lo streaming live sia per lo streaming di video on demand.

Lo streaming multimediale è sensibile all'ora perché i pacchetti che vengono ricevuti in ritardo sul client possono compromettere l'esperienza di visualizzazione, ad esempio con frequenti memorizzazioni nel buffer del contenuto video. L'ottimizzazione dello streaming multimediale riduce la latenza di distribuzione del contenuto multimediale e offre un'esperienza di flusso uniforme agli utenti. 

Si tratta di uno scenario comune per i clienti di servizi multimediali di Azure. Quando si usano i servizi multimediali di Azure, si otterrà un endpoint di streaming che può essere usato per lo streaming live e on demand. In questo scenario i clienti non devono passare a un altro endpoint quando passa dallo streaming live a quello on demand. L'ottimizzazione dello streaming multimediale generale supporta questo tipo di scenario.

La **rete per la distribuzione di contenuti di Azure da Verizon** usa l'ottimizzazione di tipo distribuzione Web generale per distribuire il contenuto multimediale.

Per altre informazioni sull'ottimizzazione dello streaming multimediale, vedere [Ottimizzazione dello streaming multimediale](cdn-media-streaming-optimization.md).

### <a name="video-on-demand-media-streaming"></a>Streaming multimediale di video on demand

L'ottimizzazione dello streaming multimediale di video on demand migliora il contenuto dello streaming di video on demand. Se si usa un endpoint per lo streaming di video on demand, è possibile usare questa opzione.

La **rete per la distribuzione di contenuti di Azure da Verizon** usa l'ottimizzazione di tipo distribuzione Web generale per distribuire il contenuto multimediale.

Per altre informazioni sull'ottimizzazione dello streaming multimediale, vedere [Ottimizzazione dello streaming multimediale](cdn-media-streaming-optimization.md).

> [!NOTE]
> Se l'endpoint viene usato principalmente per il contenuto di video on demand, usare questo tipo di ottimizzazione. La differenza principale tra questa ottimizzazione e quella multimediale generale è il timeout per i tentativi di connessione. Il timeout è molto più breve per gli scenari di streaming live.

### <a name="large-file-download"></a>Download di file di grandi dimensioni

Se si usa la **rete per la distribuzione di contenuti di Azure da Akamai**, è necessario usare il download di file di grandi dimensioni per distribuire file più grandi di 1,8 GB. La **rete per la distribuzione di contenuti di Azure da Verizon** non prevede un limite alla dimensione del download di file nell'ottimizzazione della distribuzione Web generale.

Se si usa la **rete per la distribuzione di contenuti di Azure da Akamai**, il download di file di grandi dimensioni è ottimizzato per contenuti più grandi di 10 MB. Se la dimensione media dei file è inferiore a 10 MB, è possibile usare la distribuzione Web generale. Se la dimensioni media dei file è costantemente superiore a 10 MB potrebbe essere più efficiente creare un endpoint separato per i file di grandi dimensioni. Ad esempio, gli aggiornamenti firmware o software sono in genere file di grandi dimensioni.

La **rete per la distribuzione di contenuti di Azure da Verizon** usa l'ottimizzazione di tipo distribuzione Web generale per distribuire il contenuto del download di file di grandi dimensioni.

Per altre informazioni sull'ottimizzazione di file di grandi dimensioni vedere [Ottimizzazione di file di grandi dimensioni](cdn-large-file-optimization.md).

### <a name="dynamic-site-acceleration"></a>Accelerazione sito dinamico

 L'accelerazione sito dinamico è disponibile nei profili sia della **rete per la distribuzione di contenuti di Azure da Akamai** che della **rete per la distribuzione di contenuti di Azure da Verizon**. Per usare questa ottimizzazione, viene applicata una tariffa aggiuntiva. Per altre informazioni, vedere [Prezzi della rete per la distribuzione di contenuti](https://azure.microsoft.com/pricing/details/cdn/).

L'accelerazione di sito dinamico include diverse tecniche che sfruttano la latenza e le prestazioni di contenuto dinamico. Le tecniche includono l'ottimizzazione di route e rete, l'ottimizzazione TCP e molto altro. 

Per accelerare un'app Web che include numerose risposte non memorizzabili nella cache, è possibile usare questa ottimizzazione. I risultati di ricerca, le transazioni di checkout o i dati in tempo reale sono degli esempi. È possibile continuare a usare le funzionalità di base di memorizzazione nella cache della rete per la distribuzione di contenuti per i dati statici. 

Per altre informazioni sull'accelerazione sito dinamico, vedere [Accelerazione sito dinamico](cdn-dynamic-site-acceleration.md).



