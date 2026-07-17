# Seamless Permission Service

## Table of Contents
  * [Ülevaade](#ülevaade)
    * [Kasutusjuht](#kasutusjuht)
    * [Kliendi teekond](#kliendi-teekond)
    * [Antavad õigused](#antavad-õigused)
  * [Integratsioon](#integratsioon)
    * [Tagasisuunamine](#tagasisuunamine)
    * [Lubatud URL-id ja whitelistimine](#lubatud-URL-id-ja-whitelistimine)
    * [Uue turuosalise liidestamine](#uue-turuosalise-liidestamine)
  * [Kliendi teekond kliendiportaalis](#kliendi-teekond-kliendiportaalis)

## Overview

The Seamless Permission Service enables an electricity supplier to direct a customer from its self-service portal directly to the Estfeed Customer Portal, where the customer can grant permission to share their metering data and metering point technical data with the supplier.

The solution works similarly to online banking authentication flows. The customer is redirected from the supplier’s self-service portal to the Estfeed Customer Portal, grants the required permissions, and is then automatically redirected back to the service provider's environment.

The purpose of the service is to make the data-sharing process as simple and fast as possible for the customer.

### Use Case

The service is intended for situations where a customer wishes to share their data before signing a contract or during the contract signing process.

For example, an electricity supplier may require access to the customer's metering data in order to prepare an offer. In such cases, the customer does not need to visit the Estfeed Customer Portal separately but can provide consent directly as part of a process initiated from the supplier's self-service portal.

### Customer Journey

The Seamless Permission process consists of the following steps:

1. The customer initiates the process in the market participant's self-service portal.
2. The customer is redirected to the Estfeed Customer Portal.
3. The customer authenticates in the Estfeed Customer Portal.
4. If multiple roles are available, the customer selects the role in which they wish to act. For example, when representation rights have been delegated to them or they have representation rights for a company.
5. The customer selects the metering points for which they wish to share data.
6. The customer is presented with a summary of the permissions to be granted.
7. The customer confirms the consent.
8. The customer is shown a message indicating whether the consent was successfully created or not.
9. The customer is redirected back to the service provider’s environment.

### Granted Rights

The consent grants access to:

- metering data from the previous 12 months;
- technical data of the metering point;

The created consent is valid for 48 hours.

Access to 12 months of historical data is only available if the customer’s network contract has been active for at least 12 months. If the contract has been active for a shorter period, access is limited to the available data for that period. If the customer’s network contract starts in the future, the customer cannot create a consent granting access to their data.

## Integration

To use the service, the market participant must redirect the customer to the Estfeed Customer Portal using a dedicated URL. For example:

`https://estfeed.elering.ee/grant?eic=38X-XXXXXXXXX&energy_type=Electricity&redirect_uri=https://iseteenindus.turuosaline.ee/uus-leping`

The following parameters are passed during the redirection:

| Parameter | Description |
|------------|-----------|
| `eicCode` | EIC code of the company that should receive access to the data. |
| `energyType` | Energy type (`electricity` or `gas`) |
| `redirectUrl` | URL to which the customer will be redirected after the process is completed |
| `showBackButton` | Determines whether the **"Back to Service Provider"** button is displayed to the user. The value is generally set to `true`. |

### Redirection

After the consent has been granted, the customer is shown a result page.

If a redirection URL has been specified:

- a **"Back to Service Provider"** button is displayed;
- if the customer does not click the button within 5 seconds, they are automatically redirected to the configured URL.

### Allowed URLs and Whitelisting

For security reasons, customers can only be redirected to pre-approved addresses after completing the consent process.

All `redirectUrl` values must be registered in the Estfeed allowed URL list (whitelist) at the domain level.

If the redirect address is not included in the whitelist, no redirection will take place.

The whitelist is managed by Elering.

### Onboarding a New Market Participant

The process for enabling the service is as follows:

1. Coordinate the use of the solution with Elering by sending an email to datahub@elering.ee. Include the following information in your email:
   - your EIC code;
   - test environment redirect URLs (at domain level) that you wish to use during testing;
   - production environment redirect URLs (at domain level).

2. Elering will whitelist your EIC code and URLs and inform you once the changes have been completed.

3. The solution will then be available for your use. We recommend testing the integration in the Estfeed Customer Portal test environment before going live.

## Customer Journey in the Customer Portal

The following screenshots illustrate what the user journey looks like in the customer portal.

![Esimene samm nõusoleku andmisel](../images/client-portal/permission-service/sujuv-nõusolek-step-1-blur.png)
![Teine samm nõusoleku andmisel](../images/client-portal/permission-service/sujuv-nõusolek-step-2-blur.png)
![kolmas samm nõusoleku andmisel](../images/client-portal/permission-service/sujuv-nousolek-step-3-redacted.png)