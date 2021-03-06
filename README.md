# Ansible Tower Configuration for integration with &quot;edb-ansible&quot;

## 1. Projects

### Create a Project to retrieve hosts inventory file

**Create** a **Project** that connects to the a github repository that contains your host file in a format such as:

```
all:
  children:
    pemserver:
      hosts:
        pemserver1:
          ansible_host: xxx.xxx.xxx.xxx
          private_ip: xxx.xxx.xxx.xxx
    primary:
      hosts:
        primary1:
          ansible_host: xxx.xxx.xxx.xxx
          private_ip: xxx.xxx.xxx.xxx
          pem_agent: true
          pem_server_private_ip: xxx.xxx.xxx.xxx
    standby:
      hosts:
        standby1:
          ansible_host: xxx.xxx.xxx.xxx
          private_ip: xxx.xxx.xxx.xxx
          upstream_node_private_ip: xxx.xxx.xxx.xxx
          replication_type: synchronous
          pem_agent: true
          pem_server_private_ip: xxx.xxx.xxx.xxx
        standby2:
          ansible_host: xxx.xxx.xxx.xxx
          private_ip: xxx.xxx.xxx.xxx
          upstream_node_private_ip: xxx.xxx.xxx.xxx
          replication_type: asynchronous
          pem_agent: true
          pem_server_private_ip: xxx.xxx.xxx.xxx
```

The repository should also contain:
* A folder named: **collections**
* A file named: **requirements.yml** with the content:
```
collections:
  - name: edb_devops.edb_postgres
```

**Click** **Projects** on the left hand navigation

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** of the project, for example: &quot;EDB-CLOUD-Inventory&quot;

**Select** **Git** from the **SCM TYPE** **Dropdown**

**Type** in the **SCM URL** **TextBox**:

```
**http://<repository>**
```

**Check** **Clean** **CheckBox** from the **SCM UPDATE OPTIONS**

**Click** the **Green SAVE** **Button**

### Create a Project to download locally **edb\_devops.edb\_postgres** ansible galaxy collection

**Create** a **Project** that connects to the **edb-ansible GitHub Repository**

**Click** **Projects** on the left hand navigation

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** of the project, for example: &quot;EDB-ANSIBLE-GALAXY&quot;

**Select** **Git** from the **SCM TYPE** **Dropdown**

**Type** in the **SCM URL** **TextBox**:

https://github.com/EnterpriseDB/edb-ansible-tower

**Check** **Clean** **CheckBox** from the **SCM UPDATE OPTIONS**

**Click** the **Green SAVE** **Button**


## 2. Create Credentials

### Create Cloud Credentials

Under **Resources** -> **Credentials**

**Click Credentials**

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** of the credential, for example: &quot;GCloud&quot;, &quot;AWS&quot; or &quot;Azure&quot;

**Select** the matching Organization from the **ORGANIZATION** **Dropdown**

**Select** the matching Cloud from the **CREDENTIAL** **Dropdown**

**The next steps will vary depending on the Cloud Vendor you are utilizing**

**Click** the **Green SAVE** **Button**

### Create Cloud Private Key Credentials

Under **Resources** -> **Credentials**

**Click Credentials**

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** of the credential, for example: &quot;GCloud – Private Key&quot;, &quot;AWS – Private Key&quot; or &quot;Azure – Private Key&quot;

**Select** the matching Organization from the **ORGANIZATION** **Dropdown**

**Select** **Machine** from the **CREDENTIAL** **Dropdown**

**Enter** the **username** for the credential, for example: &quot;centos&quot;, &quot;root&quot; or &quot;ec2-user&quot; varies by your Linux Distribution

**Add** the **SSH PRIVATE KEY** for the credential by either **clicking** on the **Refresh Button** on the right hand side or **dragging and dropping** the **SSH PRIVATE KEY file** or its contents onto the **TextBox**

**Click** the **Green SAVE** **Button**

## 3. Create Inventories

### Create the Cloud Inventory

Under **Resources** -> **Inventories**

**Click** the **Green Plus Sign** on the right hand side of the browser

**Click Inventories**

**Enter** the **name** , for example: &quot;GCloud - Inventory&quot;, &quot;AWS - Inventory&quot; or &quot;Azure - Inventory&quot;

**Click** the **Green SAVE** **Button**

**Click** the **SOURCES Button** on the top right

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** , for example: &quot;Gcloud - VMs&quot;, &quot;AWS - VMs&quot; or &quot;Azure - VMs&quot;

**Select** the **CLOUD SOURCE** from the **SOURCE** **Dropdown**

**Click** the **Green SAVE** **Button**

**Scroll down**

**Locate** the **cloud - VMs** recently created in the **SOURCES Grid**

**Click** the **cloud - VMs** project **Start Sync Button** on the right hand side under **ACTIONS**

**Click** the **HOST Button** on the top right next to the **SOURCE Button**

**Wait** for the **Green Cloud** to be solid

Verify that the List of Hosts matches the Cloud Virtual Machines in which EPAS/Postgres playbook will be executed upon by **Clicking** the **HOST Button** on the top of the grid

### Create the Hosts Inventory

