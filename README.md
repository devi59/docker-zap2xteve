# [xTeVe](https://xteve.de/) + [zap2xml](http://zap2xml.awardspace.info/) Docker Container

### Docker usage
```
docker create \
  --name=zap2xteve \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Europe/London \
  -e ZAP2XML_USERNAME= \
  -e ZAP2XML_PASSWORD= \
  -p 34400:34400 \
  -v <path to config>:/config \
  -v <path to data>:/data \
  -v <path to cache>:/cache \
  --restart unless-stopped \
  devi59/docker-zap2xteve
```

## Parameters
| Parameter | Function |
| :----: | --- |
| `-p 34400` | The exposed port for the xTeVe webinterface |
| `-e XTEVE_PORT=34400` | The port for the xTeVe webinterface |
| `-e PUID=1000` | for UserID - see below for explanation |
| `-e PGID=1000` | for GroupID - see below for explanation |
| `-e TZ=Europe/London` | Specify a timezone to use ex/Europe/London |
| `-e TVGUIDE_EPG=FALSE` | Specify whether to use TVGuide instead of Zap2it |
| `-e ZAP2XML_USERNAME=` | Specify username for either Zap2it or TVGuide |
| `-e ZAP2XML_PASSWORD=` | Specify password for either Zap2it or TVGuide |
| `-e ZAP2XML_ARGS= -D -I -F -L -T -O -b` | Specify additional arguments for zap2xml |
| `-e XMLTV_FILENAME=xmltv.xml` | Specify filename for zap2xml EPG-XML file |
| `-e XML_UPDATE_INTERVAL=24` | Specify update interval for zap2xml (in hours). |
| `-v /config` | Location of xTeVe config files |
| `-v /data` | Location of zap2xml EPG-XML file |
| `-v /cache` | Location of zap2xml cache |

### OPTIONAL ARGUMENTS
```

  -u <username>
  -p <password>
  -d <# of days> (default = $days)
  -n <# of no-cache days> (from end)   (default = $ncdays)
  -N <# of no-cache days> (from start) (default = $ncsdays)
  -B <no-cache day>
  -s <start day offset> (default = $start)
  -o <output xml filename> (default = "$outFile")
  -c <cacheDirectory> (default = "$cacheDir")
  -l <lang> (default = "$lang")
  -i <iconDirectory> (default = don't download channel icons)
  -m <#> = offset program times by # minutes (better to use TZ env var)
  -b = retain website channel order
  -x = output XTVD xml file format (default = XMLTV)
  -w = wait on exit (require keypress before exiting)
  -q = quiet (no status output)
  -r <# of connection retries before failure> (default = $retries, max 20)
  -e = hex encode entities (html special characters like accents)
  -E "amp apos quot lt gt" = selectively encode standard XML entities
  -F = output channel names first (rather than "number name")
  -O = use old tv_grab_na style channel ids (C###nnnn.zap2it.com)
  -A "new live" = append " *" to program titles that are "new" and/or "live"
  -M = copy movie_year to empty movie sub-title tags
  -U = UTF-8 encoding (default = "ISO-8859-1")
  -L = output "<live />" tag (not part of xmltv.dtd)
  -T = don't cache files containing programs with "$sTBA" titles 
  -P <http://proxyhost:port> = to use an http proxy
  -C <configuration file> (default = "$confFile")
  -S <#seconds> = sleep between requests to prevent flooding of server 
  -D = include details = 1 extra http request per program!
  -I = include icons (image URLs) - 1 extra http request per program!
  -J <xmltv> = include xmltv file in output
  -Y <lineupId> (if not using username/password)
  -Z <zipcode> (if not using username/password)
  -z = use tvguide.com instead of zap2it.com
  -a = output all channels (not just favorites) 
  -j = add "series" category to all non-movie programs

## Using Multiple zap2xml users/guides
```
Add as many zap2xml user details as wanted (users must be sequentially numbered). 
(OPTIONAL): Add separate zap2xml arguments for each user by following the numbering scheme.  Will use default (ZAP2XML_ARGS) if no numbered (ZAP2XML_ARGS_#) is provided.
For example:
```
| Parameter | Function |
| :----: | --- |
| `-e ZAP2XML_USERNAME_1=` | Specify username 1 for either Zap2it or TVGuide |
| `-e ZAP2XML_PASSWORD_1=` | Specify password 1 for either Zap2it or TVGuide |
| `-e ZAP2XML_ARGS_1= -D` | (OPTIONAL) Specify additional arguments for zap2xml |
| `-e ZAP2XML_USERNAME_2=` | Specify username 2 for either Zap2it or TVGuide |
| `-e ZAP2XML_PASSWORD_2=` | Specify password 2 for either Zap2it or TVGuide |
| `-e ZAP2XML_ARGS_2= -z` | (OPTIONAL) Specify additional arguments for zap2xml |
| `-e ZAP2XML_USERNAME_3=` | Specify username 3 for either Zap2it or TVGuide |
| `-e ZAP2XML_PASSWORD_3=` | Specify password 3 for either Zap2it or TVGuide |
| `-e ZAP2XML_ARGS_3= -D -I -F -L` | (OPTIONAL) Specify additional arguments for zap2xml |

### NOTES
'''

Notes: This repo is derived from the work of [shuaiscott] (https://github.com/shuaiscott/zap2xml) and [crlorentzen] (https://github.com/crlorentzen/docker-zap2xml) and [sjsaleem] (https://github.com/sjsaleem/zap2xml)
