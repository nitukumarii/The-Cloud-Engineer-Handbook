### Follow-up: How did you automate the certificate monitoring process?

To reduce manual effort, we automated the certificate expiry monitoring process using a Python script.

The script was scheduled to run daily through a cron job. It connected to our list of application endpoints, retrieved the SSL certificate information, and extracted the certificate expiry date.

The script then calculated the number of days remaining before expiration. Based on predefined thresholds—for example, 60 days, 30 days, and 15 days—it generated a report of certificates approaching expiry.

The report was automatically shared with the operations team, allowing us to initiate the renewal process well before the certificates expired. After the certificate was renewed, we validated the new certificate by checking the updated expiry date and verifying that the application was accessible over HTTPS.

This automation eliminated the need for engineers to manually check hundreds of certificates every week, reduced the risk of missing certificate renewals, and helped us proactively manage certificate lifecycles.
