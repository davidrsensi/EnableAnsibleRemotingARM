# Enable windows VM to connect to Ansible from ARM

Add to ARM template under "resources":
```
    {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "[concat(variables('vmName1'),'/CustomScriptExtension')]",
      "apiVersion": "2015-05-01-preview",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName1'))]"
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
          "commandToExecute": "[concat('powershell.exe -file EnableAnsibleRemoting.ps1 ', parameters('adminName'), ' ', parameters('adminPassword'))]"
        }
      }
    }
```
