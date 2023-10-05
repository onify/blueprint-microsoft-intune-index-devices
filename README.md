![Onify Blueprints](https://files.readme.io/8ba3f14-onify-blueprints-logo.png)

[![Project Status: WIP – Initial development is in progress, but there has not yet been a stable, usable release suitable for the public.](https://www.repostatus.org/badges/latest/wip.svg)](https://www.repostatus.org/#wip)
![Test suite](https://github.com/onify/blueprint-microsoft-intune-index-devices/workflows/Test%20suite/badge.svg)

# Onify Blueprint: Index devices from Microsoft Intune

[Microsoft Intune](https://www.microsoft.com/security/business/microsoft-intune) is a cloud-based service that focuses on mobile device management (MDM) and mobile application management (MAM). It allows organizations to manage devices and applications across various platforms, including Windows, iOS, and Android. Intune integrates seamlessly with Azure Active Directory and Microsoft 365 to enable secure access to company resources. It offers features like remote wipe, policy enforcement, and software distribution to maintain security and compliance. Overall, Intune provides a centralized platform for managing a mobile workforce.

In this Blueprint we show how we can index devices from Microsoft Intune using Graph API integration.

![Onify Blueprint: Index devices from Microsoft Intune](blueprint.jpg "Blueprint")

## Requirements

* [Onify Hub](https://github.com/onify/install)
* [Camunda Modeler](https://camunda.com/download/modeler/)
* [Microsoft Intune](https://www.microsoft.com/security/business/microsoft-intune)

## Included

* 1 x Flow

## Setup

### Microsoft

To set up and get devices using the Microsoft Graph API endpoint `https://graph.microsoft.com/beta/deviceManagement`, you'll need to go through several steps. Here's a general outline:

#### Prerequisites
1. **Azure Subscription**: You need an Azure subscription to use Azure AD and register an application.
2. **Office 365 Subscription**: Required for device management through Microsoft Intune.
3. **Microsoft Intune**: Make sure you have Intune set up to manage your devices.

#### Register an Application in Azure AD
1. Go to the Azure portal and navigate to "Azure Active Directory".
2. Go to "App registrations" and click "New registration".
3. Fill in the details and click "Register".

#### Assign API Permissions
1. Once the app is registered, go to "API permissions".
2. Click "Add a permission" and choose "Microsoft Graph".
3. Under "Application permissions", add the permissions required for device management like `DeviceManagementConfiguration.ReadWrite.All`, `DeviceManagementServiceConfig.ReadWrite.All`, etc.

##### Generate Client Secret
1. Go to "Certificates & secrets" and click "New client secret".
2. Fill in the details and click "Add".

> The `/beta` version of the API is subject to change and should not be used in production.

### Onify

Add the following settings.

|Key|Name|Value|Type|Tag|Role|
|---|----|-----|----|---|----|
|_azure_intune_app_client_id|Microsoft Azure App Client ID|***|string|intune, azure|admin|
|_azure_intune_app_client_secret|Microsoft Azure App Client Secret|***|password|intune, azure|admin|
|_azure_intune_app_tenant_id|Microsoft Azure Tenant ID|***|string|intune, azure|admin|
|_azure_intune_select_fields|Fields to get for each device|id,deviceName,managedDeviceOwnerType,userId,complianceState,model,manufacturer,enrolledDateTime,lastSyncDateTime,operatingSystem,userDisplayName,userPrincipalName,managementState,deviceType,osVersion,aadRegistered,deviceEnrollmentType,serialNumber,managedDeviceName|string|intune, azure|admin|
|_azure_intune_url|Microsoft Azure Graph API endpoint for device management|https://graph.microsoft.com/beta/deviceManagement|string|intune, azure|admin|

> Note: Creating settings via admin interface add a trailing `_` in key. This is required for flow to work.

## Test

1. Open the BPMN diagram in Camunda Modeler.
2. Deploy the BPMN diagram (click `Deploy current diagram` and follow the steps).
3. Run it (click `Start current diagram`).

## Support

* Community/forum: https://support.onify.co/discuss
* Documentation: https://support.onify.co/docs
* Support and SLA: https://support.onify.co/docs/get-support

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.