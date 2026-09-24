# Portainer-Authentik Integration Guide

A comprehensive guide to **_integrating Authentik OIDC_** with an **_Portainer_** photo backup instance in a homelab environment.

## 1. Authentik Configuration

### Provider Setup

- Navigate to **Applications** > **Providers** and create an **_OAuth2/OpenID Provider_**.
- Fill out the details:

|                   Field                   | Setting                                                                   |
| :---------------------------------------: | :------------------------------------------------------------------------ |
|                 **Name**                  | `Portainer - OIDC`                                                        |
|          **Authorization Flow**           | `default-provider-authorization-explicit-consent (Authorize Application)` |
|              **Client Type**              | `Confidential`                                                            |
| **Redirect URIs/Origins (Authorization)** | `https://portainer.khangvum.com/`                                         |

> [!IMPORTANT]
> Copy the generated **_Client ID_** and **_Client Secret_**, which are needed for Immich configuration later.

### Application Setup

- Navigate to **Applications** > **Applications** and create a **_New Application_**:
- Fill out the details:

|     Field      | Setting                       |
| :------------: | :---------------------------- |
|    **Name**    | `Portainer`                      |
|  **Provider**  | Select `Portainer - OIDC`        |

### References

[Integrate with Portainer](https://integrations.goauthentik.io/hypervisors-orchestrators/portainer/#what-is-portainer)
