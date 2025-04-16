# Uninstall Procedure

## 1-Edge unprovisioning
  - From the Edge Cluster, execute the following commands:
    ```bash
      az account set --subscription $TTYF_SUBSCRIPTION_ID
      az iot ops delete --yes --name $TTYF_AIO_CLUSTER_NAME --resource-group $TTYF_RESOURCE_GROUP --include-deps
      az connectedk8s delete --yes --name $TTYF_AIO_CLUSTER_NAME --resource-group $TTYF_RESOURCE_GROUP      
      az logout
      /usr/local/bin/k3s-uninstall.sh
      rm -r ~/.kube
    ```

## 2-Cloud unprovisioning
   - Open a browser and navigate to the [Azure Portal](https://portal.azure.com/)
   - Use the [Azure Cloud Shell (**Bash**)](https://learn.microsoft.com/en-us/azure/cloud-shell/get-started/ephemeral?tabs=azurecli#start-cloud-shell)
   - Execute the following commands in Azure Cloud Shell (Bash):
      ```bash
      az account set --subscription $TTYF_SUBSCRIPTION_ID
      az group delete --resource-group $TTYF_RESOURCE_GROUP --yes
      az keyvault purge --no-wait --name $TTYF_KEYVAULT_NAME --location $TTYF_LOCATION
      az cognitiveservices account purge --name $TTYF_AZURE_OPENAI_NAME --resource-group $TTYF_RESOURCE_GROUP --location "swedencentral"
      az ad app delete --id $TTYF_FACTORY_AGENT_SP_APPID      
      az ad app delete --id $TTYF_AIO_SP_APPID
      ```