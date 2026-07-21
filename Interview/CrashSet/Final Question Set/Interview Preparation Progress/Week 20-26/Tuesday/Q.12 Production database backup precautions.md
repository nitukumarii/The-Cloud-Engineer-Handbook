
### Production database backup precautions



Before taking a production database backup, I first ensure the backup is scheduled during the approved maintenance window if required. 
Then I verify that there is sufficient disk space using df -h and check the overall server health, such as CPU, memory, and disk utilization.
I also ensure there are no ongoing deployments, production incidents, 
or heavy batch jobs that could impact the backup. After the backup completes, I verify that it finished successfully and confirm the backup is valid for recovery if needed.
