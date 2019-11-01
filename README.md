# RaidenFTPD
RaidenFTPD Logging Content Pack for Graylog

### Includes

* Input (RaidenFTPD-gelf - GELF/UDP/5443)
* Extractors (RaidenFTPD GROK && Convert File Size && Convert Speed && all action descriptions)
* Dashboard (RaidenFTPD)

### Requirements

* RaidenFTPD with license and configured to log in separate utf-8 log.
* A GELF capable log exporter/collector such as nxlog or Graylog Collector monitoring the log file path

#### Example of a working NXlog.conf file input/output configuration (using Collector Sidecar):
```
<Input in_raidenftpd>
    Module im_file
    File "C:\RaidenServer\RaidenFTPD\Log\utf8-pippin-*.log"
    PollInterval 1
    SavePos True
    ReadFromLast True
    Recursive False
    RenameCheck True
    Exec $FileName = file_name(); # Send file name with each message
</Input>

<Output out_raidenftpd>
    Module om_udp
    Host 10.0.0.14
    Port 5443
    OutputType  GELF
    Exec $short_message = $raw_event; # Avoids truncation of the short_message field.
    Exec $Hostname = hostname_fqdn();
</Output>
```

## Screenshots
![Dashboard](https://cloud.githubusercontent.com/assets/813996/17567464/c811b5bc-5f3f-11e6-8b15-7295f109bc44.jpg)
