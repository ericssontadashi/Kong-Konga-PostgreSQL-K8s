# Kong-Konga-PostgreSQL-K8s
Running Konga, Kong Community and PostgreSQL on Kubernetes

How to run:

kubectl apply -f pg_konga_pgadmin.yaml

Add to hosts file:
- <YOUR_INGRESS_IP> pgadmin.testdomain.com.br
- <YOUR_INGRESS_IP> konga.testdomain.com.br

Initially deploying:
Konga:
- Ingress
- Service
- Deployment

PostgreSQL
- Service
- Deployment

PGAdmin
- Ingress
- Service
- Deployment

TODO:
- Deploy Kong Community
- Use KONGA_SEED_USER_DATA_SOURCE_FILE variable to create initial Konga user

Konga Credentials for PostgreSQL:
- User: konga
- Password: konga