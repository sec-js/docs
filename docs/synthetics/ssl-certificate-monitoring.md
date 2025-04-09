title: SSL/TLS Certificate Monitoring
description: Monitor & get notified on SSL/TLS certificate expiry and change. 

Issues with SSL/TLS certificates doesn't only cause downtime of APIs and websites, but also hurts their reputation. Sematext Synthetics performs the following SSL certificate checks on all the certificates in the chain - the leaf, intermediate, and root certificates.

* **Certificate Validation** - Validates the SSL certificates of the API/websites in every run
* **Certificate Expiry** - Checks for the expiration of the certificates every day and alerts you 28, 14, 7 and 3 days before the expiry
* **Certificate Change** - Checks for certificate change every 10 minutes and alerts you on detecting any changes, with a detailed change report
* **Certificate Authority** - Checks Root/Intermediate certificate authorities and alerts you if they don't match with the expected authority

Sematext Synthetics alerts you on the failure of these checks via the monitor's configured [alert notification hooks](/docs/alerts/alert-notifications). Apart from these checks, Synthetics also provides an SSL certificate report, with details of all the certificates in the chain.

Both the HTTP and Browser monitors perform these checks, though certificate change detection is available only for HTTP monitors.

## Certificate Validation

Synthetics performs a set of validity checks on SSL certificates sent by the server for every monitor run. Synthetics will mark the monitor status as failing if any of these checks fail. Synthetics will raise a run failure alert with the details of the failure. Self-signed certificates are not supported and any websites or APIs using self-signed certificates will fail unless you select the **Relaxed** type of SSL certificate check under **Configure Alerts** -> **SSL Monitoring**.

![Relaxed SSL certificate check](/docs/images/synthetics/ssl-check-type.png)

The HTTP monitor performs the following checks:

* If there is a valid chain, connecting the leaf certificate of the server to a trusted root
* Certificate has not expired
* Certificate is active (if the certificate is not used before its validity starts)
* Verify name constraints, if any
* Verify if there are too many intermediate certificates (more than 3 intermediates)
* Hostname validation, check if the hostname of the website/API is present in the list of allowed DNS names of the certificate

The Browser monitor loads the website in a real Google Chrome browser and performs all the checks done by the Google Chrome browser. We update the Chrome browser periodically, so that the list of checks stays up-to-date with recent implementations. Alongside all the checks above done by the HTTP monitor, the Browser monitor performs the following extra checks:

* Certificate is revoked
* Certificate uses a weak signature algorithm (e.g. SHA-1)
* Certificate authority is not trusted
* Certificate validity is too long
* Certificate uses a weak key ( e.g. too small RSA key)
* Certificate has Certificate Transparency data

## Certificate Expiry

Sematext Synthetics checks the certificate expiry every day and alerts you via the monitor's configured [alert notification hooks](/docs/alerts/alert-notifications) multiple times before it expires. We make sure you're reminded about the expiry multiple times.

You can set the certificate expiry alert condition within the Conditions tab for both HTTP and Browser monitors

![Certificate expiry BM](/docs/images/synthetics/cert-expiry2.png)

Or from SSL Monitoring tab for HTTP Monitors

![Relaxed SSL certificate check](/docs/images/synthetics/ssl-check-type.png)

The monitor performs the expiry check for all the certificates in the chains - leaf, intermediate, or root certificates. The **Monitor Overview** page displays the expiry time of the recently expiring certificate.

![Certificate expiry](/docs/images/synthetics/cert-expiry.png)

## Certificate Authority

Sematext Synthetics checks the certificate authority for both Root or Intermediate level and alerts you via the monitor's configured [alert notification hooks](/docs/alerts/alert-notifications) if the conditions are not met.

The alert condition is supported for both HTTP and Browser monitors and can be set from the Conditions tab

![CA check](/docs/images/synthetics/cert-authority.png)


Using a Browser monitor with a User Journey script that visits multiple pages will perform SSL certificate checks for the first page only.

Visiting a http:// instead of a https:// website, or a https:// website that doesn’t provide the full certificate chain will cause the condition to fail and display an error that the full certificate chain wasn’t provided.


## Certificate Change

In modern, dynamic application environments, the SSL certificates are managed by a certificate manager, which can update the certificates automatically. This could sometimes cause issues like missing `hostname` in certificates or if the client time is not correct, certificate validation will fail. 

Sematext Synthetics checks for the certificate change every 10 minutes and notifies you via the monitor's configured [alert notification hooks](/docs/alerts/alert-notifications) about the change. The monitor detects the change based on the fingerprint of the certificate. The change alert contains a detailed change report.

**Certificate Change Alert**
![Certificate change alert](/docs/images/synthetics/cert-change-alert.png)

**Certificate Change Report**
![Certificate change report](/docs/images/synthetics/cert-change-report.png)

## SSL Certificate Report

The SSL certificate report provides an overview of the certificate along with the details of the intermediate and root certificates. It contains the following details:

* Common name of the subject and issuer
* Validity period
* List of domain names for which the certificate can be used
* Hostname where the certificate was retrieved
* Last changed timestamp (if available)
* Certificate chain details

![Certificate report](/docs/images/synthetics/cert-report.png)
