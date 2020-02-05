
# Zugriffszahlenanalyse Open Data Portal

Apache/Nginx Logdateien kann man gut mit GoAccess analysieren.

GoAccess Dokumentation: \
https://goaccess.io/get-started


# Shell Befehle zur Analyse
## Logs kombinieren
```bash 
# Direkt mit zcat verketten und analysieren
zcat access_log-ssl.?.gz | goaccess --config-file=goaccess.conf access_log-ssl -

# Files manuell verketten
cat access_log* >> log.txt
```
## Auswertung

```bash 
# Analysetool starten
goaccess --config-file=goaccess.conf log.txt

# Auswertung für alle Dateien auswerten
cat access-logs-2019-11/logs201911.txt access-logs-2019-12/logs201912.txt | goaccess --config-file=goaccess.conf access-logs-2020-01/logs202001.txt
```


## Manuelle Auswertung
```bash 
# Test
zcat access_log-ssl.1.gz |awk '{ print $11 }'|grep dataset |grep -v taxonomy | grep -oP '.*\/\/[^\/]+\/[^\/]+\/[^\/"]+'

# Meistbesuchte Datensätze
cat access-logs-2019-11/logs201911.txt access-logs-2019-12/logs201912.txt access-logs-2020-01/logs202001.txt | awk '{ print $11 }'|grep dataset | grep -oP '.*\/\/[^\/]+\/[^\/]+\/[^\/"]+'|  sort | uniq -c|  sort -nr
```
