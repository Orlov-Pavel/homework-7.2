# Домашнее задание к занятию "7.2. Облачные провайдеры и синтаксис Terraform."
1. Terraform установлен и инициализирован по инструкции яндекса:  
   ![terraform init](./pictures/terraform%20init.PNG)  
   Переменные, чтобы не указывать токен в коде, добавлены:  
   ![YC variables for terraform](./pictures/YC%20variables%20for%20terraform.PNG)
2. terraform plan отработал без ошибок:  
```
    root@ubuntu:~/netology/7.2/cloud-terraform# terraform plan
    Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
    + create

    Terraform will perform the following actions:

    # yandex_compute_instance.vm-netology will be created
    + resource "yandex_compute_instance" "vm-netology" {
        + created_at                = (known after apply)
        + folder_id                 = (known after apply)
        + fqdn                      = (known after apply)
        + hostname                  = (known after apply)
        + id                        = (known after apply)
        + metadata                  = {
            + "ssh-keys" = <<-EOT
                    ubuntu:ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJdr1z+fQ86mkrd9yqM2ubQwkvB2zTPf7PTXt3tOaLdy root@ubuntu
                EOT
            }
        + name                      = "netology"
        + network_acceleration_type = "standard"
        + platform_id               = "standard-v1"
        + service_account_id        = (known after apply)
        + status                    = (known after apply)
        + zone                      = (known after apply)

        + boot_disk {
            + auto_delete = true
            + device_name = (known after apply)
            + disk_id     = (known after apply)
            + mode        = (known after apply)

            + initialize_params {
                + block_size  = (known after apply)
                + description = (known after apply)
                + image_id    = "fd8ch5n0oe99ktf1tu8r"
                + name        = (known after apply)
                + size        = (known after apply)
                + snapshot_id = (known after apply)
                + type        = "network-hdd"
                }
            }

        + network_interface {
            + index              = (known after apply)
            + ip_address         = (known after apply)
            + ipv4               = true
            + ipv6               = (known after apply)
            + ipv6_address       = (known after apply)
            + mac_address        = (known after apply)
            + nat                = true
            + nat_ip_address     = (known after apply)
            + nat_ip_version     = (known after apply)
            + security_group_ids = (known after apply)
            + subnet_id          = (known after apply)
            }

        + placement_policy {
            + host_affinity_rules = (known after apply)
            + placement_group_id  = (known after apply)
            }

        + resources {
            + core_fraction = 100
            + cores         = 2
            + memory        = 2
            }

        + scheduling_policy {
            + preemptible = (known after apply)
            }
        }

    # yandex_vpc_network.network-1 will be created
    + resource "yandex_vpc_network" "network-1" {
        + created_at                = (known after apply)
        + default_security_group_id = (known after apply)
        + folder_id                 = (known after apply)
        + id                        = (known after apply)
        + labels                    = (known after apply)
        + name                      = "network1"
        + subnet_ids                = (known after apply)
        }

    # yandex_vpc_subnet.subnet-1 will be created
    + resource "yandex_vpc_subnet" "subnet-1" {
        + created_at     = (known after apply)
        + folder_id      = (known after apply)
        + id             = (known after apply)
        + labels         = (known after apply)
        + name           = "subnet1"
        + network_id     = (known after apply)
        + v4_cidr_blocks = [
            + "192.168.10.0/24",
            ]
        + v6_cidr_blocks = (known after apply)
        + zone           = "ru-central1-a"
        }

    Plan: 3 to add, 0 to change, 0 to destroy.

    Changes to Outputs:
    + external_ip_address_vm-netology = (known after apply)
    + internal_ip_address_vm-netology = (known after apply)

    ────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

    Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
```
   Собственный образ можно создать при помощи утилиты ```packer```.  
   Мой файл [main.tf](./terraform/main.tf).