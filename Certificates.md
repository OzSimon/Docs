# Introduction

As an administrator, ensuring secure network communication is crucial. One way to achieve this is through secure certificates. CA-signed certificates, issued by trusted third parties, offer high security but can be costly and sometimes unnecessary. In these cases, a self-signed public certificate is a cost-effective and convenient alternative.

Self-signed certificates are ideal for testing and provide a secure solution for administrators needing certificate-based security. With just a single PowerShell cmdlet, you can create an SSL certificate that meets your needs.

This documentation provides a comprehensive guide on creating certificates for various purposes, simplifying the process for administrators.

Creating your own SSL certificate is straightforward. With the New-SelfSignedCertificate cmdlet, you can quickly generate a self-signed certificate.

```powershell
$Certificate = New-SelfSignedCertificate –Subject Contoso.com -CertStoreLocation Cert:\CurrentUser\My 
```

The cmdlet above will create a self-signed SSL server authentication certificate for the domain Contoso.com in the current user's certificate store. By default, the certificate is valid for one year, but you can adjust the expiry using the NotAfter parameter. Additional parameter details will be covered later.

> [NOTE!] **Note**: Creating a certificate in the current user store makes it available only to the current user. To make it available to all users on the local machine, create the certificate in Cert:\LocalMachine\My.
