# Azure AD B2C Home Realm Discovery using Custom Domainsb2c-custom-domain-home-realm-discovery

This is an example custom policy for doing home realm discovery using [custom domains](https://learn.microsoft.com/en-us/azure/active-directory-b2c/custom-domain). This will allow you to automatically pre-select the identity provider that you'd like the user to sign in with based on what domain they are accessing B2C with. 

Prerequisites: 

### Prerequisites

- You must first setup your B2C tenant for use by custom policies and deploy the custom policy [starter pack](https://learn.microsoft.com/en-us/azure/active-directory-b2c/tutorial-create-user-flows?pivots=b2c-custom-policy#get-the-starter-pack). This sample has dependencies on some claims and values found in the starter pack. You can automate this setup by using the [setup tool](https://aka.ms/iefsetup) if you already have an Azure AD B2C tenant and have not gone through the [setup steps](https://learn.microsoft.com/en-us/azure/active-directory-b2c/tutorial-create-user-flows?pivots=b2c-custom-policy) yet.

## A few things to note:

- This sample has 2 identity providers configured with dummy configuration values: Microsoft Accounts and Azure AD. You'll need to replace them with the identity providers that you are planning to use and configure them appropriately.
- This sample assumes you are using subdomains (ie customer1.contoso.com, customer2.contoso.com) and contains logic to parse the subdomain out into a claim called `customerId`. If you are using dedicated domains per customer (ie customer1.com, customer2.com, etc), you will need to modify this logic. 
- In typical home realm discovery using the user's email address domain, there is usually a default identity provider for the scenario in which B2C is provided an email it doesn't have a mapping for. Since we are using custom domains, we can assume that the mapping has already been done (since you have to set up the custom domains on a per tenant basis), so we should be able to assume we do not need a fallback identity provider. However, if your scenario is different, you may want to consider adding it back. Refer to the other home realm discovery samples below. 
- The mapping right now from subdomain -> identity provider is done in the B2C policy XML. This is a fine approach for a small number of subdomains, but if you have more, you may want to consider adding logic to call out to a REST API to do the mapping for you. 

Other resources/samples:

- [Host name validation](https://github.com/azure-ad-b2c/samples/tree/master/policies/check-host-name)
- ["Modern" home realm discovery](https://github.com/azure-ad-b2c/samples/tree/master/policies/home-realm-discovery-modern)