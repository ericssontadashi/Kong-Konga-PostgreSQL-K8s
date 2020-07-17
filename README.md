# Kong-Konga-PostgreSQL-K8s
Running Konga, Kong Community and PostgreSQL on Kubernetes

How to run:

kubectl apply -f pg_konga_pgadmin.yaml
kubectl apply -f configmap_for_kong.yaml
kubectl apply -f postgres_for_kong.yaml
kubectl apply -f proxy.yaml
kubectl apply -f admin.yaml

Add to hosts file (/etc/hosts):
- <YOUR_INGRESS_IP> pgadmin.testdomain.com.br
- <YOUR_INGRESS_IP> konga.testdomain.com.br
- <YOUR_INGRESS_IP> kong.admin.testdomain.com
- <YOUR_INGRESS_IP> kong.testdomain.com

On Mac run the commmand, after editing hosts file:
killall -HUP mDNSResponder

Initially deploying:
Konga:
- Ingress
- Service
- Deployment

PostgreSQL for Konga
- Service
- Deployment

PGAdmin
- Ingress
- Service
- Deployment

PostgreSQL for Kong
- Service
- Deployment

Kong Proxy Only:
- Ingress
- Service
- Deployment

Kong Admin Only:
- Ingress
- Service
- Deployment

TODO:
- Use KONGA_SEED_USER_DATA_SOURCE_FILE variable to create initial Konga user

Kong Credentials for PostgreSQL:
- User: kong
- Password: kong

Konga Credentials for PostgreSQL:
- User: konga
- Password: konga

-----------------------------------------------
For Grafana and Prometheus:

How to run:
kubectl apply -f prometheus.yaml
kubectl apply -f grafana.yaml

Add to hosts file (/etc/hosts):
- <YOUR_INGRESS_IP> grafana.testdomain.com.br
- <YOUR_INGRESS_IP> prometheus.testdomain.com.br

Open Grafana`s page http://grafana.testdomain.com.br and use the following user/password: admin/admin

In grafana -> Configuration -> DataSources click on Add data source button and then Prometheus
On URL, add Prometheus service name: http://prometheus:8080 and click on the button "Save & Test"

For Kong`s Postgres, do the following:
CREATE USER grafanareader WITH PASSWORD 'password';
GRANT USAGE ON SCHEMA public TO grafanareader;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO grafanareader;

In grafana -> Configuration -> DataSources click on Add data source button and then Postgres
On Host add Postgres service name: postgres.kong.svc.cluster.local
On Database, add: kong
On User and Password, add the credentials created above.
On SSL Mode, set disable.
On Version, set 9.6.

On Dashboards, import the following: 7424 and select Prometheus data source.

Import the following dashboard on grafana for cluster`s view: 315