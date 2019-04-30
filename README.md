# EnableRemotingARM

Add to ARM template:


```
        {
          "type": "Microsoft.Compute/virtualMachines/extensions",
          "name": "[concat(parameters('vmName'),'AnsibleSetup')]",
          "apiVersion": "2015-05-01-preview",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[concat('Microsoft.Compute/virtualMachines/', parameters('vmName'))]"
          ],
          "properties": {
            "publisher": "Microsoft.Azure.Extensions",
            "type": "CustomScript",
            "typeHandlerVersion": "2.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "fileUris": [
                "https://raw.githubusercontent.com/davidrsensi/EnableAnsibleRemotingARM/master/EnableAnsibleRemoting.ps1"
              ],
              "commandToExecute": "powershell.exe -file EnableAnsibleRemoting.ps1 [parameters('adminName')] [parameters('adminPassword')]"
            }
          }
        }
```
