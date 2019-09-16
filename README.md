# Elastic Stack
Repository for Kubernetes ELK Stack containing the following apps:

- [Elasticsearch](https://www.elastic.co/products/elasticsearch)
- [Kibana](https://www.elastic.co/products/kibana)
- [Logstash](https://www.elastic.co/products/logstash)

## Resource allocation
Set the following values in the `yml` files for your needs

- `elasticsearch.yml`

```yml
  # Set the storage settings based on available infrastructure & needs
  volumeClaimTemplates:
  - metadata:
      name: data
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 30Gi
      storageClassName: rbd

      containers:
      	# Set JAVA options for Elasticsearch
        env:
        - name: ES_JAVA_OPTS
          value: "-Xmx4g -Xms4g"
        # Limit resources based on available architecture
        resources:
          requests:
            cpu: 1
            memory: 4Gi
          limits:
            cpu: 4
            memory: 8Gi
```

- `kibana.yml`

```yml
      containers:
      	# Limit resources based on available architecture
        resources:
          requests:
            cpu: 1
            memory: 2Gi
          limits:
            cpu: 2
            memory: 4Gi
```

- `logstash.yml`

TBD

## Base code
This repository is the modification of official [elastic helm-charts](https://github.com/elastic/helm-charts) for proper deployment on K8s cloud
