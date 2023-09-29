# OpenObserve + minio in kubernetes (1 node minio + 1 node openobserve)

create namespace:

```bash
kubectl create namespace openobserve-minio
```


Install minio in kubernetes:

```bash
kubectl apply -f minio.yaml
```

access console by port-forwarding an create a bucket:

```bash
kubectl port-forward -n openobserve-minio svc/minio 41234:41234
```

create the bucket:
`openobservebucket`


Install openobserve in kubernetes:

```bash
kubectl apply -f openobserve_minio.yaml
```

port-forward to access the openobserve console:

```bash
kubectl port-forward -n openobserve-minio svc/openobserve 5080:5080
```

access the console at: `http://localhost:5080`


Download the sample data:

```bash
curl -L https://zinc-public-data.s3.us-west-2.amazonaws.com/zinc-enl/sample-k8s-logs/k8slog_json.json.zip -o k8slog_json.json.zip
```

Unzip the sample data:

```bash
unzip k8slog_json.json.zip
```

Insert sample data:

```bash
curl http://localhost:5080/api/default/default/_json -i -u "root@example.com:Complexpass#123"  -d "@k8slog_json.json"
```

Visit the logs page to see the logs:

`http://localhost:5080`

