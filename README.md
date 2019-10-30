# number_of_days_vm_was_pathched_last
script to see when was redhat vm was last patched

## current date in numeric 

date +%s

## get all installed patches with date and name in human redable form
rpm -qa --queryformat '%{installtime} %{installtime:date} %{name}\n'

## get all installed patches with date and name in human redable form, sort it using installtime and return top record

rpm -qa --queryformat '%{installtime} %{installtime:date} %{name}\n' | sort | tail -n 1

## get all installed patches installtime only, sort it using installtime and return top record

rpm -qa --queryformat '%{installtime}\n' | sort | tail -n 1

## putting it all together and substracting dates
current_date=$(date +%s)

last_path_installed_date=$(rpm -qa --queryformat '%{installtime}\n' | sort | tail -n 1)

let last_patched=($current_date - $last_path_installed_date)/86400

echo $last_patched
