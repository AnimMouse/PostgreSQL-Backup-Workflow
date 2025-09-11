# PostgreSQL Backup Reusable Workflows
Reusable GitHub Actions workflows for backing up PostgreSQL databases.

## Rclone
Example workflow:

```yaml
name: Backup PostgreSQL
on:
  schedule:
    - cron: '7 1,10 * * 1-5'
  workflow_dispatch:
  
concurrency:
  group: ${{ github.workflow }}
  
jobs:
  backup:
    uses: AnimMouse/PostgreSQL-Backup-Workflow/.github/workflows/rclone.yaml@v1
    with:
      file_name: postgresql-backup
      dbname: postgres
      host: aws-0-ap-southeast-1.pooler.supabase.com
      port: 5432
      username: postgres
      postgresql_version: 17
      zstd_clevel: 17
      rclone_remote_to: "dest:PostgreSQL Backups"
    secrets:
      password: ${{ secrets.PASSWORD }}
      rclone_config: ${{ secrets.RCLONE_CONFIG }}
````