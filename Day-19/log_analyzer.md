```bash
#!/bin/bash

error_count() {
        
        res=$(awk '{print $3}' "$1" | sort | uniq -c)
	errorCount=$(echo "$res" | grep "ERROR")
	echo $errorCount
}

critical_errors() {
        
	res=$(awk '{print $3}' "$1" | sort | uniq -c)
        criticalCounts=$(echo "$res" | grep "CRITICAL")
	echo $criticalCounts

	resErrors=$(grep -n "CRITICAL" "$1")
	echo "$resErrors"
}

top_error() {

	res=$(awk '{print $4, $5, $6, $7}' "$1" | sort -k3 | uniq -c | sort -nr | head -n 5)
	echo "$res"
}
creating_report() {

        report="log_report_$(date +'%F_%T').txt"
	touch $report
	echo "Date of Analysis: $(date +'%F_%T')" >> $report
	echo "====================================================================================================="
        echo "Log file name: $1" >> $report
	echo "====================================================================================================="
	echo "Total lines processed: $(wc -l $1 | awk '{print $1}')" >> $report
	echo "====================================================================================================="
	echo "Total error count: $(awk '{print $3}' $1 | sort | uniq -c | grep "ERROR" | awk '{print $1}')" >> $report
	echo "====================================================================================================="
	echo "Top error messages: $(awk '{print $4,$5,$6,$7}' $1 | sort -k3 | uniq -c | sort -nr | head -n 5)" >> $report
	echo "====================================================================================================="
	echo "Critical events: $(grep -n "CRITICAL" "$1")" >> $report

	
}

path=$1
file_name=$2
if [ -z "$path" ]
then echo "Error: Path of file not defined"
elif [ -z "$file_name" ]
then echo "Error: Name of file not defined"
else 
	res=$(find $path -name $file_name)
	if [ -z $res ]
	then
		echo "Failed"
	else
		echo "Success"

		error_count "$path/$file_name"
		critical_errors "$path/$file_name"
		top_error "$path/$file_name"
		creating_report "$path/$file_name"
	fi
fi





bash
