---
external help file: ExchangeOnlineManagement-help.xml
Module Name: ExchangeOnlineManagement
online version: https://docs.microsoft.com/powershell/module/exchange/connect-ippssession
applicable: Exchange Online
title: Connect-IPPSSession
schema: 2.0.0
author: chrisda
ms.author: chrisda
ms.reviewer: navgupta
---

# Connect-IPPSSession

## SYNOPSIS
This cmdlet is available only in the Exchange Online PowerShell V2 module. For more information, see [Connect to Exchange Online PowerShell](https://docs.microsoft.com/powershell/exchange/connect-to-exchange-online-powershell).

Use the Connect-IPPSSession cmdlet in the Exchange Online PowerShell V2 module to connect to Security & Compliance Center PowerShell or standalone Exchange Online Protection PowerShell.

**Note**: If your organization is on-premises Exchange, and you have Exchange Enterprise CAL with Services licenses for Exchange Online Protection (EOP), use the [Connect-ExchangeOnline](https://docs.microsoft.com/powershell/module/exchange/connect-exchangeonline) cmdlet the Exchange Online PowerShell instructions to connect to your EOP PowerShell environment.

For information about the parameter sets in the Syntax section below, see [Exchange cmdlet syntax](https://docs.microsoft.com/powershell/exchange/exchange-cmdlet-syntax).

## SYNTAX

```
Connect-IPPSSession
 [[-ConnectionUri] <String>]
 [[-AzureADAuthorizationEndpointUri] <String>]
 [[-DelegatedOrganization] <String>]
 [[-PSSessionOption] <PSSessionOption>]
 [[-Prefix] <String>]
 [[-CommandName] <String[]>]
 [[-FormatTypeName] <String[]>]
 [-BypassMailboxAnchoring]
 [-Credential <PSCredential>]
 [-UserPrincipalName <String>]
 [<CommonParameters>]
```

## DESCRIPTION
This cmdlet allows you to create a remote PowerShell session to Exchange-related PowerShell environments other than Exchange Online PowerShell. For example, Security & Compliance Center PowerShell or standalone Exchange Online Protection PowerShell (for organizations without Exchange Online mailboxes).

For details about the current and past public versions of the EXO V2 module, see [Release notes](https://docs.microsoft.com/powershell/exchange/exchange-online-powershell-v2#release-notes). This topic is written for the current public version. Features or parameters that are only available in a Preview version of the module are specifically noted.

## EXAMPLES

### Example 1
```powershell
$UserCredential = Get-Credential
Connect-IPPSSession -Credential $UserCredential
```

This example connects to Security & Compliance Center PowerShell in a Microsoft 365 organization.

The first command gets the user credentials and stores them in the $UserCredential variable.

The second command connects the current PowerShell session using the credentials in the $UserCredential, which isn't MFA enabled. Note that after the second command is complete, the password key in the $UserCredential variable becomes empty.

After the Connect-IPPSSession command is successful, you can run Security & Compliance Center cmdlets.

### Example 2
```powershell
Connect-IPPSSession -Credential (Get-Credential) -ConnectionUri https://ps.protection.outlook.com/powershell-liveid/
```

This example connects to standalone Exchange Online Protection PowerShell in an organization that doesn't have Exchange Online mailboxes.

## PARAMETERS

### -ConnectionUri
The ConnectionUri parameter specifies the connection endpoint for the remote PowerShell session.

- For Security & Compliance Center PowerShell in Microsoft 365 or Microsoft 365 GCC, don't use this parameter.
- For Security & Compliance Center PowerShell in Office 365 Germany, use the value <https://ps.compliance.protection.outlook.de/PowerShell-LiveID> for this parameter.
- For Exchange Online Protection PowerShell in standalone EOP organizations without Exchange Online mailboxes, use the value <https://ps.protection.outlook.com/powershell-liveid/> for this parameter.

```yaml
Type: String
Parameter Sets: (All)
Aliases:
Applicable: Exchange Online

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -AzureADAuthorizationEndpointUri
The AzureADAuthorizationEndpointUri parameter specifies the Azure AD Authorization endpoint Uri that can issue OAuth2 access tokens. You use this parameter with multi-factor authentication (MFA) and federated authentication.

- For Security & Compliance Center PowerShell in Microsoft 365 or Microsoft 365 GCC, don't use this parameter.
- For Security & Compliance Center PowerShell in Office 365 Germany, use the value <https://login.microsoftonline.de/common> for this parameter.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -DelegatedOrganization
The DelegatedOrganization parameter specifies the customer organization that you want to manage (for example, contosoelectronics.onmicrosoft.com). This parameter only works if the customer organization has agreed to your delegated management via the CSP program.

After you successfully authenticate, the cmdlets in this session are mapped to the customer organization, and all operations in this session are done on the customer organization.

```yaml
Type: String
Parameter Sets: (All)
Aliases:
Applicable: Exchange Online

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -PSSessionOption
The PSSessionOption parameter specifies the PowerShell session options to use in your connection to Exchange Online. You store the output of the [New-PSSessionOption](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/new-pssessionoption) command in a variable, for example:

`$Options = New-PSSessionOption <Settings>`

And you use the variable name as the value for this parameter (for example, `$Options`).

```yaml
Type: PSSessionOption
Parameter Sets: (All)
Aliases:
Applicable: Exchange Online

Required: False
Position: 3
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Prefix
The Prefix parameter specifies an alias to add to nouns in the names of older remote PowerShell cmdlets (cmdlet with nouns that don't already start with EXO). A valid value is a text string without spaces, and you can't use the value EXO (this prefix is reserved for PowerShell V2 module cmdlets).

```yaml
Type: String
Parameter Sets: (All)
Aliases:
Applicable: Exchange Online

Required: False
Position: 4
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -CommandName
The CommandName parameter specifies the comma separated list of commands to import into the session. Use this parameter for applications or scripts that use a specific set of cmdlets. Reducing the number of cmdlets in the session helps improve performance and reduces the memory footprint of the application or script.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:
Applicable: Exchange Online

Required: False
Position: 5
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -FormatTypeName
The FormatTypeName parameter specifies the output format of the cmdlet.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:
Applicable: Exchange Online

Required: False
Position: 6
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -BypassMailboxAnchoring
The BypassMailboxAnchoring switch bypasses the use of the mailbox anchoring hint. You don't need to specify a value with this switch.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:
Applicable: Exchange Online

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Credential
The Credential parameter specifies the username and password that's used to run this command. Typically, you use this parameter in scripts or when you need to provide different credentials that have the required permissions.

A value for this parameter requires the Get-Credential cmdlet. To pause this command and receive a prompt for credentials, use the value `(Get-Credential)`. Or, before you run this command, store the credentials in a variable (for example, `$cred = Get-Credential`) and then use the variable name (`$cred`) for this parameter. For more information, see [Get-Credential](https://docs.microsoft.com/powershell/module/microsoft.powershell.security/get-credential).

```yaml
Type: PSCredential
Parameter Sets: (All)
Aliases:
Applicable: Exchange Online

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -UserPrincipalName
The UserPrincipalName parameter specifies the account that you want to use to connect (for example, navin@contoso.onmicrosoft.com). Using this parameter allows you to skip the first screen in authentication prompt.

```yaml
Type: String
Parameter Sets: (All)
Aliases:
Applicable: Exchange Online

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/p/?LinkID=113216).

## INPUTS

###  

## OUTPUTS

###  

## NOTES

## RELATED LINKS
