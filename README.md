# InfluxDB
How to work with InfluxDB

## InfluxDB Server
The InfluxDB Server (V 1.8.10) runs on HomeAssistant at ``http://192.168.178.63:8086/``.

## Install InfluxDB for Windows
Binaries downloaded from https://portal.influxdata.com/downloads/ as admin.
That includes Server and Client while I'm just using the Client to connect to the Server from HomeAssistant.

## Start InfluxDB Client
```
PS C:\Program Files\InfluxData\influxdb\influxdb-1.8.10-1> .\influx.exe -host 192.168.178.63 -username influx_user_1 -password ********

Connected to http://192.168.178.63:8086 version 1.8.10
InfluxDB shell version: 1.8.10

> show databases
name: databases
name
----
influx_db_1
influx_db_2
```

## SELECT command
Example:
```
> select value from kWh where entity_id='walli_energy_total' and time >= now() - 7d

name: kWh
time                value
----                -----
1682707200291570000 1313.133
1682707800333715000 1314.896
1682708400322344000 1316.664
1682709000303324000 1318.434
```
- get just the `value` data
- from the `kWh` measurement
- where the `entity_id` equals `walli_energy_total`
- from the last 10 days

## HELP command
```
> help
Usage:
        connect <host:port>   connects to another node specified by host:port
        auth                  prompts for username and password
        pretty                toggles pretty print for the json format
        chunked               turns on chunked responses from server
        chunk size <size>     sets the size of the chunked responses.  Set to 0 to reset to the default chunked size
        use <db_name>         sets current database
        format <format>       specifies the format of the server responses: json, csv, or column
        precision <format>    specifies the format of the timestamp: rfc3339, h, m, s, ms, u or ns
        consistency <level>   sets write consistency level: any, one, quorum, or all
        history               displays command history
        settings              outputs the current settings for the shell
        clear                 clears settings such as database or retention policy.  run 'clear' for help
        exit/quit/ctrl+d      quits the influx shell

        show databases        show database names
        show series           show series information
        show measurements     show measurement information
        show tag keys         show tag key information
        show field keys       show field key information

        A full list of influxql commands can be found at:
        https://docs.influxdata.com/influxdb/latest/query_language/spec/
```