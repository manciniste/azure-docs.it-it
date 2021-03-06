---
title: File di inclusione
description: File di inclusione
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 03/21/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: e49cfe786272b34675ca377808e2961e61a757e4
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2018
---
È possibile connettersi a una VM distribuita nella rete virtuale creando una connessione Desktop remoto alla VM. Il modo migliore per verificare inizialmente che è possibile connettersi alla VM consiste nel connettersi usando il rispettivo indirizzo IP privato, invece del nome del computer. Ciò consente di verificare se è possibile connettersi, non se la risoluzione dei nomi è configurata correttamente. 

1. Individuare l'indirizzo IP privato per la VM. È possibile trovare l'indirizzo IP privato di una VM esaminando le proprietà per la VM nel portale di Azure oppure usando PowerShell.
2. Verificare di essere connessi alla rete virtuale con la connessione VPN da punto a sito. 
3. Aprire la connessione Desktop remoto digitando "RDP" o "Connessione Desktop remoto" nella casella di ricerca sulla barra delle applicazioni, quindi selezionare Connessione Desktop remoto. È anche possibile aprire una connessione Desktop remoto usando il comando "mstsc" in PowerShell. 
3. In Connessione Desktop remoto immettere l'indirizzo IP privato della VM. È possibile fare clic su "Mostra opzioni" per modificare altre impostazioni e quindi connettersi.

### <a name="to-troubleshoot-an-rdp-connection-to-a-vm"></a>Per risolvere i problemi di una connessione RDP a una VM

Se si verificano problemi di connessione a una macchina virtuale tramite la connessione VPN, è possibile controllare alcuni elementi. Per altre informazioni sulla risoluzione dei problemi, vedere l'articolo su come [risolvere i problemi delle connessioni Desktop remoto a una VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).

- Verificare che la connessione VPN sia attiva.
- Verificare che venga effettuata la connessione all'indirizzo IP privato per la VM.
- Usare "ipconfig" per controllare l'indirizzo IPv4 assegnato alla scheda Ethernet nel computer da cui viene effettuata la connessione. Se l'indirizzo IP è compreso nell'intervallo di indirizzi della rete virtuale a cui ci si connette o nell'intervallo di indirizzi del pool di indirizzi del client VPN, si verifica la cosiddetta sovrapposizione dello spazio indirizzi. Con questo tipo di sovrapposizione, il traffico di rete non raggiunge Azure e rimane nella rete locale.
- Se è possibile connettersi alla VM usando l'indirizzo IP privato, ma non il nome del computer, verificare di avere configurato correttamente il valore per DNS. Per altre informazioni sul funzionamento della risoluzione dei nomi per le macchine virtuali, vedere [Risoluzione dei nomi per le macchine virtuali](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
- Verificare che il pacchetto di configurazione del client VPN sia stato generato dopo che sono stati specificati gli indirizzi IP del server DNS per la rete virtuale. Se gli indirizzi IP del server DNS sono stati aggiornati, generare e installare un nuovo pacchetto di configurazione del client VPN.