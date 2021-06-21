---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "grafana_data_source Resource - terraform-provider-grafana"
subcategory: ""
description: |-
  Official documentation https://grafana.com/docs/grafana/latest/datasources/HTTP API https://grafana.com/docs/grafana/latest/http_api/data_source/
  The required arguments for this resource vary depending on the type of data
  source selected (via the 'type' argument).
---

# grafana_data_source (Resource)

* [Official documentation](https://grafana.com/docs/grafana/latest/datasources/)
* [HTTP API](https://grafana.com/docs/grafana/latest/http_api/data_source/)

The required arguments for this resource vary depending on the type of data
source selected (via the 'type' argument).

## Example Usage

```terraform
resource "grafana_data_source" "influxdb" {
  type          = "influxdb"
  name          = "myapp-metrics"
  url           = "http://influxdb.example.net:8086/"
  username      = "myapp"
  password      = "foobarbaz"
  database_name = influxdb_database.metrics.name
}

resource "grafana_data_source" "cloudwatch" {
  type = "cloudwatch"
  name = "cw-example"

  json_data {
    default_region = "us-east-1"
    auth_type      = "keys"
  }

  secure_json_data {
    access_key = "123"
    secret_key = "456"
  }
}

resource "grafana_data_source" "stackdriver" {
  type = "stackdriver"
  name = "sd-example"

  json_data {
    token_uri           = "https://oauth2.googleapis.com/token"
    authentication_type = "jwt"
    default_project     = "default-project"
    client_email        = "client-email@default-project.iam.gserviceaccount.com"
  }

  secure_json_data {
    private_key = "-----BEGIN PRIVATE KEY-----\nprivate-key\n-----END PRIVATE KEY-----\n"
  }
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- **name** (String) A unique name for the data source.
- **type** (String) The data source type. Must be one of the supported data source keywords.

### Optional

- **access_mode** (String) The method by which Grafana will access the data source: `proxy` or `direct`. Defaults to `proxy`.
- **basic_auth_enabled** (Boolean) Whether to enable basic auth for the data source. Defaults to `false`.
- **basic_auth_password** (String, Sensitive) Basic auth password. Defaults to ``.
- **basic_auth_username** (String) Basic auth username. Defaults to ``.
- **database_name** (String) (Required by some data source types) The name of the database to use on the selected data source server. Defaults to ``.
- **id** (String) The ID of this resource.
- **is_default** (Boolean) Whether to set the data source as default. This should only be `true` to a single data source. Defaults to `false`.
- **json_data** (Block List) (Required by some data source types) (see [below for nested schema](#nestedblock--json_data))
- **password** (String, Sensitive) (Required by some data source types) The password to use to authenticate to the data source. Defaults to ``.
- **secure_json_data** (Block List) (see [below for nested schema](#nestedblock--secure_json_data))
- **url** (String) The URL for the data source. The type of URL required varies depending on the chosen data source type.
- **username** (String) (Required by some data source types) The username to use to authenticate to the data source. Defaults to ``.

<a id="nestedblock--json_data"></a>
### Nested Schema for `json_data`

Optional:

- **assume_role_arn** (String) (CloudWatch) The ARN of the role to be assumed by Grafana when using the CloudWatch data source.
- **auth_type** (String) (CloudWatch) The authentication type used to access the data source.
- **authentication_type** (String) (Stackdriver) The authentication type: `jwt` or `gce`.
- **client_email** (String) (Stackdriver) Service account email address.
- **conn_max_lifetime** (Number) (MySQL, PostgreSQL, and MSSQL) Maximum amount of time in seconds a connection may be reused (Grafana v5.4+).
- **custom_metrics_namespaces** (String) (CloudWatch) A comma-separated list of custom namespaces to be queried by the CloudWatch data source.
- **default_project** (String) (Stackdriver) The default project for the data source.
- **default_region** (String) (CloudWatch) The default region for the data source.
- **encrypt** (String) (MSSQL) Connection SSL encryption handling: 'disable', 'false' or 'true'.
- **es_version** (Number) (Elasticsearch) Elasticsearch version as a number (2/5/56/60/70).
- **graphite_version** (String) (Graphite) Graphite version.
- **http_method** (String) (Prometheus) HTTP method to use for making requests.
- **interval** (String) (Elasticsearch) Index date time format. nil(No Pattern), 'Hourly', 'Daily', 'Weekly', 'Monthly' or 'Yearly'.
- **log_level_field** (String) (Elasticsearch) Which field should be used to indicate the priority of the log message.
- **log_message_field** (String) (Elasticsearch) Which field should be used as the log message.
- **max_concurrent_shard_requests** (Number) (Elasticsearch) Maximum number of concurrent shard requests.
- **max_idle_conns** (Number) (MySQL, PostgreSQL and MSSQL) Maximum number of connections in the idle connection pool (Grafana v5.4+).
- **max_open_conns** (Number) (MySQL, PostgreSQL and MSSQL) Maximum number of open connections to the database (Grafana v5.4+).
- **postgres_version** (Number) (PostgreSQL) Postgres version as a number (903/904/905/906/1000) meaning v9.3, v9.4, etc.
- **profile** (String) (CloudWatch) The credentials profile name to use when authentication type is set as 'Credentials file'.
- **query_timeout** (String) (Prometheus) Timeout for queries made to the Prometheus data source in seconds.
- **ssl_mode** (String) (PostgreSQL) SSLmode. 'disable', 'require', 'verify-ca' or 'verify-full'.
- **time_field** (String) (Elasticsearch) Which field that should be used as timestamp.
- **time_interval** (String) (Prometheus, Elasticsearch, InfluxDB, MySQL, PostgreSQL, and MSSQL) Lowest interval/step value that should be used for this data source.
- **timescaledb** (Boolean) (PostgreSQL) Enable usage of TimescaleDB extension.
- **tls_auth** (Boolean) (All) Enable TLS authentication using client cert configured in secure json data.
- **tls_auth_with_ca_cert** (Boolean) (All) Enable TLS authentication using CA cert.
- **tls_skip_verify** (Boolean) (All) Controls whether a client verifies the server’s certificate chain and host name.
- **token_uri** (String) (Stackdriver) The token URI used, provided in the service account key.
- **tsdb_resolution** (String) (OpenTSDB) Resolution.
- **tsdb_version** (String) (OpenTSDB) Version.


<a id="nestedblock--secure_json_data"></a>
### Nested Schema for `secure_json_data`

Optional:

- **access_key** (String, Sensitive) (CloudWatch) The access key to use to access the data source.
- **basic_auth_password** (String, Sensitive) (All) Password to use for basic authentication.
- **password** (String, Sensitive) (All) Password to use for authentication.
- **private_key** (String, Sensitive) (Stackdriver) The service account key `private_key` to use to access the data source.
- **secret_key** (String, Sensitive) (CloudWatch) The secret key to use to access the data source.
- **tls_ca_cert** (String, Sensitive) (All) CA cert for out going requests.
- **tls_client_cert** (String, Sensitive) (All) TLS Client cert for outgoing requests.
- **tls_client_key** (String, Sensitive) (All) TLS Client key for outgoing requests.

