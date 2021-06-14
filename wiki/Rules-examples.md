**Block ads, tracking or malware domains globally**:

https://github.com/evilsocket/opensnitch/wiki/block-lists

**Blocking connections from an executable, allowing only a few domains**:

https://github.com/evilsocket/opensnitch/wiki/block-lists

**Filtering connections by multiple ports:**

`  [x] To this port: ^(53|80|443)$`

targets ports 53 OR 80 OR 443.

`  [x] To this port: ^555[12345]$`

targets ports 5551, 5552, 5553, 5554 OR 5555.

**Filtering connections by an exact domain, and nothing else:**

`  [x] To this host: github.com` (will match only github.com, not www.github.com, etc)

**Filtering connections by a domain and its subdomains:**

`  [x] To this host: .*\.github.com`

**Filtering connections by an executable path:** 

`  [x] From this executable: /usr/bin/python3`
     
(warning: /usr/bin/python3.6/3.7/3.8/etc won't match this rule)

**Allowing or denying Appimages:**

`  [x] From this executable: ^(/tmp/.mount_Archiv[0-9A-Za-z]+/.*)$`

**Allow common system commands:**

  ```
  Name: 000-allow-system-cmds
  Action: Allow
  [x] Priority rule
  [x] From this executable: ^(/usr/sbin/ntpd|/lib/systemd/systemd-timesyncd|/usr/bin/xbrlapi|/usr/bin/dirmngr)$
  [x] To this port: ^(53|123)$
  [x] From this User ID: ^(0|115|118)$
  ```

**Blocking connections made by executables launched from /tmp:**
  ```
  Action:                   Deny
  [x] From this executable: /tmp/.*
  ```

**Filtering an executable path with regexp, for example any python binary in /usr/bin/:**

`  [x] From this executable: ^/usr/bin/python[0-9\.]*$`


**Filtering LAN IPs or multiple ranges:**

`  ^(127\..*|172\..*|192.168\..*|10\..*)$`

See these issues for some discussions and more examples: [#17](https://github.com/gustavo-iniguez-goya/opensnitch/issues/17), [#31](https://github.com/gustavo-iniguez-goya/opensnitch/issues/31), [#73](https://github.com/gustavo-iniguez-goya/opensnitch/issues/73)

**Note:** Don't use "," to specify domains, IPs, etc. It's not supported. For example this won't work (it could be added if you complain loud enough):

> [x] To this host: www.example.org, www.test.me