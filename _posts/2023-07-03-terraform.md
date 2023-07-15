---
layout: post
title: Terraform Basics
subtitle: 
categories: Basics
tags: [Terraform, Cloud]
---

## [Providers](https://developer.hashicorp.com/terraform/language/providers)

are for interacting with remote systems, like cloud providers, and call APIs. `terraform init` will install providers.

### Provider Config

```tf
provider "aws" {
  access_key = var.aws_access_key
  secret_key = var.aws_secret_key
  region = "us-east-1"
}
```

## [Resources](https://developer.hashicorp.com/terraform/language/resources)

describe infrastructure objects and are implemented by a provider.

- resource type: "aws_instance"
- resource name: "server"
- resource argument: "ami", "instance_type", "tags"
- Meta_Argument: "count"

Use the `<RESOURCE TYPE>.<NAME>.<ATTRIBUTE>` to access attributes.

### Provisioners

are used to run some commands when the resource is created/destroyed.  Generally not recommnended by Terraform.

```tf
resource "aws_instance" "server" {
  count = 4 # create four similar EC2 instances

  ami           = "ami-a1b2c3d4"
  instance_type = "t2.micro"

  tags = {
    Name = "Server ${count.index}"
  }

  provisioner "local-exec" {
    command = "echo The server's IP address is ${self.private_ip}"
  }
}
```

### Meta-Arguemnts
- depends_on
- count
- for_each
- provider
- lifecycle
- provisioner

## [Data Sources](https://developer.hashicorp.com/terraform/language/data-sources)

are essentially read only resources.  Usually provided alongside with resource type for accessing info via `data.<TYPE>.<NAME>.<ATTRIBUTE>`.

```tf
data "aws_ami" "example" {
  most_recent = true

  owners = ["self"]
  tags = {
    Name   = "app-server"
    Tested = "true"
  }
}
```

### Meta-Arguemnts
- depends_on
- count
- for_each
- provider
- provisioner

## [Variables, Outputs and Values](https://developer.hashicorp.com/terraform/language/values)

### Input Variables

serve as parameters for a Terraform module, like function arguments, and can be accessed via `var.<NAME>`.

```tf
variable "image_id" {
  type = string
}

variable "availability_zone_names" {
  type    = list(string)
  default = ["us-west-1a"]
}

variable "docker_ports" {
  type = list(object({
    internal = number
    external = number
    protocol = string
  }))
  default = [
    {
      internal = 8300
      external = 8300
      protocol = "tcp"
    }
  ]
}
```

#### Optional arguments
- default
- type
- description
- validation
- sensitive
- nullable

Varialbes in root modudule can be assigned with `.tfvars` file.  Also, terraform searches for environment variables named `TF_VAR_` followed by the name of a declared variable.

```tf
image_id = "ami-abc123"
availability_zone_names = [
  "us-east-1a",
  "us-west-1c",
]
```

### Output Values

are like return values for a Terraform module, like function return values.  In a parent module, outputs of child modules are available in expressions as `module.<MODULE NAME>.<OUTPUT NAME>`.


```tf
output "instance_ip_addr" {
  value = aws_instance.server.private_ip
}
```

#### Optional arguments
- description
- precondition
- sensitive
- depends_on

### Local Values

are a convenience feature for assigning a short name to an expression, like local variable.  A set of related local values can be declared together in a single locals block and can be referenced as `local.<NAME>`.

```tf
locals {
  service_name = "forum"
  owner        = "Community Team"
}

locals {
  # Ids for multiple sets of EC2 instances, merged together
  instance_ids = concat(aws_instance.blue.*.id, aws_instance.green.*.id)
}

locals {
  # Common tags to be assigned to all resources
  common_tags = {
    Service = local.service_name
    Owner   = local.owner
  }
}
```


## [Modules](https://developer.hashicorp.com/terraform/language/modules)

Modules are containers for multiple resources that are used together. A module consists of a collection of `.tf` and/or `.tf.json` files kept together in a directory.

Calling a child module with specific values for its input variables.

```tf
module "consul" {
  source  = "hashicorp/consul/aws"
  version = "0.0.5"

  servers = 3
}
```

Accessing module output values via `module.<NAME>.<OUTPUT NAME>`.

### Meta-Arguments
- `source` argument is mandatory for all modules.
- `version` argument is recommended for modules from a registry.
- count
- for_each
- providers
- depends_on

### Module Sources

The `source` argument in a module block tells Terraform where to find the source code for the desired child module.

#### Local Paths

A local path must begin with either `./` or `../` to indicate that a local path is intended

```tf
module "consul" {
  source = "./consul"
}
```

#### Terraform Registry

Modules on the public Terraform Registry can be referenced using a registry source address of the form `<NAMESPACE>/<NAME>/<PROVIDER>`.

```tf
module "consul" {
  source = "hashicorp/consul/aws"
  version = "0.1.0"
}
```

#### GitHub

Terraform will recognize unprefixed `github.com` URLs and interpret them automatically as Git repository sources.

```tf
module "consul" {
  source = "github.com/hashicorp/example"
}
```


```tf
module "consul" {
  source = "hashicorp/consul/aws"
  version = "0.1.0"
}
```



## Other Topics

- [Files and Directories](https://developer.hashicorp.com/terraform/language/files)
- [Expressions](https://developer.hashicorp.com/terraform/language/expressions)
- [Functions](https://developer.hashicorp.com/terraform/language/functions)
- [State](https://developer.hashicorp.com/terraform/language/state)
- [Import](https://developer.hashicorp.com/terraform/language/import)