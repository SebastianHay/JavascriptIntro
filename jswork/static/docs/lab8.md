#!/bin/bash
#geoip2
# hays

#mkiptbl.sql3

# the following code unzips and cleans up the ip address information
function get_ipinfo() {
  xz -d -c /home/acc*.xz > my_access_log
  sort -u $HOME/inclass/my_access_log | awk '{print $1}' | uniq -u > geoip1.tmp
}
# this function sends the collected ip addresses from the previous file and gathers location data into a file
function get_geoinfo() {
  ipaddr=$(cat geoip1.tmp)

  for x in $ipaddr
  do
   echo $(curl -s http://freegeoip.net/csv/$x) >> first.pass.tmp
  done
}
# this next command line adjusts punctuation and saves these changes in a new file
function get_sqlinfo() {
  cat first.pass.tmp | tr ',' '|' > last.pass.log

# finally we use sqlite to store the data in a premade table

  sqlite3 ipvisitors.sqlite < mkiptbl.sql3
  echo ".import last.pass.log visitors" | sqlite3 ipvisitors.sqlite

  echo "select ip,latitude,longitude from visitors;"  | sqlite3 ipvisitors.sqlite
}
get_ipinfo
get_geoinfo
get_sqlinfo
