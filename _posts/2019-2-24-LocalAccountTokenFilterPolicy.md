---
category: Security
title: 'LocalAccountTokenFilterPolicy'

layout: nil
---

### LocalAccountTokenFilterPolicy

```HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\LocalAccountTokenFilterPolicy```

The LocalAccountTokenFilterPolicy is a registry key related to UAC that if enabled, will strip the administrative SIDs and privileges from the token when they remotely authenticate for the system. Note that this will only happen with LOCAL Admins. Domain Admins are unaffected. There are two values with this key:

* 0 - enabled
* 1 - disabled

This causes problems for both adversaries but also sysadmins. Trying to perform any administrative tasks without RDP is virtually impossible. However, attacks like Pass the Hash are severely mitigated on non-domain joined computers. 