**Create** a **GitHub Repository** in which you can upload/create a **HOSTS** file that contains the inventory to be utilized

The **HOSTS** file should match the format listed in **the Inventory file content** available at: [https://github.com/EnterpriseDB/edb-ansible](https://github.com/EnterpriseDB/edb-ansible)

**Within Ansible Tower**

Under **Resources** -> **Inventories**

**Click** the **Green Plus Sign** on the right hand side of the browser

**Click Inventory**

**Enter** the **name** , for example: &quot;HOSTS&quot;

**Click** the **Green SAVE** **Button**

**Click** the **SOURCES Button** on the top right

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** , for example: &quot;Source Host File&quot;

**Select** the **Sourced from a Project** from the **SOURCE** **Dropdown**

**Select** the **EDB-CLOUD-Inventory** from the **PROJECT Dropdown**

**Select** the **Inventory File**, most likely a file named: **'hosts'** from the **INVENTORY FILE** **Dropdown**

**Check** **OVERWRITE** **CheckBox** from the **UPDATE OPTIONS**

**Check** **UPDATE ON LAUNCH** **CheckBox** from the **UPDATE OPTIONS**

**Click** the **Green SAVE** **Button**

**Scroll down**

**Click** the **Start Sync Button** from the **SOURCES** Grid under **ACTIONS**

**Click** the **HOST Button** on the top right next to the **SOURCE Button**

**Wait** for the **Green Cloud** to be solid

Verify that the List of Hosts matches the Host List content of the file  in the GitHub Repo utilized for the Hosts File by **Clicking** the **HOST Button** on the top of the grid

## 4. Create Local Manual Projects

### Download locally the **edb\_devops.edb\_postgres** Ansible Galaxy Collection

**Within Ansible Tower**

Under **Resources** -> **Projects** on the left hand navigation

**Click Projects Link** on the left hand side of the browser

**Locate** the project **EDB–ANSIBLE-GALAXY"

**Click** the **Get the latest SCM Revision Button** under the **Name** **Column**

**Wait** for the **Green Dot** to be solid next to the **EDB-ANSIBLE-GALAXY** **Project**

A directory located in: **/var/lib/awx/projects** with the '_xx__project_name' will be created

### Download locally the **EDB-CLOUD-INVENTORY**

**Within Ansible Tower**

Under **Resources** -> **Projects** on the left hand navigation

**Click** **Projects** on the left hand navigation

**Locate** the **EDB-CLOUD-INVENTORY** project

**Click** the **Get the latest SCM Revision Button** under the **Name** **Column**

**Wait** for the **Green Dot** to be solid next to the **EDB-CLOUD-INVENTORY** **Project**

A directory located in: **/var/lib/awx/projects** with the '_xx__project_name' will be created

### Prepare a local Ansible Tower Ansible Project

**Open** a **Terminal Window**

**Type**:

```
sudo su

cd /var/lib/awx/projects

mkdir edb-ansible

cd edb-ansible

cp -r ../\_**xx__edb_ansible_galaxy**/collections/ .

cp -r ../\_**xx__edb_ansible_galaxy**/plugins/ .

cp -r ../\_**xx__edb_ansible_galaxy**/playbook.yml .

```

### Create the Ansible Tower **edb-ansible** Project

**Within Ansible Tower**

Under **Resources** -> **Projects**

**Click Projects**

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** , for example: &quot;EDB – Ansible&quot;

**Select** **Manual** from the **SCM TYPE** **Dropdown**

**Select** **edb-ansible** from the **PLAYBOOK DIRECTORY** **Dropdown**

**Click** the **Green SAVE** **Button**

## 5. Templates

### Create Template to deploy the Cluster

**Within Ansible Tower**

Under **Resources** -> **Templates**

**Click** the **Green Plus Sign** on the right hand side of the browser

**Click Job Template**

**Enter** the **name** , for example: &quot;EDB–ANSIBLE-TEMPLATE&quot;

**Select** **Run** from the **JOB TYPE** **Dropdown**

**Select** **HOSTS** from the **INVENTORY Dropdown**

**Select** **EDB-ANSIBLE** from the **PROJECT Dropdown**

**Select** **playbook.yml** from the **PLAYBOOK** **Dropdown**

**Keep in mind the 'machine' and 'Cloud' credentials filter when selecting the credentials**

**Select** **'your cloud credentials'** from the **CREDENTIALS CheckBox**

**Select** **'your cloud private key file credentials'** from the **CREDENTIALS CheckBox**

**EXTRA VARIABLES TextBox** should have the parameters for the playbook as listed below:

```
---
pg_version: 12
pg_type: "EPAS"
yum_username: "yum_user"
yum_password: "yum_password"
```

**Check** **ENABLE PRIVILEGE ESCALATION** from the **OPTIONS Checkbox**

**Click** the **Green SAVE** **Button**

**Click** the **LAUNCH Button**

## Authenticating into the EDB Postgres Advanced Server Cluster

To change the authentication credentials you can reference the blog posting: [Postgres, Passwords and Installers](https://www.enterprisedb.com/blog/postgres-passwords-and-installers#:~:text=Just%20right%2Dclick%20each%20service,account%20on%20the%20EnterpriseDB%20website.)
