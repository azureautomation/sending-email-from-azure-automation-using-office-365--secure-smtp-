Sending email from Azure Automation using Office 365 (Secure SMTP)
==================================================================

            
This script  demonstrates how to send an email from Microsoft Azure automation using secure SMTP for sending the mail. In this setup the script is sending mails using Microsoft Office 365. This is could a nice feature to have
 to inform someone that Azure Automation just perform somekind of action and inform them about the result of that action.

You have to define Office 365 Credentials under Azure Automation Assets. You should also change the references within the script to point to the correct Asset name.


Hope you enjoy sending some automated mails from Azure


 


![Image](https://github.com/azureautomation/sending-email-from-azure-automation-using-office-365-(secure-smtp)/raw/master/screen-shot-2014-09-20-at-15.36.11.png)


 


 



PowerShell Workflow
Edit|Remove
powershellworkflow
workflow SendMailUsingOffice365
{
 
     $MyCredential = 'enSence Office 365'
     $Body = 'Content of mail'
     $subject = 'Mail send from Azure Automation using Office 365'
     $userid='psd@ensence.com'
     
    # Get the PowerShell credential and prints its properties
    $Cred = Get-AutomationPSCredential -Name $MyCredential
    if ($Cred -eq $null)
    {
        Write-Output 'Credential entered: $MyCredential does not exist in the automation service. Please create one `n'   
    }
    else
    {
        $CredUsername = $Cred.UserName
        $CredPassword = $Cred.GetNetworkCredential().Password
        
        Write-Output '-------------------------------------------------------------------------'
        Write-Output 'Credential Properties: '
        Write-Output 'Username: $CredUsername'
        Write-Output 'Password: *** `n'
        Write-Output '-------------------------------------------------------------------------'
       # Write-Output 'Password: $CredPassword `n'
    }
        
     
     Send-MailMessage `
    -To 'peter.dahl@proactive.dk' `
    -Subject $subject  `
    -Body $Body `
    -UseSsl `
    -Port 587 `
    -SmtpServer 'smtp.office365.com' `
    -From $userid `
    -BodyAsHtml `
    -Credential $Cred
  
        Write-Output 'Mail is now send `n'
        Write-Output '-------------------------------------------------------------------------'
  
}



workflow SendMailUsingOffice365 
{ 
  
     $MyCredential = 'enSence Office 365' 
     $Body = 'Content of mail' 
     $subject = 'Mail send from Azure Automation using Office 365' 
     $userid='psd@ensence.com' 
      
    # Get the PowerShell credential and prints its properties 
    $Cred = Get-AutomationPSCredential -Name $MyCredential 
    if ($Cred -eq $null) 
    { 
        Write-Output 'Credential entered: $MyCredential does not exist in the automation service. Please create one `n'    
    } 
    else 
    { 
        $CredUsername = $Cred.UserName 
        $CredPassword = $Cred.GetNetworkCredential().Password 
         
        Write-Output '-------------------------------------------------------------------------' 
        Write-Output 'Credential Properties: ' 
        Write-Output 'Username: $CredUsername' 
        Write-Output 'Password: *** `n' 
        Write-Output '-------------------------------------------------------------------------' 
       # Write-Output 'Password: $CredPassword `n' 
    } 
         
      
   




        
    
TechNet gallery is retiring! This script was migrated from TechNet script center to GitHub by Microsoft Azure Automation product group. All the Script Center fields like Rating, RatingCount and DownloadCount have been carried over to Github as-is for the migrated scripts only. Note : The Script Center fields will not be applicable for the new repositories created in Github & hence those fields will not show up for new Github repositories.
