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

**Enter** the **name** of the credential, for example: &quot;GCloud&quot;, &quot;AWS&quot; or &quot;Azure&quot; varies by your Linux Distribution

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

**Enter** the **username** for the credential, for example: &quot;centos&quot;, &quot;root&quot; or &quot;ec2-user&quot;

**Add** the **SSH PRIVATE KEY** for the credential by either **clicking** on the **Refresh Button** on the right hand side or **dragging and dropping** the **SSH PRIVATE KEY file** or its contents onto the **TextBox**

**Click** the **Green SAVE** **Button**

## 3. Create Inventories

### Create the Cloud Inventory

Under **Resources** -> **Inventories**

**Click Projects**

**Enter** the **name** , for example: &quot;EDB - GCloud&quot;, &quot;EDB - AWS&quot; or &quot;EDB - Azure&quot;

**Click** the **Green SAVE** **Button**

**Click** the **SOURCES Button** on the top right

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** , for example: &quot;EDB – Gcloud - VMs&quot;, &quot;EDB – AWS - VMs&quot; or &quot;EDB – Azure - VMs&quot;

**Select** the **CLOUD SOURCE** from the **SOURCE** **Dropdown**

**Click** the **Green SAVE** **Button**

**Locate** the **Cloud Inventory** recently created in the **SOURCES Grid**

**Click** the **EDB-ANSIBLE** project **Refresh Button**

**Click** the **HOST Button** on the top right next to the **SOURCE Button**

Verify that the List of Hosts matches the Cloud Virtual Machines in which EPAS/Postgres playbook will be executed upon

### Create the Hosts Inventory

**Create** a **GitHub Repository** in which you can upload/create a **HOSTS** file that contains the inventory to be utilized

The **HOSTS** file should match the format listed in **the Inventory file content** available at: [https://github.com/EnterpriseDB/edb-ansible](https://github.com/EnterpriseDB/edb-ansible)

**Within Ansible Tower**

Under **Resources** -> **Inventories**

**Click Inventories**

**Enter** the **name** , for example: &quot;HOSTS&quot;

**Click** the **Green SAVE** **Button**

**Click** the **SOURCES Button** on the top right

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** , for example: &quot;Source Host File&quot;

**Select** the **Sourced from a Project** from the **SOURCE** **Dropdown**

**Select** the **Project** from the **PROJECT Dropdown**

**Select** the **Inventory File**, most likely a file named: **'hosts'** from the **INVENTORY FILE** **Dropdown**

**Check** **OVERWRITE** **CheckBox** from the **UPDATE OPTIONS**

**Check** **UPDATE ON LAUNCH** **CheckBox** from the **UPDATE OPTIONS**

**Click** the **Green SAVE** **Button**

**Click** the **Refresh Button** from the **SOURCES** Grid

**Click** the **HOST Button** on the top right next to the **SOURCE Button**

Verify that the List of Hosts matches the Host List content of the file in the GitHub Repo utilized for the Hosts File

## 4. Create Local Manual Projects

### Create the project to Download locally the **edb\_devops.edb\_postgres** ansible galaxy collection

**Within Ansible Tower**

Under **Resources** -> **Projects**

**Click Projects**

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** , for example: &quot;EDB – Ansible - Galaxy&quot;

**Select** **Git** from the **SCM TYPE** **Dropdown**

**Type** in the **SCM URL** **TextBox**:

https://github.com/EnterpriseDB/edb-ansible.git

**Type** in the **SCM URL** **TextBox**:

https://github.com/EnterpriseDB/edb-ansible.git

**Check** **Clean** **CheckBox** from the **SCM UPDATE OPTIONS**

**Click** the **Green SAVE** **Button**

**Click** the **Refresh Button** from the **PROJECTS** Grid

A folder located in: **/var/lib/awx/projects** with the '__**project_name' prefixes will be created

### Download locally the **edb\_devops.edb\_postgres** ansible galaxy collection

**Click** **Projects** on the left hand navigation

**Locate** the **EDB-ANSIBLE** project

**Click** the **EDB-ANSIBLE** project **Refresh Button**

A folder located in: **/var/lib/awx/projects** with the '__**project_name' prefixes will be created

### Prepare a local Ansible Tower Ansible Project

**Open** a **Terminal Window**

**Type**:

```
sudo su

cd /var/lib/awx/projects

mkdir edb-ansible

cd edb-ansible

```

**Locate and notice a directory that contains the name of the project created in the steps above**

**Back** in the **Terminal Window**

**playbook.yml** should look as shown below:

Playbook content should look like as shown below:

```
---
- hosts: all
  name: Postgres deployment playbook for reference architecture EDB-RA-2
  become: yes
  gather_facts: yes

  collections:
    - edb_devops.edb_postgres
  pre_tasks:
    - name: Initialize the user defined variables
      set_fact:
        use_hostname: yes
        disable_logging: false
        efm_version: 4.1
  roles:
    - role: setup_repo
      when: "'setup_repo' in lookup('edb_devops.edb_postgres.supported_roles', wantlist=True)"
    - role: install_dbserver
      when: "'install_dbserver' in lookup('edb_devops.edb_postgres.supported_roles', wantlist=True)"
    - role: init_dbserver
      when: "'init_dbserver' in lookup('edb_devops.edb_postgres.supported_roles', wantlist=True)"
    - role: setup_replication
      when: "'setup_replication' in lookup('edb_devops.edb_postgres.supported_roles', wantlist=True)"
    - role: manage_dbserver
      when: "'init_dbserver' in lookup('edb_devops.edb_postgres.supported_roles', wantlist=True)"
    - role: setup_efm
      when: "'setup_efm' in lookup('edb_devops.edb_postgres.supported_roles', wantlist=True)"
    - role: setup_pemserver
      when: "'setup_pemserver' in lookup('edb_devops.edb_postgres.supported_roles', wantlist=True)"
    - role: setup_pemagent
      when: "'setup_pemagent' in lookup('edb_devops.edb_postgres.supported_roles', wantlist=True)"
    - role: autotuning
      when: "'autotuning' in lookup('edb_devops.edb_postgres.supported_roles', wantlist=True)"
    - role: pot_setup
      when: group_names | select('search','barmanserver') | list | count < 1
```

**Type**:

```
mkdir edb-ansible

cd edb-ansible

cp -r ../\_**directory\_name**/collections/ .

cp -r ../\_**directory\_name**/plugins/ .

cp -r ../\_**directory\_name**/playbook.yml .

```

### Create the Ansible Tower **edb-ansible** Ansible Project

**Within Ansible Tower**

Under **Resources** -> **Projects**

**Click Projects**

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** , for example: &quot;EDB – Ansible&quot;

**Select** **Manual** from the **SCM TYPE** **Dropdown**

**Select** **Manual** from the **PLAYBOOK DIRECTORY** **Dropdown**

**Click** the **Green SAVE** **Button**

## 5. Templates

### Create Template to deploy the Cluster

**Within Ansible Tower**

Under **Resources** -> **Templates**

**Click Templates**

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** , for example: &quot;EDB – Ansible - Template&quot;

**Select** **Run** from the **JOB TYPE** **Dropdown**

**Select** **Hosts** from the **INVENTORY Dropdown**

**Select** **EDB-ANSIBLE** from the **PROJECT Dropdown**

**Select** **playbook.yml** from the **PLAYBOOK** **Dropdown**

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
