---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAML SSO for Bitbucket di resolution GmbH | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e SAML SSO for Bitbucket di resolution GmbH.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: fc947df1-f24e-43ae-9a34-518293583d69
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/04/2017
ms.author: jeedes
ms.openlocfilehash: 52c741c66a796e53698a690c415cc60c814f74e8
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-bitbucket-by-resolution-gmbh"></a>Esercitazione: Integrazione di Azure Active Directory con SAML SSO for Bitbucket di resolution GmbH

Questa esercitazione spiega come integrare la funzionalità SAML SSO for Bitbucket di resolution GmbH con Azure Active Directory (Azure AD).

L'integrazione di SAML SSO for Bitbucket di resolution GmbH con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi ha accesso a SAML SSO for Bitbucket di resolution GmbH.
- È possibile abilitare gli utenti per l'accesso automatico a SAML SSO for Bitbucket di resolution GmbH, ovvero per il Single Sign-On, con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>prerequisiti

Per configurare l'integrazione di Azure AD con SAML SSO for Bitbucket di resolution GmbH, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Una sottoscrizione attiva di SAML SSO for Bitbucket di resolution GmbH

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di SAML SSO for Bitbucket di resolution GmbH dalla raccolta
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-saml-sso-for-bitbucket-by-resolution-gmbh-from-the-gallery"></a>Aggiunta di SAML SSO for Bitbucket di resolution GmbH dalla raccolta
Per configurare l'integrazione di SAML SSO for Bitbucket di resolution GmbH in Azure AD, è necessario aggiungere SAML SSO for Bitbucket di resolution GmbH dalla raccolta all'elenco di app SaaS gestite.

**Per aggiungere SAML SSO for Bitbucket di resolution GmbH dalla raccolta, eseguire la procedura seguente:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Pulsante Azure Active Directory][1]

2. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![Pannello Applicazioni aziendali][2]
    
3. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![Pulsante Nuova applicazione][3]

