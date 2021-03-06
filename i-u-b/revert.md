### 3.3.3 Reverting to an Older Version

ERPNext is not really designed to be reverted or back-ported. However, with some planning it can be done. The main trick is to have good backups. Refer to [3.4 Backing up ERPNext](backup.md "Backing up ERPNext"). This is the primary reason why we backup all sites before we do an [upgrade](upgrade.md "Upgrading ERPNext"). With planning and a good backup, you can restore the database to match the known good code base.

Assuming the steps to take a **full backup** were completed from [3.4 Backing up ERPNext](backup.md "Backing up ERPNext"), follow these steps to revert to the backed up state.

    sudo su - erpnext
    # you should be in the root of the erpnext user home directory
    rm -Rf frappe-bench
    tar -xvf erp-prd-backup-[yyyy-mm-dd].tar.bz2
    cd frappe-bench
    # find the latest backup files in sites/[site name]/private/backups/
    # you will be prompted for the mysql pwd
    bench --force restore \
        sites/[site name]/private/backups/[sql.gz file]
    bench migrate
    bench clear-cache
    bench clear-website-cache
    bench restart

Following these commands will essentially wipe the old version completely and restore what was taken in the full backup to production.<br /><br />

Previous [3.2 Upgrading ERPNext](upgrade.md "Upgrading ERPNext") | Next: [3.3.4 Upgrade Troubleshooting](upgrade-trouble.md "Upgrade Troubleshooting")
