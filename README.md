# MySQL Data Backup and Restore Sidecar

## Overview

It is a sidecar that will run inside mysql pod. Its main purpose is to backup and restore mysql data.

## Description

mysql backup and restore [image](https://hub.docker.com/r/stakater/mysql-backup-restore-s3/) [MBR] container can be used to backup mysql data on S3 bucket. It runs inside mysql pod as a sidecar container. Sidecar container dump the mysql data and store it in S3 as an object.


| Environment Variable | Description | Default value |
|---|---|---|
| CRON_TIME | Data backup interval | Default backup interval is "00 */1 * * *", which means take backup after each hour. |
| MYSQL_DB | Name of the database for backup | --all-databases is its default value which means that it will backup all databases. If a database name is provided then it will only take that database backup |
| S3_BUCKET_NAME | AWS S3 bucket name | "" |
| AWS_ACCESS_KEY_ID | AWS account access id | "" |
| AWS_SECRET_ACCESS_KEY | AWS account access id secret | "" |
| AWS_DEFAULT_REGION | AWS default region | "" |
| BACKUP_NAME | Name of the backup. | Its default value is yyyy.mm.dd-HH-MM-SS.sql |
| LAST_BACKUP | Name of the last backup. Last backup name in extracted from S3 bucket name using the script written in `run.sh` file. | None |
| RESTORE | Variable for check to restore data from S3 bucket. If `true` data will be restored from S3 bucket and store in location given in `RESTORE_FOLDER` env variable otherwise only data backup script will execute in the container. | true |