4. Nella casella di ricerca digitare **SAML SSO for Bitbucket di resolution GmbH**, selezionare **SAML SSO for Bitbucket by resolution GmbH** dal riquadro dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![SAML SSO for Bitbucket di resolution GmbH nel riquadro dei risultati](./media/active-directory-saas-bitbucket-tutorial/tutorial_bitbucket_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAML SSO for Bitbucket di resolution GmbH tramite l'utente di test "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere il nome dell'utente controparte in SAML SSO for Bitbucket di resolution GmbH corrispondente all'utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in SAML SSO for Bitbucket di resolution GmbH.

Per stabilire la relazione di collegamento, in SAML SSO for Bitbucket di resolution GmbH assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On di Azure AD con SAML SSO for Bitbucket di resolution GmbH, è necessario completare i blocchi predefiniti seguenti:

1. **[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.
2. **[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
3. **[Creare un utente di test di SAML SSO for Bitbucket di resolution GmbH](#create-a-saml-sso-for-bitbucket-by-resolution-gmbh-test-user)**: per avere una controparte di Britta Simon in SAML SSO for Bitbucket di resolution GmbH che sia collegata alla rappresentazione di Azure AD dell'utente.
4. **[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
5. **[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione SAML SSO for Bitbucket di resolution GmbH.

**Per configurare l'accesso Single Sign-On di Azure AD con SAML SSO for Bitbucket di resolution GmbH, eseguire la procedura seguente:**

1. Nella pagina di integrazione dell'applicazione **SAML SSO for Bitbucket di resolution GmbH** del portale di Azure fare clic su **Single Sign-On**.

    ![Collegamento Configura accesso Single Sign-On][4]

2. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-bitbucket-tutorial/tutorial_bitbucket_samlbase.png)

3. Nella sezione **URL e dominio SAML SSO for Bitbucket di resolution GmbH**, se si vuole configurare l'applicazione in modalità avviata da IDP, eseguire la procedura seguente:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On in SAML SSO for Bitbucket di resolution GmbH](./media/active-directory-saas-bitbucket-tutorial/tutorial_bitbucket_url.png)

    a. Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<server-base-url>/plugins/servlet/samlsso`

    b. Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<server-base-url>/plugins/servlet/samlsso`

4. Selezionare **Mostra impostazioni URL avanzate** e seguire questa procedura se si vuole configurare l'applicazione in modalità avviata da **SP**:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On in SAML SSO for Bitbucket di resolution GmbH](./media/active-directory-saas-bitbucket-tutorial/tutorial_bitbucket_url1.png)

    Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<server-base-url>/plugins/servlet/samlsso`
     
    > [!NOTE] 
    > Poiché questi non sono i valori reali, è necessario aggiornarli con l'identificatore, l'URL di risposta e l'URL di accesso effettivi. Per ottenere questi valori, contattare il [team di assistenza per il client di SAML SSO for Bitbucket di resolution GmbH](https://marketplace.atlassian.com/plugins/com.resolution.atlasplugins.samlsso-bitbucket/server/support). 

5. Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.

    ![Collegamento di download del certificato](./media/active-directory-saas-bitbucket-tutorial/tutorial_bitbucket_certificate.png) 

6. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-bitbucket-tutorial/tutorial_general_400.png)
    
7. Accedere al sito aziendale SAML SSO for Bitbucket di resolution GmbH come amministratore.

8. Sul lato destro della barra degli strumenti principale fare clic su **Impostazioni**.

9. Passare alla sezione ACCOUNT e fare clic su **SAML SingleSignOn** sulla barra dei menu.

    ![SAML SingleSignOn](./media/active-directory-saas-bitbucket-tutorial/tutorial_bitbucket_samlsingle.png)

10. Nella pagina **SAML SingleSignOn Plugin Configuration** (Configurazione plug-in SAML SingleSignOn) fare clic su **Add idp** (Aggiungi IdP). 

    ![Add idp (Aggiungi IdP)](./media/active-directory-saas-bitbucket-tutorial/tutorial_bitbucket_addidp.png)

11. Nella pagina **Choose your SAML Identity Provider** (Scegliere il provider di identità SAML) eseguire la procedura seguente:

    ![Provider di identità](./media/active-directory-saas-bitbucket-tutorial/tutorial_bitbucket_identityprovider.png)

    a. Come **Idp Type** (Tipo IdP) selezionare **AZURE AD**.

    b. Nella casella di testo **Name** (Nome) digitare un nome.

    c. Nella casella di testo **Description** (Descrizione) digitare la descrizione.

    d. Fare clic su **Avanti**.

12. Nella pagina **Identity provider configuration** (Configurazione provider di identità) fare clic su **Next** (Avanti).

    ![Configurazione identità](./media/active-directory-saas-bitbucket-tutorial/tutorial_bitbucket_identityconfig.png)

13.  Nella pagina **Import SAML Idp Metadata** (Importa metadati IdP SAML) fare clic su **Load File** (Carica file) per caricare il file **METADATA XML** scaricato dal portale di Azure.

    ![idpmetadata](./media/active-directory-saas-bitbucket-tutorial/tutorial_bitbucket_idpmetadata.png)
    
14. Fare clic su **Avanti**.

15. Fare clic su **Save settings** (Salva impostazioni).

    ![Salvataggio](./media/active-directory-saas-bitbucket-tutorial/tutorial_bitbucket_save.png)

> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

   ![Creare un utente test di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.

    ![Pulsante Azure Active Directory](./media/active-directory-saas-bitbucket-tutorial/create_aaduser_01.png)

2. Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-bitbucket-tutorial/create_aaduser_02.png)

3. Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.

    ![Pulsante Aggiungi](./media/active-directory-saas-bitbucket-tutorial/create_aaduser_03.png)

4. Nella finestra di dialogo **Utente** seguire questa procedura:

    ![Finestra di dialogo Utente](./media/active-directory-saas-bitbucket-tutorial/create_aaduser_04.png)

    a. Nella casella **Nome** digitare **BrittaSimon**.

    b. Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.

    c. Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.

    d. Fare clic su **Crea**.
 
### <a name="create-a-saml-sso-for-bitbucket-by-resolution-gmbh-test-user"></a>Creare un utente di test di SAML SSO for Bitbucket di resolution GmbH

L'obiettivo di questa sezione è creare l'utente Britta Simon in SAML SSO for Bitbucket di resolution GmbH. SAML SSO for Bitbucket di resolution GmbH supporta il provisioning JIT e anche la creazione manuale di utenti. Contattare il [team di assistenza per il client SAML SSO for Bitbucket di resolution GmbH](https://marketplace.atlassian.com/plugins/com.resolution.atlasplugins.samlsso-bitbucket/server/support) in base ai propri requisiti.

### <a name="assign-the-azure-ad-test-user"></a>Assegnare l'utente test di Azure AD

In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a SAML SSO for Bitbucket di resolution GmbH.

![Assegnare il ruolo utente][200] 

**Per aggiungere Britta Simon a SAML SSO for Bitbucket di resolution GmbH, eseguire la procedura seguente:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco delle applicazioni selezionare **SAML SSO for Bitbucket by resolution GmbH** (SAML SSO for Bitbucket di resolution GmbH).

    ![Collegamento SAML SSO for Bitbucket di resolution GmbH nell'elenco delle applicazioni](./media/active-directory-saas-bitbucket-tutorial/tutorial_bitbucket_app.png)  

3. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Collegamento "Utenti e gruppi"][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Riquadro Aggiungi assegnazione][203]

5. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro di SAML SSO for Bitbucket di resolution GmbH nel riquadro di accesso, si effettua automaticamente l'accesso all'applicazione SAML SSO for Bitbucket di resolution GmbH.
Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bitbucket-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bitbucket-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bitbucket-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bitbucket-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bitbucket-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bitbucket-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bitbucket-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bitbucket-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bitbucket-tutorial/tutorial_general_203.png

