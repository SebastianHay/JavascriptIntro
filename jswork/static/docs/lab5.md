#!/bin/bash
# ts_input
# hays

echo "$TD"
dialog --msgbox "Enter project code and a brief description" 10 50
dialog --inputbox "Enter a project code and a brief description" 8 60 2> /tmp/inputbox.tmp.$$

retval=$?

INPVAR=$(cat /tmp/inputbox.tmp.$$)

echo -n "$TD" "| ">> "$HOME/log/timesheet.log"
echo "$INPVAR" >> "$HOME/log/timesheet.log"
rm /tmp/inputbox.tmp.$$
echo "Done."
./ts_mkweb
#eof

