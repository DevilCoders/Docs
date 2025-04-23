# Pulumi vm deployment

* Create project with: `pulumi new azure-go`
* Describe your infrastructure as a code in `main.go` file.
* Preview changes `pulumi preview`

````shell
❯ pulumi preview
Please choose a stack, or create a new one: dev
Previewing update (dev)

     Type                               Name                                               Plan
 +   pulumi:pulumi:Stack                azure-dev                                          create
 +   ├─ azure:core:ResourceGroup        example-resource-group                             create
 +   ├─ azure:network:VirtualNetwork    example-virtual-network                            create
 +   ├─ azure:network:Subnet            example-subnet                                     create
 +   ├─ azure:network:NetworkInterface  azeastus-0003.rtc-oc.yandex.net-network-interface  create
 +   ├─ azure:network:NetworkInterface  azeastus-0007.rtc-oc.yandex.net-network-interface  create
 +   ├─ azure:network:NetworkInterface  azeastus-0004.rtc-oc.yandex.net-network-interface  create
 +   ├─ azure:network:NetworkInterface  azeastus-0006.rtc-oc.yandex.net-network-interface  create
 +   ├─ azure:network:NetworkInterface  azeastus-0005.rtc-oc.yandex.net-network-interface  create
 +   ├─ azure:network:NetworkInterface  azeastus-0009.rtc-oc.yandex.net-network-interface  create
 +   ├─ azure:network:NetworkInterface  azeastus-0001.rtc-oc.yandex.net-network-interface  create
 +   ├─ azure:network:NetworkInterface  azeastus-0000.rtc-oc.yandex.net-network-interface  create
 +   ├─ azure:network:NetworkInterface  azeastus-0008.rtc-oc.yandex.net-network-interface  create
 +   ├─ azure:network:NetworkInterface  azeastus-0002.rtc-oc.yandex.net-network-interface  create
 +   ├─ azure:compute:VirtualMachine    azeastus-0003.rtc-oc.yandex.net                    create
 +   ├─ azure:compute:VirtualMachine    azeastus-0006.rtc-oc.yandex.net                    create
 +   ├─ azure:compute:VirtualMachine    azeastus-0007.rtc-oc.yandex.net                    create
 +   ├─ azure:compute:VirtualMachine    azeastus-0004.rtc-oc.yandex.net                    create
 +   ├─ azure:compute:VirtualMachine    azeastus-0005.rtc-oc.yandex.net                    create
 +   ├─ azure:compute:VirtualMachine    azeastus-0001.rtc-oc.yandex.net                    create
 +   ├─ azure:compute:VirtualMachine    azeastus-0009.rtc-oc.yandex.net                    create
 +   ├─ azure:compute:VirtualMachine    azeastus-0000.rtc-oc.yandex.net                    create
 +   ├─ azure:compute:VirtualMachine    azeastus-0008.rtc-oc.yandex.net                    create
 +   └─ azure:compute:VirtualMachine    azeastus-0002.rtc-oc.yandex.net                    create

Resources:
    + 24 to create
````

* Deploy resources: `pulumi up`
* Destroy all resources: `pulumi destroy`
