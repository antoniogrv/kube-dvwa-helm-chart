# DVWA Helm Chart
> A simple Helm distribution for the vulnerable-by-design DVWA application.

For alternative Kubernetes implementations of DVWA, please refer to [this repository](https://github.com/antoniogrv/kube-dvwa).

## Installation

Clone the repository and execute `helm install dvwa .` in the root directory. In order to access the application, run `kubectl port-forward deployment/dvwa 4281:80` and access `localhost:4281`.

## Additional Configuration

You can customize the chart's behavior by editing the `values.yaml` file.

```yaml
Database:
  Port: 3306
  DNS: "db"
  Replicas: 1
  Container:
    Repository: "docker.io/library"
    Image: 
      Name: "mariadb" # MySQL, PostgresSQL...
      Version: 10
  Volume:
    Access_Mode: "ReadWriteOnce"
    Minimum_Storage: "50Mi"
    Mount_Path: "/var/lib/mysql"

Web:
  Port: 80
  DNS: "dvwa"
  Replicas: 1
  Container:
    Repository: "ghcr.io/digininja"
    Image: 
      Name: "dvwa"
      # Refer to chart configuration (Chart.yaml) to set the DVWA image release 

```