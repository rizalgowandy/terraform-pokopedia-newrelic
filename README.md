# terraform-peractio-newrelic

Terraform module to interact with NewRelic.

### Getting Started

```hcl
data "newrelic_entity" "app_grpc" {
  name   = "app_grpc"
  # Replace with your service name.
  domain = "APM"
  type   = "APPLICATION"
}

module "grpc_dashboard" {
  source = "git::https://github.com/rizalgowandy/terraform-peractio-newrelic?ref=v0.0.2"

  service_name   = "app_grpc"
  # Replace with your service name.
  application_id = data.newrelic_entity.app_grpc.application_id
  event_name     = "grpc_performance"
  # Replace with your metric name.
  event_methods  = [
    "/inventory.v1.Inventory/GetProducts", # Replace with your metric method name.
    "/inventory.v1.Inventory/CheckStocks",
  ]
}
```
