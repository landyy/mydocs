---
category: Security
title: 'Enabling Protection on lsass'

layout: nil
---

### Enabling Protection on lsass

For whatever reason, the folks at Redmond decided that lsass should not be protected even though it is a integral part of the operating system. Regardless, we can enable it with the following Key

```HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa
Key: RunAsPPL```

Options:

* 0 - disabled
* 1 - enabled

When enabled, the lsass process will spawn as a protected process. This will prevent injection of code into the process as well as other restrictions. This prevents process injection as well as stops mimikatz from dumping credentials/hashes. In a domain environment, this is best enabled through a GPO.