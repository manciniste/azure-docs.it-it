---
title: "Come configurare l'Identità del servizio gestito in una macchina virtuale di Azure tramite il portale di Azure"
description: "Istruzioni dettagliate per la configurazione dell'Identità del servizio gestito in una macchina virtuale di Azure, tramite il portale di Azure."
services: active-directory
documentationcenter: 
author: daveba
manager: mtillman
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/15/2017
ms.author: daveba
ROBOTS: NOINDEX,NOFOLLOW
ms.openlocfilehash: 37710015904c8112e5d2de504ed5b42895ffb809
ms.sourcegitcommit: eeb5daebf10564ec110a4e83874db0fb9f9f8061
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="configure-a-vm-managed-service-identity-msi-using-the-azure-portal"></a>Configurare un'Identità del servizio gestito della macchina virtuale tramite il portale di Azure

[!INCLUDE[preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)]

Identità del servizio gestito offre servizi di Azure con un'identità gestita automaticamente in Azure Active Directory. È possibile usare questa identità per l'autenticazione a qualsiasi servizio che supporti l'autenticazione di Azure AD senza dover inserire le credenziali nel codice. 

In questo articolo si apprende come abilitare e rimuovere l'Identità del servizio gestito per una VM di Azure tramite il portale di Azure.

## <a name="prerequisites"></a>prerequisiti

[!INCLUDE [msi-core-prereqs](~/includes/active-directory-msi-core-prereqs-ua.md)]

## <a name="enable-msi-during-creation-of-an-azure-vm"></a>Abilitare l'Identità del servizio gestito durante la creazione di una macchina virtuale di Azure

Al momento della redazione del presente documento, l'abilitazione dell'Identità del servizio gestito durante la creazione di una macchina virtuale nel portale di Azure non è supportata. In alternativa, prima di creare una VM, vedere uno dei seguenti articoli di guida introduttiva sulla creazione di VM:

- [Creare una macchina virtuale Windows con il portale di Azure](~/articles/virtual-machines/windows/quick-create-portal.md#create-virtual-machine)
- [Creare una macchina virtuale Linux con il portale di Azure](~/articles/virtual-machines/linux/quick-create-portal.md#create-virtual-machine)  

Procedere quindi alla sezione successiva per informazioni dettagliate sull'abilitazione di MSI nella VM.

## <a name="enable-msi-on-an-existing-azure-vm"></a>Abilitare l'Identità del servizio gestito in una macchina virtuale di Azure esistente

Se si dispone di una macchina virtuale su cui è stato originariamente è stato eseguito il provisioning senza un'Identità del servizio gestito:

1. Accedere al [portale di Azure](https://portal.azure.com) usando un account associato alla sottoscrizione di Azure che contiene la VM. Assicurarsi anche che l'account appartenga a un ruolo che fornisce le autorizzazioni di scrittura nella VM, ad esempio "Collaboratore macchine virtuali".

2. Passare alla macchina virtuale desiderata.

2. Fare clic sulla pagina "Configurazione", abilitare l'Identità del servizio gestito nella macchina virtuale selezionando l'opzione "Sì" in "Managed service identity" (Identità del servizio gestito), quindi fare clic su **Salva**. Il completamento di questa operazione può richiedere circa 60 secondi:

   ![Schermata della pagina Configurazione](~/articles/active-directory/media/msi-qs-configure-portal-windows-vm/create-windows-vm-portal-configuration-blade.png)  

## <a name="remove-msi-from-an-azure-vm"></a>Rimuovere l'Identità del servizio gestito da una macchina virtuale di Azure

Se si dispone di una macchina virtuale per cui non è più necessaria un'Identità del servizio gestito:

1. Accedere al [portale di Azure](https://portal.azure.com) usando un account associato alla sottoscrizione di Azure che contiene la VM. Assicurarsi anche che l'account appartenga a un ruolo che fornisce le autorizzazioni di scrittura nella VM, ad esempio "Collaboratore macchine virtuali".

2. Passare alla macchina virtuale desiderata.

3. Fare clic sulla pagina "Configurazione", rimuovere l'Identità del servizio gestito dalla macchina virtuale selezionando l'opzione "No" in "Managed service identity" (Identità del servizio gestito), quindi fare clic su **Salva**. Il completamento di questa operazione può richiedere circa 60 secondi:

   ![Schermata della pagina Configurazione](~/articles/active-directory/media/msi-qs-configure-portal-windows-vm/create-windows-vm-portal-configuration-blade-disable.png)  

## <a name="related-content"></a>Contenuti correlati

- Per una panoramica dell'Identità di servizio gestito, vedere [Panoramica dell'Identità di servizio gestito](msi-overview.md).

## <a name="next-steps"></a>Passaggi successivi

- Tramite il portale di Azure, concedere all'Identità del servizio gestito della macchina virtuale di Azure l'[accesso a un'altra risorsa di Azure](msi-howto-assign-access-portal.md).

Usare la sezione dei commenti seguente per fornire commenti e suggerimenti utili per migliorare e organizzare i contenuti disponibili.
