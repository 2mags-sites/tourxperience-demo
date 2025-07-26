# TourXperience Demo Site

This is a demo deployment for testing GitHub Actions to WHM/cPanel.

Last updated: 2025-01-24 19:55 UTC

Repository is now PUBLIC to use organization secrets.

---

## Deployment Notes

This project uses the `appleboy/scp-action` for deployment via SSH. Several issues were encountered and resolved during setup:

1.  **SSH Key Authentication:** The primary deployment failure was due to `Permission denied (publickey)`. This was resolved by generating a new SSH key pair and ensuring the public key was correctly added to the `authorized_keys` file for the `root` user in WHM (`Security Center` > `Manage root's SSH Keys`).

2.  **Rsync Failures:** Initial attempts to use `rsync` (both via the `burnett01/rsync-deployments` action and manual commands) failed with a persistent `hostname contains invalid characters` error. The root cause was not definitively identified but appears to be an environmental issue with how `rsync` parses the host string in the GitHub Actions environment.

3.  **Working Solution:** The final, working solution uses the `appleboy/scp-action`. While potentially slower than `rsync` for large projects as it transfers all files each time, it has proven to be a reliable and robust method for this environment.
