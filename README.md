# Syncplicity_Connector_for_APIM

***WARNING: This policy is a work in progress that has been uploaded for collaborative purposes. The policy is a sample that works for integration in the context it was created, but is not ready for production use.***

Syncplicity SSO Documentation:
https://syncplicity.zendesk.com/hc/en-us/articles/202392804-Configuring-single-sign-on-SSO-

API Gateway SAML Documentation:
https://docs.axway.com/bundle/APIGateway_753_PolicyDevFilterReference_allOS_en_HTML5/page/Content/PolicyDevTopics/authn_saml_assertion.htm

# Description

Syncplicity allows companies of any size to leverage their existing corporate directories and authentication systems to authorize employee access to Syncplicity. The Syncplicity support for SSO is built on top of an industry-standard SAML 2.0 protocol. This widely supported protocol enables federated authentication between SaaS applications, like Syncplicity, and on-premise directory systems, such as Active Directory and LDAP. The key to SAML-based federated authentication is the intermediary server – often referred to as the Identity Provider (IdP). The IDP speaks the SAML 2.0 protocol and services actual authentication requests. In the context of this project, Syncplicity sees the API Gateway as the IDP, though in fact is is acting as an identity broker to one or more IDPs.

The Axway API Gateway can act as a federated authentication end point for Syncplicity, extending its default authentication and access control capabilities by mediating many supported credential types as a STS (security token service) and IDPs (identity providers) as an identity broker. It can enable the integration of one or many supported credentials (eg digital certificate/smartcards, OTP for mobile, biometrics), identity sources (eg AD, LDAP, Radiant Logic), and/or attribute repositories, from one or more sources (eg internal, partner, new M&A stores) in a single digital policy that returns the SAML 2.0 token to Syncplicity to authenticate a user.

The Axway API Gateway can also implement additional fine grain security, applying contextual logic in digital policy to apply different levels of security or SLA/Contractual controls. This may include decisions and enforcement based on things such as who is trying to access the resources, what type of device they are using, where they are coming from, what type of day or day of the week, and more. The Axway API Gateway can also extend this security further with integration into best in breed tools such as Elastic Beam API Behavioral Security, Axiomatics advanced dynamic authorization, and even the Axway Validation Authority for digital certificate validation.

This artifact is a prebuilt policy for the API Gateway that creates a SAML 2.0 token to authenticate an end user to Syncplicity, applying sample logic supporting MFA (multifactor authentication) with digital certificate and password, and digital certificate validation, before authenticating a user to the Syncplicity system.

# Implementation

- Import XML policy from the 'src' directory into the API Gateway. Update LDAP locations, digital signing certificates.
- Import the Syncplicity certificates from the 'src' directory into your API Gateway trust store (Env Config --> Certs/Keys --> Import CA).
- Configure your Syncplicity SSO configuration to point at your API Gateway and trust your signing certificate.
- Create the user(s) you wish to authenticate in Syncplicity.

# Troubleshooting

If you want to look into your SAMLResponse to verify your results, the SAML form data is deflated, Base64 encoded, and URL Encoded. To see it plain text, do these in the reverse order. This site has worked pretty well for me when testing this: https://www.samltool.com/decode.php
