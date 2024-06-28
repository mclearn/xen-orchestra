> This file contains all changes that have not been released yet.
>
> Keep in mind the changelog is addressed to **users** and should be
> understandable by them.

### Enhancements

> Users must be able to say: “Nice enhancement, I'm eager to test it”

- [Netbox] Check Netbox version before attempting to synchronize (PR [#7735](https://github.com/vatesfr/xen-orchestra/pull/7735))
- [Netbox] Support Netbox 4 (Thanks [@ChrisMcNichol](https://github.com/ChrisMcNichol)!) (PR [#7735](https://github.com/vatesfr/xen-orchestra/pull/7735))
- [Migration] Disable CBT when needed during a disk/VM migration (PR [#7756](https://github.com/vatesfr/xen-orchestra/pull/7756))
- [Disks] Show and edit the use of CBT (Change Block Tracking) in disks (PR [#7732](https://github.com/vatesfr/xen-orchestra/pull/7732))
- [Create/SR] Display SCSI ID and LUN during HBA storage creation (PR [#7742](https://github.com/vatesfr/xen-orchestra/pull/7742))
- [Backups] Implements Change Block Tracking (CBT) (PR [#7750](https://github.com/vatesfr/xen-orchestra/pull/7750))
- [REST API] _Rolling Pool Reboot_ action available `pools/<uuid>/actions/rolling_reboot` (PR [#7761](https://github.com/vatesfr/xen-orchestra/pull/7761))
- [XOSTOR] Possibility to directly access an XOSTOR SR from the view that lists all XOSTOR SRs (PR [#7764](https://github.com/vatesfr/xen-orchestra/pull/7764))
- [VM/Advanced] Display an accurate secure boot status and allow user to propagate certificates from pool to VM [#7495](https://github.com/vatesfr/xen-orchestra/issues/7495) (PR [#7751](https://github.com/vatesfr/xen-orchestra/pull/7751))

### Bug fixes

> Users must be able to say: “I had this issue, happy to know it's fixed”

### Packages to release

> When modifying a package, add it here with its release type.
>
> The format is the following: `- $packageName $releaseType`
>
> Where `$releaseType` is
>
> - patch: if the change is a bug fix or a simple code improvement
> - minor: if the change is a new feature
> - major: if the change breaks compatibility
>
> Keep this list alphabetically ordered to avoid merge conflicts

<!--packages-start-->

<!--packages-end-->
