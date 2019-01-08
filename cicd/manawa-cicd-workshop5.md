# 

Vault is a secret management tool to store your secrets (ex: password, SSH key, etc ...). In order to authenticate to Vault, we use AppRole authentication. It is an authentication mechanism within Vault to allow machines or apps to acquire a token to interact with Vault. It uses Role ID and Secret ID for login. 

The basic workflow is:

![Homepage Jfrog]({% image_path screens/vault-approle-workflow.png %})


All these project's secrets are stored in Vault. In order to retrieve them, you will have to do the following:

Request Role ID & Secret ID 
Set the following environment variables in your Gitlab CI variables (Settings/ CICD / variables):

```
KEY: VAULT_PAYLOAD
```

```
VALUE: {"role_id": "my-role-id", "secret_id": "my-secret-id"}
```

To retrieve the role-id and secret-id there is a procedure accessible at the following link: [https://jira.adeo.com/confluence/pages/viewpage.action?pageId=121719862](https://jira.adeo.com/confluence/pages/viewpage.action?pageId=121719862)
