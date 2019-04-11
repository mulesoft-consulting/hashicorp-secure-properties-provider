# The HashiCorp hashicorp-secure-properties

The HashiCorp Secure Properties connector allows you to retrieve properties from an HashiCorp Vault instance in a similar way as the mule-secure-configuration-property module

A secure properties file is configured with a `<hashi-corp-vault-properties:config>` tag, for example:

```
    <hashi-corp-vault-properties:config name="HashiCorp_Vault_Properties_Config" 
	doc:name="HashiCorp Vault Properties Config" 
	doc:id="93aee799-006c-48ad-8844-3fbcf438b93c" 
	vaultToken="${vaultToken.runtime.property}"
	vaultURL="https://localhost:8200" 
	vaultStoragePath="secret/gs-vault-config" truststorePassword="${truststorePassword.runtime.property}" truststorePath="vault_truststore.jks">
	</hashi-corp-vault-properties:config>

    <global-property name="prop" value="${vault::property.key1}" />
```

In this example, two values are passed into the Mule runtime at deployment time as a system environment variables `vaultToken.runtime.property` and `truststorePassword.runtime.property`. These properties must be the exact ones used to configure the vault and the truststore (if any for truststore as both the truststorePath and truststorePassword are optional, JVM's is used by default).

**Note**: When using encrypted properties, it is especially important to secure access to the operating system. Anyone who can run a `ps` command or view a Java console will be able to see the decrypted values that are stored in the Mule application's memory.

As this is built as a Mule module, the way to use it within an application is the same as for any other Mule module. Simply search for the HashiCorp module in Exchange from the Mule Palette within Anypoint Studio and import it from there.

```
<?xml version="1.0" encoding="UTF-8"?>

<mule xmlns:core="http://www.mulesoft.org/schema/mule/core" xmlns:tls="http://www.mulesoft.org/schema/mule/tls" xmlns:hashi-corp-vault-properties="http://www.mulesoft.org/schema/mule/hashi-corp-vault-properties"
	xmlns:hashicorp-secure-properties="http://www.mulesoft.org/schema/mule/hashicorp-secure-properties"
	xmlns:hashicorp-properties-loader="http://www.mulesoft.org/schema/mule/hashicorp-properties-loader" xmlns:secure-properties="http://www.mulesoft.org/schema/mule/secure-properties" xmlns:http="http://www.mulesoft.org/schema/mule/http" xmlns="http://www.mulesoft.org/schema/mule/core" xmlns:doc="http://www.mulesoft.org/schema/mule/documentation" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.mulesoft.org/schema/mule/core http://www.mulesoft.org/schema/mule/core/current/mule.xsd http://www.mulesoft.org/schema/mule/core http://www.mulesoft.org/schema/mule/core/current/mule.xsd
http://www.mulesoft.org/schema/mule/http http://www.mulesoft.org/schema/mule/http/current/mule-http.xsd
http://www.mulesoft.org/schema/mule/hashi-corp-vault-properties http://www.mulesoft.org/schema/mule/hashi-corp-vault-properties/current/mule-hashi-corp-vault-properties.xsd">
	<http:listener-config name="HTTP_Listener_config" doc:name="HTTP Listener config" doc:id="bc09acb1-3064-4df9-b1e6-b50bfdb9aa4a" >
		<http:listener-connection host="0.0.0.0" port="8081" >
		</http:listener-connection>
	</http:listener-config>

	<hashi-corp-vault-properties:config name="HashiCorp_Vault_Properties_Config" 
	doc:name="HashiCorp Vault Properties Config" 
	doc:id="93aee799-006c-48ad-8844-3fbcf438b93c" 
	vaultToken="49VLojFvnnv5wnIY3GGW9i6x" 
	vaultURL="https://localhost:8200" 
	vaultStoragePath="secret/gs-vault-config" truststorePassword="changeit" truststorePath="vault_truststore.jks">
	</hashi-corp-vault-properties:config>
	<flow name="security-propertiesFlow" doc:id="970128be-94c9-443c-9f54-f64917d3b3c0" >
		<http:listener doc:name="Listener" doc:id="cbda0d25-7f90-4187-a491-338e79f7f34b" config-ref="HTTP_Listener_config" path="/test"/>
		<set-payload value="Test properties example.password = ${vault::example.password}" doc:name="Set Payload" doc:id="64b5fcfb-11b0-4a62-82c3-92f8379f95fc" />
	</flow>
</mule>
```
