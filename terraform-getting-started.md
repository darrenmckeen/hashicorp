# Getting Started with Terraform

Terraform is one of the most popular tools for defining and provisioning infrastructure as code (IaC). 

This guide will introduce you to the basics of Terraform to help you get started. You'll learn how to install Terraform, create infrastructure with Terraform, initialize the Terraform environment, provision the infrastructure, and finally, destroy the infrastructure.

Later, check out our [tutorials](https://developer.hashicorp.com/terraform/tutorials) for in-depth exercises on using Terraform with your favorite platform.

## Installing Terraform

[Download](https://developer.hashicorp.com/terraform/downloads) the Terraform binary and install it to your platform, machine, or environment. 



## Creating infrastructure with Terraform

After installing Terraform, we're going to use a Docker provider and deploy a local web server.

Create a project directory (`terraform-demo`).

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

Create `main.tf` for your Terraform code.

```shell
$ touch main.tf
```

Paste the following lines into `main.tf`.

```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}

provider "docker" {
    host = "unix:///var/run/docker.sock"
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = "training"
  ports {
    internal = 80
    external = 8080
  }
}

resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```


## Initializing the Terraform environment

Next, initialize the Terraform environment to download the required infrastructure providers.

Initialize Terraform.

```shell
$ terraform init
```




## Provisioning the infrastructure

Provision the resources.

```shell
$ terraform apply
```

You'll see this output.

```shell
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the
following symbols:
  + create

Terraform will perform the following actions:

  # docker_container.nginx will be created
  + resource "docker_container" "nginx" {
      + attach                                      = false
      + bridge                                      = (known after apply)
      + command                                     = (known after apply)
      + container_logs                              = (known after apply)
      + container_read_refresh_timeout_milliseconds = 15000
      + entrypoint                                  = (known after apply)
      + env                                         = (known after apply)
      + exit_code                                   = (known after apply)
      + hostname                                    = (known after apply)
      + id                                          = (known after apply)
      + image                                       = "sha256:xxxx"
      + init                                        = (known after apply)
      + ipc_mode                                    = (known after apply)
      + log_driver                                  = (known after apply)
      + logs                                        = false
      + must_run                                    = true
      + name                                        = "training"
      + network_data                                = (known after apply)
      + read_only                                   = false
      + remove_volumes                              = true
      + restart                                     = "no"
      + rm                                          = false
      + runtime                                     = (known after apply)
      + security_opts                               = (known after apply)
      + shm_size                                    = (known after apply)
      + start                                       = true
      + stdin_open                                  = false
      + stop_signal                                 = (known after apply)
      + stop_timeout                                = (known after apply)
      + tty                                         = false
      + wait                                        = false
      + wait_timeout                                = 60

      + healthcheck {
          + interval     = (known after apply)
          + retries      = (known after apply)
          + start_period = (known after apply)
          + test         = (known after apply)
          + timeout      = (known after apply)
        }

      + labels {
          + label = (known after apply)
          + value = (known after apply)
        }

      + ports {
          + external = 8080
          + internal = 80
          + ip       = "0.0.0.0"
          + protocol = "tcp"
        }
    }

Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

docker_container.nginx: Creating...
docker_container.nginx: Creation complete after 1s [id=xxx]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```



## Destroying the infrastructure

When you are done, run `destroy` to remove the infrastructure. Notice that the `destroy` command requires confirmation to run.

```shell
$ terraform destroy
```



## Next Steps

You now know how to install Terraform, create infrastructure with Terraform, initialize the Terraform environment, provision the infrastructure, and destroy the infrastructure.

To learn more about Terraform, see our documentation, tutorials, and other helpful resources.

* [Terraform documentation](https://www.terraform.io/docs/index.html)
* [Get Started - AWS](https://developer.hashicorp.com/terraform/tutorials/aws-get-started)
* [Get Started - Azure](https://developer.hashicorp.com/terraform/tutorials/azure-get-started)
* [Get Started - Docker](https://developer.hashicorp.com/terraform/tutorials/docker-get-started)
* [Get Started - Google Cloud](https://developer.hashicorp.com/terraform/tutorials/gcp-get-started)
* [Get Started - OCI](https://developer.hashicorp.com/terraform/tutorials/oci-get-started)
* [Get Started - Terraform Cloud](https://developer.hashicorp.com/terraform/tutorials/cloud-get-started)
* [Terraform Registry](https://registry.terraform.io/)
* [Terraform community](https://www.terraform.io/community/index.html) 
* [HashiCorp Learn](https://learn.hashicorp.com/terraform)
* [Terraform blog](
