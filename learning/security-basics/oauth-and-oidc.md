# OAuth and OIDC

#### O Auth 2.0

[OAuth 2.0](https://oauth.net/2/) is an industry-standard protocol for authorization that provides a secure way for applications to access user data or perform actions on behalf of the user without requiring the user to share their credentials directly with the application. OAuth 2.0 allows users to grant limited access to their accounts or resources to third-party applications through an authorization server.

The significance of OAuth 2.0 lies in its ability to enhance security and user privacy while enabling seamless integration of third-party services. By leveraging OAuth 2.0, users can selectively grant permissions to applications without exposing their credentials, reducing the risk of credential theft or misuse. Additionally, OAuth 2.0 simplifies the authentication process for users, as they only need to authenticate with the authorization server once, rather than providing their credentials to multiple applications. This protocol has become widely adopted across various platforms and industries, enabling specific authorization flows for web applications, desktop applications, mobile phones, and living room devices.

<figure><img src="../../.gitbook/assets/abstract_flow.png" alt=""><figcaption></figcaption></figure>

#### **OpenID Connect (OIDC)**

While OAuth 2.0 focuses on authorization, [OIDC](https://www.microsoft.com/en-us/security/business/security-101/what-is-openid-connect-oidc) adds an identity layer to the process, allowing applications to receive identity information from an authorization server.

The significance of OIDC lies in its ability to simplify the authentication process for both developers and users. By leveraging OIDC, developers can offload the complex task of managing user identities to a trusted identity provider, reducing the risk of security vulnerabilities and ensuring compliance with industry standards. For users, OIDC streamlines the login experience by allowing them to authenticate once with the identity provider and seamlessly access multiple applications without the need to create and manage separate credentials for each service.

OIDC provides a standardized format for identity tokens, which contain claims (pieces of information) about the authenticated user, such as their name, email address, and other relevant details. These tokens can be easily shared and verified by applications, enabling a more secure and efficient way of managing user identities across different platforms and services. As a result, OIDC has gained widespread adoption, particularly in enterprise environments and cloud-based applications, where secure and scalable identity management is crucial.

<figure><img src="../../.gitbook/assets/oidc-basic-flow.png" alt=""><figcaption></figcaption></figure>
