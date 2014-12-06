#!/bin/bash 
# script1
# lab 4 script1
# hays

# today
SDATE=$(date +%s)
# Date of Birth
EDATE=$(date -d '07/01/1995' +%s)
# seconds alive
SALIVE=$(($SDATE - $EDATE))
# days alive
DALIVE=$(($SALIVE / 86400))
TENDAYS=$(($SALIVE + 864000000))
TDATE=$(date -d '@'$TENDAYS'' +%m/%d/%Y)

echo "You have been alive "$SALIVE" seconds."
echo "You have been alive "$DALIVE" days."
echo "Ten Thousand Days for you is: "$TDATE"."

echo -n "Please enter your first name: "
read fname
echo -n "Please enter your first number: "
read numb1
echo -n "Please enter your second number: "
read numb2
SUM1=$((numb1+numb2))

echo "Hi $fname, the sum of your numbers is: $SUM1."
echo $(date +%s) $fname $SUM1 >> script1.log
