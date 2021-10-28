# Define the number of days on which files older than this date needs to be removed.

$logfile = "c:\TempPath\DeleteFiles.txt"
$CurrentDate = Get-Date
$limit = (Get-Date).AddDays(-62)

# Check if logfile exists, if not, create it.

if (!(test-path -path $logfile)){
    New-Item $logfile
}

# Add current run date to the logfile.

Add-Content $logfile " "
Add-Content $logfile "The cleanup component for Navision drop folders under user accounts ran on $currentdate."
Add-Content $logfile " "

# Delete files older than the $limit.

try {
    Get-ChildItem -Recurse -Force | Where-Object { !$_.PSIsContainer -and $_.CreationTime -lt $limit } | Remove-Item -Force -verbose 4>&1 | Add-Content $logfile
}
catch {
    write-host "Because of an unknown reason, the file or files could not be removed" | Add-Content $logfile
}
