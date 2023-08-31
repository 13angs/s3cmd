# MongoDB Backup Job for Kubernetes


## Setup
- Rename .env.sample to .env
- Fill in all the variable values
- Create the secret from .env file

```bash
kubectl create secret generic <secret-name> --from-env-file=.env
```

- Run the k8s job

```bash
kubectl apply -f job.yaml
```

## Running the Backup Job

The backup job consists of two containers that execute sequentially:

1. backup-and-compress: This container performs the MongoDB backup and compression. The backup files are stored in the backup-volume which is an emptyDir volume.
2. upload-and-remove: This container uploads the compressed backup to object storage and then removes local backup files.

To monitor the status of the backup job:

```sh
kubectl get jobs
kubectl describe job/mongo-backup
```

## Cleanup

To remove the backup job and related resources:

```sh
kubectl delete -f job.yaml
```