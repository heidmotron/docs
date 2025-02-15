---
title: Single-Tenant Authentication and Self-Service SAML SSO
keywords: administration
tags: [integrations, administration]
sidebar: doc_sidebar
permalink: auth_self_service_sso.html
summary: Learn how to enable single-tenant authentication and set up self-service SSO.
---

Tanzu Observability by Wavefront supports a number of third-party authentication solutions that use SAML. The SAML (Security Assertion Markup Language) standard enables an identity provider (IdP) to pass authorization credentials to service providers (SP). In environments that use SAML, users log in once and authenticate to many different services.

* Self-Service SAML SSO is not available for customers who have set up [multi-tenant authentication](authentication.html#multi-tenant-authentication).
* Self-Service SAML SSO is not available for trial customers.

{% include tip.html content="If you set up SAML SSO for your environment, user accounts can no longer sign in with their user name and password. They must log in through the IdP. Service accounts can continue to use their authentication tokens."%}

## Single-Tenant Authentication

Most administrators set up authentication in their environment by setting up SSO using an identity provider (IdP). Authentication integrations with the following IdPs are predefined. SSO setup with other IdPs is also possible.

* [ADFS](adfs.html)
* [Azure AD](azure_ad.html)
* [Google](google.html)
* [OneLogin](onelogin.html)
* [Okta](okta.html)
* [PingOne](pingone.html)
* [VMware Workspace ONE Access](workspace-one.html).

As an administrator, in single-tenant authentication environments, you can set up SAML SSO and your users will log in to the identity provider. After a user has been successfully authenticated, you can set the permissions for that user. [Permissions](permissions_overview.html) determine what the user can do in the environment.

## Set Up SAML SSO

{% include note.html content="You must have **SAML IdP Admin** permission to set up SAML SSO for your Wavefront instance."%}

1. Log in to your Wavefront instance as a user with the **SAML IdP Admin** permission.
2. Click the gear icon <i class="fa fa-cog"/> on the toolbar and select **Self Service SAML**.
3. From the **Identity Provider** drop-down menu, select the identity provider that is used in your environment.
4. Click the **Setup Instructions** link. 
   
   The link directs you to the instructions for setting up the provider integration that you selected.
   
5. Follow the instructions to retrieve the metadata for your identity provider.
6. In the **Configure Connection** field, paste the metadata and click **Test** to validate the metadata.
7. Log in to your identity provider.
   
   After the login is successful and if the test was successful, the **Save** button becomes available.
   
8. Click the **Save** button to save your changes.

![screenshot with fields filled in & blurred out](images/self_service_sso.png)


## Update SAML SSO

If the certificate that's used in your setup must be replaced, you can delete the existing setup and set up SAML SSO again.

1. Log in to your Wavefront instance as a user with the **SAML IdP Admin** permission.
2. From the gear icon <i class="fa fa-cog"/> on the toolbar, select **Self Service SAML**.
3. Click the **Click Here** link to delete the existing key pair.
4. Repeat the setup process.

{% include tip.html content="If the certificate that is used in the SSO setup has expired and you are unable to authenticate and perform the required changes, [engage our Support team](wavefront_support_feedback.html#support) to request that the SSO integration be deactivated. After that, authenticate by using a user name and password to set up SSO again with the updated metadata."%}

<!---
## FedRAMP Certification of Different Providers

The different SAML providers have the following FedRAMP certification:

* ADFS – FedRAMP High.
* G-Suite – FedRAMP Moderate.
* Okta – FedRAMP Moderate.
* WorkSpaceOne - FedRAMP Moderate.
* OneLogin – No FedRAMP compliance.

--->
