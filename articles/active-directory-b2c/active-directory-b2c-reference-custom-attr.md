---
title: 'Azure Active Directory B2C: attributi personalizzati | Documentazione Microsoft'
description: Come utilizzare gli attributi personalizzati in Azure Active Directory B2C per raccogliere informazioni sugli utenti
services: active-directory-b2c
documentationcenter: ''
author: davidmu1
manager: mtillman
editor: ''
ms.service: active-directory-b2c
ms.workload: identity
ms.topic: article
ms.date: 12/06/2016
ms.author: davidmu
ms.openlocfilehash: 6f285c10b7d8ff92c8568c42b6a78dc4ea9bcc74
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2018
---
# <a name="azure-active-directory-b2c-use-custom-attributes-to-collect-information-about-your-consumers"></a>Azure Active Directory B2C: usare attributi personalizzati per raccogliere informazioni sugli utenti
La directory Azure Active Directory (Azure AD) B2C viene fornita con un set predefinito di informazioni (attributi), ad esempio nome, cognome, città, codice postale e altri attributi. Tuttavia, ogni applicazione consumatori ha requisiti specifici relativi agli attributi da raccogliere. Con Azure AD B2C, è possibile estendere il set di attributi archiviati in ogni account utente. È possibile creare attributi personalizzati nel [portale di Azure](https://portal.azure.com/) e usarli nei criteri di iscrizione, come illustrato di seguito. Questi attributi possono anche essere scritti e letti usando l' [API Graph di Azure AD](active-directory-b2c-devquickstarts-graph-dotnet.md).

> [!NOTE]
> Gli attributi personalizzati usano le [Estensioni dello schema di directory dell'API Graph di Azure AD](https://msdn.microsoft.com/library/azure/dn720459.aspx).
> 
> 

## <a name="create-a-custom-attribute"></a>Creare un attributo personalizzato
1. [Seguire questa procedura per passare al pannello delle funzionalità B2C nel portale di Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Fare clic su **Attributi utente**.
3. Fare clic su **+Aggiungi** nella parte superiore del pannello.
4. Fornire un **Nome** per l'attributo personalizzato (ad esempio, "ShoeSize") e, facoltativamente, una **Descrizione**. Fare clic su **Crea**.
   
   > [!NOTE]
   > Come **tipi di dati** sono attualmente disponibili solo "String", "Boolean" e "Int".
   > 
   > 

L'attributo personalizzato è ora disponibile nell'elenco degli **Attributi utente**e per l'uso nei criteri di iscrizione.

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a>Usare un attributo personalizzato nei criteri di iscrizione
1. [Seguire questa procedura per passare al pannello delle funzionalità B2C nel portale di Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Fare clic su **Criteri di iscrizione**.
3. Fare clic sul criterio di iscrizione (ad esempio, "B2C_1_SiUp") per aprirlo. Fare clic su **Modifica** nella parte superiore del pannello.
4. Fare clic su **Attributi iscrizione** e selezionare l'attributo personalizzato (ad esempio, "ShoeSize"). Fare clic su **OK**.
5. Fare clic su **Attestazioni applicazione** e selezionare l'attributo personalizzato. Fare clic su **OK**.
6. Fare clic su **Salva** nella parte superiore del pannello.

È possibile utilizzare la funzionalità "Esegui ora" nei criteri per verificare l'esperienza utente. Ora si dovrebbe vedere "ShoeSize" nell'elenco di attributi che vengono raccolti durante l'iscrizione dell’utente e nel token inviato all'applicazione.

## <a name="notes"></a>Note
* Insieme ai criteri di iscrizione, gli attributi personalizzati possono essere usati anche nei criteri di iscrizione o accesso e nei criteri di modifica del profilo.
* Esiste una limitazione nota degli attributi personalizzati. Si verifica solo la prima volta che viene usato in un criterio e non quando viene aggiunto all'elenco di **Attributi utente**.

