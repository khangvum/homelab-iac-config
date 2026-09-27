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

|    Field     | Setting                   |
| :----------: | :------------------------ |
|   **Name**   | `Portainer`               |
| **Provider** | Select `Portainer - OIDC` |

## 2. Portainer OAuth Configuration

- Log in to the Portainer instance as an **_Administrator_**.
- Navigate to **Settings** > **Authentication**.
- Under **Authentication method**, select **OAuth**, and configure the following settings.

  |              Field              | Value       |
  | :-----------------------------: | :---------- |
  |           **Use SSO**           | **Enabled** |
  | **Automatic user provisioning** | **Enabled** |

- Under **Provider**, select **Custom**.
- Under **OAuth Configuration**, configure the following settings:

|         Field         | Value                                                                 |
| :-------------------: | :-------------------------------------------------------------------- |
|     **Client ID**     | (Paste the **_Client ID_** from Authentik)                            |
|   **Client secret**   | (Paste the **_Client Secret_** from Authentik)                        |
| **Authorization URL** | `https://authentik.khangvum.com/application/o/authorize/`             |
| **Access token URL**  | `https://authentik.khangvum.com/application/o/token/`                 |
|   **Resource URL**    | `https://authentik.khangvum.com/application/o/userinfo`               |
|   **Redirect URL**    | `https://portainer.khangvum.com/`                                     |
|    **Logout URL**     | `https://authentik.khangvum.com/application/o/portainer/end-session/` |
|  **User identifier**  | `preferred_username`                                                  |
|      **Scopes**       | `openid profile email`                                                |

> [!IMPORTANT]
> Ensure the **Redirect URL** path terminates correctly with the trailing slash or matches the exact Authentik application endpoint provider path.

### References

[Integrate with Portainer](https://integrations.goauthentik.io/hypervisors-orchestrators/portainer/#what-is-portainer)
