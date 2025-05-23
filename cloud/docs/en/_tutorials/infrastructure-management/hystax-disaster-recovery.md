# Fault protection with Hystax Acura

No matter how your resource allocation is structured, you can protect your infrastructure with the Hystax Acura solution.

Supported platforms:
* Cloud services.
* Hypervisors.
* Physical servers.

To begin, create a VM with Hystax Acura Disaster Recovery to manage replication and recovery. Continuous and periodic replication is performed by auxiliary Hystax Cloud Agent VMs. For a detailed description of the architecture, see the [documentation](https://hystax.com/documentation/dr/solution_description.html#architecture).

To run Hystax Acura Disaster Recovery, perform the steps below:
1. [Before you start](#before-begin).
1. [Create a service account and authorized key](#create-sa).
1. [Configure network traffic permissions](#network-settings).
1. [Create a VM with Hystax Acura](#create-acura-vm).
1. [Set up Hystax Acura](#setup-hystax-acura).
1. [Prepare and install the agents for disaster recovery](#prepare-agent).
1. [Enable replication](#start-protection).
1. [Set up the subnets to run the VMs](#prepare-network).
1. [Create a disaster recovery plan](#disaster-recovery-plan).
1. [Run exercises](#run-tests).
1. [Perform disaster recovery](#run-recover).

If you no longer need these resources, [delete them](#clear-out).

## Before you start {#before-begin}

{% include [before-you-begin](../_tutorials_includes/before-you-begin.md) %}

{% if product == "yandex-cloud" %}

### Required paid resources {#paid-resources}


{% note info %}

Please note that the infrastructure for Hystax Acura and Hystax Acura Cloud Agent, as well as all migrated VMs, consume [quotas]({{ link-console-quotas }}) and require payment.
* A Hystax Acura VM uses 8 vCPUs, 16 GB of RAM, and a 200 GB disk.
* A Hystax Acura Cloud Agent VM uses 2 vCPUs, 4 GB of RAM, and an 8 GB disk. A single Hystax Acura Cloud Agent VM can serve up to 6 replicated disks at the same time. If there are more than 6 disks, additional Hystax Acura Cloud Agent VMs are created automatically.

{% endnote %}

Resource costs for Hystax Acura and Hystax Acura Cloud Agent include:
* A fee for the disks and continuously running VMs (see [{{ compute-full-name }} pricing](../../compute/pricing.md)).
* A fee for storing images (see [{{ compute-full-name }} pricing](../../compute/pricing.md)).
* A fee for using a dynamic or static external IP address (see [{{ vpc-full-name }} pricing](../../vpc/pricing.md)).

{% endif %}

## Create a service account and authorized key {#create-sa}

The Hystax Acura Disaster Recovery application will run under a [service account](../../iam/concepts/users/service-accounts.md):
1. [Create](../../iam/operations/sa/create.md) service account `hystax-acura-account` with the `editor` and the `marketplace.meteringAgent` roles.
1. [Create](../../iam/operations/authorized-key/create.md) an authorized key for a service account.

Save the following for use in subsequent steps:
1. ID of the service account.
1. The service account authorized key ID.
1. The service account private authorized key.

## Configure network traffic permissions {#network-settings}

Configure network traffic permissions in the [default security group](../../vpc/concepts/security-groups.md#default-security-group). If a security group is unavailable, any incoming or outgoing VM traffic will be allowed.

If a security group is available, [add](../../vpc/operations/security-group-update.md#add-rule) to it the rules below:

| Traffic<br>direction | Description | Port<br>range | Protocol | Source<br>type | Source/Purpose |
--- | --- | --- | --- | --- | ---
| Incoming | http | 80 | TCP | CIDR | 0.0.0.0/0 |
| Incoming | https | 443 | TCP | CIDR | 0.0.0.0/0 |
| Incoming | https | 4443 | TCP | CIDR | 0.0.0.0/0 |
| Incoming | vmware | 902 | TCP | CIDR | 0.0.0.0/0 |
| Incoming | vmware | 902 | UDP | CIDR | 0.0.0.0/0 |
| Incoming | iSCSI | 3260 | TCP | CIDR | 0.0.0.0/0 |
| Incoming | udp | 12201 | UDP | CIDR | 0.0.0.0/0 |
| Incoming | TCP | 15,000 | TCP | CIDR | 0.0.0.0/0 |
| Outgoing | http | 80 | TCP | CIDR | 0.0.0.0/0 |
| Outgoing | https | 443 | TCP | CIDR | 0.0.0.0/0 |
| Outgoing | vmware | 902 | TCP | CIDR | 0.0.0.0/0 |
| Outgoing | vmware | 902 | UDP | CIDR | 0.0.0.0/0 |
| Outgoing | iSCSI | 3260 | TCP | CIDR | 0.0.0.0/0 |
| Outgoing | udp | 12201 | UDP | CIDR | 0.0.0.0/0 |

Save the security group ID. You will need it when creating VMs with Hystax Acura.

## Create a VM with Hystax Acura {#create-acura-vm}

Create a VM with a boot disk using an image of `Hystax Acura Disaster Recovery to {{ yandex-cloud }}`.

### Run the VM

{% list tabs %}

- Management console

   1. In the [management console]({{ link-console-main }}), select the folder to create your VM in.
   1. In the list of services, select **{{ compute-name }}**.
   1. Click **Create VM**.
   1. Under **Basic parameters**:
      * Enter `hystax-acura-vm` as your name and a VM description.
      * Select an [availability zone](../../overview/concepts/geo-scope.md) to place the VM in.
   1. Under **Image/boot disk selection**:
      * Click the **{{ marketplace-name }}** tab.
      * Click **Show more**.
      * In the public image list, select **Hystax Acura Disaster Recovery to {{ yandex-cloud }}** and click **Use**.
   1. Under **Disks**, enter 80 GB as your disk size.
   1. Under **File storage**, keep the default value.
   1. Under **Computing resources**, specify:
      * vCPU: 4.
      * RAM: 8 GB.
   1. Under **Network settings**:
      * Select a cloud network and a [subnet](../../vpc/concepts/network.md#subnet) from the list. If there is no subnet, click **Add subnet** and create one.

         To add a subnet, select a folder, enter a subnet name, select the availability zone, and specify a CIDR in the resulting window. Then click **Create**.
      * If a list of **Security groups** is available, select the [security group](../../vpc/concepts/security-groups.md#default-security-group) for which you previously configured network traffic permissions. If this list does not exist, all incoming and outgoing traffic will be enabled for the VM.

   1. Under **Access**, specify the information required to access the instance:
      * Select the previously created `hystax-acura-account` service account.
      * In the **Login** field, enter a user name for SSH access, such as `yc-user`.
      * In the **SSH key** field, paste the [public SSH key](../../compute/operations/vm-connect/ssh.md#creating-ssh-keys).
   1. Click **Create VM**.

- CLI

   {% include [cli-install](../../_includes/cli-install.md) %}

   {% include [default-catalogue](../../_includes/default-catalogue.md) %}

   In the terminal, run the following command:

   ```bash
   yc compute instance create \
     --name hystax-acura-vm \
     --zone <availability zone> \
     --cores 4 \
     --memory 8 \
     --network-interface subnet-id=<subnet ID>,nat-ip-version=ipv4,security-group-ids=<security group ID if previously configured> \
     --create-boot-disk name=hystax-acura-disk,size=80,image-id=<Hystax Acura image ID> \
     --service-account-id <service account ID> \
     --ssh-key ~/.ssh/id_rsa.pub
   ```

   Parameters:
   * `name`: VM name, such as `hystax-acura-vm`.
   * `zone`: [Availability zone](../../overview/concepts/geo-scope.md), such as `ru-central1-b`.
   * `cores`: [number of vCPUs](../../compute/concepts/vm.md) in your VM.
   * `memory`: [amount of RAM](../../compute/concepts/vm.md) in your VM.
   * `network-interface`: VM network interface description:
      * `subnet-id`: Subnet to connect your VM to.

         You can get a list of subnets using the `yc vpc subnet list` command.
      * `nat-ip-version=ipv4`: Connect a public IP.
      * `security-group-ids`: Security groups.

         You can retrieve a group list using the `yc vpc security-group list` command. If you omit the parameter, the [default security group](../../vpc/concepts/security-groups.md#default-security-group) will be assigned.
   * `create-boot-disk`: Crete a new disk for the VM:
      * `name`: Disk name, such as `hystax-acura-disk`.
      * `size`: Disk size.
      * `image-id`: Disk image ID.

         For this example, use `image_id` from the [product description](/marketplace/products/hystax/hystax-acura-disaster-recovery-3-7) in {{ marketplace-name }}.
   * `service-account-id`: ID of [previously created](#create-sa) service account.

      You can retrieve a list using the `yc iam service-account list` command.
   * `ssh-key`: Path to [public SSH key](../../compute/operations/vm-connect/ssh.md#creating-ssh-keys) file.

{% endlist %}

### Make the IP static

VMs are created with a public dynamic IP. Since a VM with Hystax Acura may reboot, make the IP static.

{% list tabs %}

- Management console

   To change a public IP address from dynamic to static:
   1. In the [management console]({{ link-console-main }}), open the page for the folder you are using.
   1. Select **Virtual Private Cloud**.
   1. Go to the **IP addresses** tab.
   1. Click ![image](../../_assets/options.svg) in the row next to the address of your Hystax Acura VM.
   1. In the menu that opens, select **Make static**.
   1. In the window that opens, click **Change**.

- CLI

   {% include [include](../../_includes/cli-install.md) %}

   {% include [default-catalogue](../../_includes/default-catalogue.md) %}

   To change a public IP address from dynamic to static:

   1. See the description of the CLI's update address attribute command:

      ```bash
      yc vpc address update --help
      ```

   1. Retrieve an address list:

      ```bash
      yc vpc address list
      ```

      Command output:

      ```bash
      +----------------------+------+---------------+----------+------+
      |          ID          | NAME |    ADDRESS    | RESERVED | USED |
      +----------------------+------+---------------+----------+------+
      | e2l46k8conff8n6ru1jl |      | 84.201.177.41 | false    | true |
      +----------------------+------+---------------+----------+------+
      ```

      The `false` value of the `RESERVED` parameter of the IP address with the `ID` `e2l46k8conff8n6ru1jl` shows that this address is dynamic.
   1. Make the address static by using the `--reserved=true` key and address `ID`:

      ```bash
      yc vpc address update --reserved=true e2l46k8conff8n6ru1jl
      ```

      Command output:

      ```bash
      id: e2l46k8conff8n6ru1jl
      folder_id: b1g7gvsi89m34pipa3ke
      created_at: "2022-01-14T09:36:46Z"
      external_ipv4_address:
        address: 84.201.177.41
        zone_id: ru-central1-b
        requirements: {}
      reserved: true
      used: true
      ```

      The `reserved` parameter value changed to `true` and the IP address is now static.

{% endlist %}

## Set up Hystax Acura {#setup-hystax-acura}

1. Open the `hystax-acura-vm` VM page in the [management console]({{ link-console-main }}) and find its public IP address.
1. Enter the `hystax-acura-vm` VM public IP address in your browser. The Hystax Acura initial setup screen opens.

   {% note info %}

   Booting the Hystax Acura Disaster Recovery VM for the first time initiates an installation process which can take over 20 minutes.

   {% endnote %}

1. By default, a Hystax Acura VM has a self-signed certificate installed. If you need to replace this certificate, follow the [procedure](https://support.hystax.com/portal/en/kb/articles/how-to-update-ssl-certificate-on-acura).
1. On the page that opens, fill in the following fields:
   * **Organization**: The name of your organization.
   * **Admin user login**: The email address for logging in to the Hystax Acura Control Panel.
   * **Password**: The administrator password.
   * **Confirm password**: Re-enter the administrator password.
1. Click **Next**.
1. Specify the connection settings {{ yandex-cloud }}:
   * **Service Account id**: The ID of your service account.
   * **Key id**: The ID of the authorized key of your service account.
   * **Private Key**: The private part of the authorized key of your service account.
   * **Default Folder id**: The ID of your folder.
   * **Zone**: availability zone.
   * **Hystax Service Subnet**: The ID of the subnet that the `hystax-acura-vm` virtual machine is connected to.
   * **Hystax Acura Control Panel Public IP** is the Hystax Acura VM's public IP. Replace the value in the field with the IP address obtained in step 1.
1. Click **Next**.

Hystax Acura automatically checks that it can access your cloud. If everything is correct, you can now log in to the Hystax Control Panel using your email address and password.

## Prepare and install the agents for disaster recovery {#prepare-agent}

The agents will install on the VMs that will be recovered to {{ yandex-cloud }}. To download and install an agent:
1. In the Hystax Acura control panel, click the Hystax logo in the top-left corner.
1. Under **Machines Groups**, create a group of protected VMs, such as `Prod-Web`.
1. Click the **Download agents** tab.
1. Choose one out of three types of agents depending on the OS:
   * VMware.
   * Windows.
   * Linux.

   Click **Next**.
1. Download and install the agent on the VMs you would like to protect:

   {% list tabs %}

   - VMware

      1. In the drop-down list, select a group of VMs, for which agents will be set up, such as `Prod-Web`.
      1. Select **New VMware vSphere** and fill in the fields:
         * **Platform Name**: The name of the platform.
         * **Endpoint**: The public IP address of the ESXi host.
         * **Login**: The user's login (the user must have the Administrator permissions).
         * **Password**: Password.

         Click **Next**.
      1. Click **Download Agent** and wait for the agent to download.
      1. Unpack the downloaded OVA file with the agent on the ESXi host.
      1. Start the VMs with the agent.

   - Windows

      1. In the drop-down list, select a group of VMs, for which agents will be set up, such as `Prod-Web`.
      1. Click **Next**.
      1. Click **Download Agent** and wait for the agent to download.
      1. Unpack the archive and install the agent from `hwragent.msi` on the VMs you would like to protect.

   - Linux

      1. In the drop-down list, select a group of VMs, for which agents will be set up, such as `Prod-Web`.
      1. Select Linux distribution type:
         * **CentOS/RHEL (.rpm package)**: CentOS or Red Hat-based.
         * **Debian/Ubuntu (.deb package)**: Ubuntu or Debian.
      1. Select driver install method:
         * **Pre-built**: Install a driver binary.
         * **DKMS**: Compile as you install.
      1. Click **Next**.
      1. Commands for the VM agent install will be generated. Run the commands as required by the procedure for your distribution and install method.

   {% endlist %}

## Enable replication {#start-protection}

After the agent is installed on the VMs to be protected, they will show up in the list as `Unprotected`.

To enable VM replication:
1. Open the Hystax Acura Control Panel. Click on the Hystax logo.
1. Under **Machines Groups**, deploy a VM group, such as `Prod-Web`.
1. Click ![image](../../_assets/options.svg) in the VM list on the right.
1. Set up a replication schedule and an image lifecycle policy using the **Edit replication schedule** and the **Edit retention policies** options. For more information, see the [Hystax documentation](https://hystax.com/documentation/dr/dr_overview.html?highlight=replication%20schedule#edit-replication-settings-schedule).
1. Select **Start Protection**.

VM replication will start. Once the process is complete, the VMs will change their status to `Protected`.

## Set up the subnets to run the VMs {#prepare-network}

As recovery starts, a Cloud site will be created as infrastructure in support of your application in {{ yandex-cloud }} that includes [subnets](../../vpc/concepts/network.md#subnet) and recovered VMs.

Create subnets, whose CIDRs will contain the IPs of your VMs.

For instance, if you are protecting two VMs with `10.155.0.23` and `192.168.0.3`as their IPs, create two subnets with `10.155.0.0/16` and `192.168.0.0/24` as their CIDRs. The subnets must be in the same [availability zone](../../overview/concepts/geo-scope.md) as the Hystax Acura Disaster Recovery VM.

To create subnets:

{% list tabs %}

- Management console

   1. Open the **{{ vpc-name }}** section in the folder to create a subnet in.
   1. Click on the name of the cloud network.
   1. Click **Add subnet**.
   1. Enter a name for the subnet, such as `net-b-155`.
   1. Select an availability zone from the drop-down list, such as `ru-central1-b`.
   1. Enter the subnet CIDR, such as `10.155.0.0/16`.
   1. Click **Create subnet**.

   Save the **IDs** of the created subnets. You will need these when you create your disaster recovery plan (DR plan).

- CLI

   {% include [cli-install](../../_includes/cli-install.md) %}

   {% include [default-catalogue](../../_includes/default-catalogue.md) %}

   1. Retrieve a list of the cloud networks:

      ```bash
      yc vpc network list
      ```

      Command output:

      ```bash
      +----------------------+----------------+
      |          ID          |      NAME      |
      +----------------------+----------------+
      | enplum7a98s1t0lhasi8 |    network     |
      +----------------------+----------------+
      ```

   1. Select the `NAME` or `ID` of the cloud network you need. Create a subnet:

      ```bash
      yc vpc subnet create \
        --name net-b-155 \
        --network-name network \
        --zone ru-central1-b \
        --range 10.155.0.0/16
      ```

   1. To view the subnet list, run the command below:

      ```bash
      yc vpc subnet list
      ```

      Command output:

      ```bash
      +----------------------+-------------+----------------------+----------------+---------------+------------------+
      |          ID          |    NAME     |      NETWORK ID      | ROUTE TABLE ID |     ZONE      |      RANGE       |
      +----------------------+-------------+----------------------+----------------+---------------+------------------+
      | e2lgjspicv43ainspl0n | net-b-155   | enplum7a98s1t0lhasi8 |                | ru-central1-b | [10.155.0.0/16]  |
      | e2l8g5u9ijd1sursv2ov | net-b-192   | enplum7a98s1t0lhasi8 |                | ru-central1-b | [192.168.0.0/24] |
      | e2l1hqsrpp932ik74aic | net-b       | enplum7a98s1t0lhasi8 |                | ru-central1-b | [192.168.1.0/24] |
      +----------------------+-------------+----------------------+----------------+---------------+------------------+
      ```

      Save the `IDs` of the subnets you created. You will need these when you create your disaster recovery plan (DR plan).

{% endlist %}

For more details, review the [Step-by step instructions](../../vpc/operations/subnet-create.md) in the {{ vpc-name}} documentation.

## Create a disaster recovery plan {#disaster-recovery-plan}

The DR plan includes a VM description and the network settings. You can have a plan generated automatically or create one manually.

{% list tabs %}

- Generate

   To generate a DR plan automatically:
   1. Open the Hystax Acura Control Panel. Click on the Hystax logo.
   1. Check the VMs you need on the list, click **Bulk actions**, and select **Generate DR plan**. You can also generate a plan for a group of VMs by clicking ![image](../../_assets/options.svg) in the group header.
   1. In the **Name** field, enter `Plan-1` as the name.
   1. Under **Subnets** on the right, specify the properties of the previously created subnets: **Subnet ID** and **CIDR**.
   1. Click **Save**.

- Manually

   To create a DR plan manually:
   1. Open the Hystax Acura Control Panel. Click on the Hystax logo.
   1. Click **Add DR Plan**.
   1. In the **Name** field, enter `Plan-1` as the name.
   1. Use one of the modes below:
      * `Basic`: Create a plan with standard settings.
      * `Expert`: Create a plan with flexible settings using JSON (see [detailed syntax description](https://hystax.com/documentation/dr/dr_overview.html#id2)).
   1. Add VMs using the ![image](../../_assets/options.svg) button. If required, specify an initialization ordering by using **Move to another Rank**.
   1. Modify the parameters of the VMs being created, as required, using the **Flavor name** field as follows: `<platform>-<cpu>-<ram>-<core_fraction>`. For example, `2-8-16-100`.
   1. Under **Subnets** on the right, specify the properties of the previously created subnets: **Subnet ID** and **CIDR**.
   1. Click **Save**.

   {% note warning %}

   Make sure that a valid IP address is specified for each VM.

   {% endnote %}

{% endlist %}

## Run exercises {#run-tests}

Regular exercises help verify disaster readiness as well as make changes to configurations in advance.

To run a test without shutting down the primary infrastructure:
1. Open the Hystax Acura Control Panel. Click on the Hystax logo.
1. In the top navigation panel, select **Run test Cloud Site**.
1. Select some disaster recovery plans on the list. Expand plans and edit as required.
1. Click **Next**.
1. In the **Cloud Site Name** field, enter a name, such as `Cloud-Site-from-Plan-1`.
1. In the **Restore point time** field, open the calendar window and select the restore point that will be used to create your VMs.
1. Under **Final DR plan**, verify that the plan is up-to-date and correct.
1. Click **Run Recover**.

The Hystax Acura control panel will display a **Cloud Sites** section. Wait for `Cloud-Site-from-Plan-1` to change its status to `Running`.

Open the [Management console]({{ link-console-main }}) and check that the required resources have moved successfully and that your applications are ready to run.

## Perform disaster recovery {#run-recover}

The procedure for an actual disaster recovery is no different than that for a test:
1. Open the Hystax Acura Control Panel. Click on the Hystax logo.
1. In the top navigation panel, select **Run Cloud Site**.

Repeat the [test recovery](#run-tests) steps.

## How to delete created resources {#clear-out}

To release folder resources:
1. [Delete](../../compute/operations/vm-control/vm-delete.md) the `hystax-acura-vm` VM.
1. [Delete](../../compute/operations/vm-control/vm-delete.md) the supplemental `cloud-agent` VMs.
1. [Delete](../../iam/operations/sa/delete.md) the `hystax-acura-account` service account.

If you reserved a public static IP address, [delete it](../../vpc/operations/address-delete.md).
