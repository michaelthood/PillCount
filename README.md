# PillCount
<#Physician Assistan/nurse counts the patients controlled substances.
Purpose of program is to make sure the patients pill count is correct.
Next step and not yet programmed is to add dates for the next 3
prescriptions (dates that they can be filled).
Another nicety would be different statements if the patient has more 
meds that supposed to instead of negative numbers. I will do this next. 
 
To implement code, in the search bar, type ISE and click on 
Run as administrator.
This will bring up Powershell.  
At the prompt type <Set-ExecutionPolicy remotesigned>
Click yes to all.  
 In the View, click on script pane and Copy and paste
 code into Powershell script pane. Hit the green arrow to run the code.
At the prompt in the blue command module at  c:\useres\Your Name\ 
type 
./pc.ps1 
The return key will run the program.
In the date to be entered, use mm/dd/yyyy format.
 Below is the code. #>

@'
$ToDate = Get-Date
$PillNum = Read-Host -Prompt 'Input counted pills '

$NxtDate = (Get-Date).ADDDAYS(90)

$DateFilled = Read-Host -Prompt 'Input date on bottle that the Rx was filled '
$PillsTakenDaily = Read-Host -Prompt 'Input Number of pills taken daily '

$TodaysDate = [system.datetime]$ToDate
$DateFilledOnBottle = [system.datetime]$DateFilled


$DateToLastUntill = $DateFilledOnBottle.AddDays(30)


$SupposedToHaveDaysofpillsLeft =  $DateToLastUntill.DayOfYear - $TodaysDate.DayOfYear
write-host "Supposed to have " $SupposedToHaveDaysofpillsLeft " days of pills left to last untill " $DateToLastUntill ".  "


$ActuallyHasDaysofpillsLeft = $PillNum /$PillsTakenDaily
write-host "Actually has " $PillNum " pills left for "  $ActuallyHasDaysofpillsLeft " more days. "
write-host "Supposed to have " ($SupposedToHaveDaysofpillsLeft * $PillsTakenDaily) " pills left to last "  $SupposedToHaveDaysofpillsLeft " more days.  "

$PillDescrepancy = ($SupposedToHaveDaysofpillsLeft * $PillsTakenDaily) - $PillNum
write-host "Deficit in pills = "  $PillDescrepancy ". "
'@ > pc.ps1
