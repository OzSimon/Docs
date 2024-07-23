# Self-Signed Certificate with PowerShell

## Introduction

As an administrator, ensuring secure network communication is crucial. One way to achieve this is through secure certificates. CA-signed certificates, issued by trusted third parties, offer high security but can be costly and sometimes unnecessary. In these cases, a self-signed public certificate is a cost-effective and convenient alternative.

Self-signed certificates are ideal for testing and provide a secure solution for administrators needing certificate-based security. With just a single PowerShell cmdlet, you can create an SSL certificate that meets your needs.

This documentation provides a comprehensive guide on creating certificates for various purposes, simplifying the process for administrators.

## Creating Your Own SSL Certificate with PowerShell

Creating your own SSL certificate is straightforward. With the **New-SelfSignedCertificate** cmdlet, you can quickly generate a self-signed certificate.

```powershell
$Certificate = New-SelfSignedCertificate –Subject Contoso.com -CertStoreLocation Cert:\CurrentUser\My 
```

The cmdlet above will create a self-signed SSL server authentication certificate for the domain Contoso.com in the current user's certificate store. By default, the certificate is valid for one year, but you can adjust the expiry using the NotAfter parameter. Additional parameter details will be covered later.

> [!NOTE]
> **Note**: Creating a certificate in the current user store makes it available only to the current user. To make it available to all users on the local machine, create the certificate in Cert:\LocalMachine\My.

## Exporting a Self-Signed Certificate with PowerShell

To export the certificate from the certificate store to a file, use the **Export-Certificate** cmdlet.

The $Certificate variable from the previous command stores your Certificate in the current session, allowing you to export it.

Now, the certificate is exported and stored at the specified FilePath.

To export a specific certificate, you can use the following example:

```powershell
$CertificateName = Contoso
$CertificateThumbprint = AB1C2D3E4F5G6H7I8J9K0L1M2N3O4P5Q6R7S8T9U0V1W2X3Y4Z5
$Certificate = Get-ChildItem –Path Cert:\CurrentUser\My\$CertificateThumbprint
Export-Certificate -Cert $Certificate -FilePath "C:\Users\Administrator\Desktop\$CertificateName.cer" 
```

To export all certificates from the cert:\CurrentUser\my store, run the following cmdlet:

```powershell
Get-ChildItem -Path Cert:\CurrentUser\My | Export-Certificate -FilePath C:\Certs\AllCertificates.sst  
```

> [!NOTE]
> When exporting a single certificate, the default format is **CER**. When exporting multiple certificates, the default format is **SST**. You can use the Type parameter to change the file type.
