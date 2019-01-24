# Create Role and Privilige for NSX-T for a vCenter user

This create the right roles for vCenter NSX Service Account.


Below outlines three scenarios.

## No svc_nsx account

```
    PS /Users/aburke/Repositories/nsx-scripts/NSX-T> ./nsxuser_create.ps1
    There is no account vsphere.local\svc_nsx created. Please create one manually and harass VMware for a new cmdlet and APIs!
    To create a local vCenter user:
    
    1. Menu -> Administration
    
    2. Single Sign On -> Users and Groups
    
    3. Domain = vSphere.local
    
    4. Add Users and match svc_nsx
    
    5. Rerun the script
```

## Creation and working

When working it will create the role and permissions and assign it to the root folder for the defined user.

```
PS /Users/aburke/Repositories/nsx-scripts/NSX-T> ./nsxuser_create.ps1
Creating role nsxt_permissions - Assigning to vsphere.local\svc_nsx
```
## Using an Active Directory account

If you're using an AD account you can use the parameter `-domain` to select your domain
```
PS /Users/aburke/Repositories/nsxt/nsx_vc_user> ./nsxuser_create.ps1 -domain corp.local -user svc_nsx
Collecting vSphere credentials

PowerShell credential request
Enter your credentials.
User: administrator@vsphere.local
Password for user administrator@vsphere.local: ********

Connecting to vCenter vc-01a.corp.local
Found existing role named nsxt_permissions. Creating a new role nsxt_permissions-09e4e2 and assigning to corp.local\svc_nsx
```
## Existing group and use it to assign

This will discover if the group exists and if it does it will then append a 6 character GUID to the privilige group name. It will then assign it to the root folder and defined user.

``` 
PS /Users/aburke/Repositories/nsx-scripts/NSX-T> ./nsxuser_create.ps1
Found existing role named nsxt_permissions. Creating a new role nsxt_permissions-8a62ed and assigning to vsphere.local\svc_nsx
```