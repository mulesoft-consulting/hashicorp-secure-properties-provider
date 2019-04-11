# hashicorp-secure-properties-provider
This module allows to read properties from the hashicorp vault as opposed to properties file

## Secure properties with Mule Vault

This asset shows with a basic application how encrypted properties can be used within it.

1. Read the documentation [page][1] for general understanding and in particular follow the instructions [here][2] on how to add secure configuration to your application, after this asset is downloaded into studio.
2. Read [here][3] on how to safely hide properties on CloudHub
3. Add the vault key and any environment specific variables in Studio, Run Configuration -> Argument and in there one can specify the typical ones are mule\_env= and secret\_key= (those are used in this example too)
4. One should be able to run the application and execute an HTTP request as below
5. To encrypt/decrypt the credentials in the dev.properties file Help -> Install New Software -> Work with -> [http://security-update-site-1.4.s3.amazonaws.com](http://security-update-site-1.4.s3.amazonaws.com) and press add. Select all the packages and install them.
6. After restarting Studio, right click on the dev.properties file and Open with Mule Properties Editor

Example URL: GET [http://localhost:8081/test](http://localhost:8081/test)

See screenshots below:

![fe738b82-7936-4528-add9-77520af63dd1-vault1.png](https://exchange2-file-upload-service-kprod.s3.us-east-1.amazonaws.com:443/fe738b82-7936-4528-add9-77520af63dd1-vault1.png)

![9082568a-4376-4079-9061-ff5e9d28b0b3-vault2.png](https://exchange2-file-upload-service-kprod.s3.us-east-1.amazonaws.com:443/9082568a-4376-4079-9061-ff5e9d28b0b3-vault2.png)

![c952f80a-d008-4bf7-8c20-649d177bcd65-vault3.png](https://exchange2-file-upload-service-kprod.s3.us-east-1.amazonaws.com:443/c952f80a-d008-4bf7-8c20-649d177bcd65-vault3.png)

  [1]: https://docs.mulesoft.com/mule-runtime/4.1/secure-configuration-properties
  [2]: https://docs.mulesoft.com/mule-runtime/4.1/secure-configuration-properties#adding-secure-configuration-properties-to-your-app
  [3]: https://docs.mulesoft.com/runtime-manager/secure-application-properties
  [4]: https://docs.mulesoft.com/mule-runtime/3.6/installing-anypoint-enterprise-security
