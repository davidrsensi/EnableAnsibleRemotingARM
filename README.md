# Enable windows VM to connect to Ansible from ARM

Add to ARM template under "resources":
```
    {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "[concat(variables('vmName'),'/CustomScriptExtension')]",
      "apiVersion": "2015-05-01-preview",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
      ],
      "properties": {
        "publisher": "Microsoft.Compute",
        "type": "CustomScriptExtension",
        "typeHandlerVersion": "1.7",
        "autoUpgradeMinorVersion": true,
        "settings": {
          "fileUris": [
            "https://raw.githubusercontent.com/davidrsensi/EnableAnsibleRemotingARM/master/EnableAnsibleRemoting.ps1"
          ],
          "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -file EnableAnsibleRemoting.ps1"
        }
      }
    }
```
