<properties 
	pageTitle="Provision Redis Cache" 
	description="Use Azure Resource Manager template to deploy an Azure Redis Cache." 
	services="redis-cache" 
	documentationCenter="" 
	authors="tfitzmac" 
	manager="wpickett" 
	editor=""/>

<tags 
	ms.service="cache" 
	ms.workload="web" 
	ms.tgt_pltfrm="cache-redis" 
	ms.devlang="na" 
	ms.topic="article" 
	ms.date="06/01/2015" 
	ms.author="tomfitz"/>

# Provision Redis Cache

In this topic, you will learn how to create an Azure Resource Manager template that deploys an Azure Redis Cache. You will learn how to define which resources are deployed and 
how to define parameters that are specified when the deployment is executed. You can use this template for your own deployments, or customize it to meet your requirements.

For more information about creating templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).

For the complete template, see [Redis Cache template](https://github.com/tfitzmac/AppServiceTemplates/blob/master/RedisCache.json).

## What you will deploy

In this template, you will deploy an Azure Redis Cache.

## Parameters to specify

With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed. The template includes a section called Parameters that contains all of the parameter values.
You should define a parameter for those values that will vary based on the project you are deploying or based on the 
environment you are deploying to. Do not define parameters for values that will always stay the same. Each parameter value is used in the template to define the resources that are deploy. 

We will describe each parameter in the template.

[AZURE.INCLUDE [app-service-web-deploy-redis-parameters](../includes/cache-deploy-parameters.md)]

### redisCacheLocation

The location of the Redics Cache. For best perfomance, use the same location as the app to be used with the cache.

    "redisCacheLocation": {
      "type": "string"
    }

    
## Resources to deploy

### Redis Cache

Creates the Azure Redis Cache.

    {
      "apiVersion": "2014-04-01-preview",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        sku": {
          "name": "[parameters('redisCacheSKU')]",
          "family": "[parameters('redisCacheFamily')]",
          "capacity": "[parameters('redisCacheCapacity')]"
        },
        "redisVersion": "[parameters('redisCacheVersion')]",
        "enableNonSslPort": true
      }
    }
     



## Commands to run deployment

[AZURE.INCLUDE [app-service-deploy-commands](../includes/app-service-deploy-commands.md)] 

### PowerShell

    New-AzureResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/tfitzmac/AppServiceTemplates/master/RedisCache.json

### Azure CLI

    azure group deployment create --template-uri https://raw.githubusercontent.com/tfitzmac/AppServiceTemplates/master/RedisCache.json


