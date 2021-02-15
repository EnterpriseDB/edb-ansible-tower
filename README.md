# Ansible Tower Configuration for &quot;edb-ansible&quot; usage

## Create a Project to download locally **edb\_devops.edb\_postgres** ansible galaxy collection

**Create** a **Project** that connects to the **edb-ansible GitHub Repository**

**Click** ** Projects** on the left hand navigation

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** of the project, for example: &quot;EDB-ANSIBLE&quot;

**Select** **Git** from the **SCM TYPE** **Dropdown**

**Type** in the **SCM URL** **TextBox**:

https://github.com/EnterpriseDB/edb-ansible.git

**Check** **Clean** **CheckBox** from the **SCM UPDATE OPTIONS**

**Click** the **Green SAVE** ** Button**

## Download locally the **edb\_devops.edb\_postgres** ansible galaxy collection

**Click** **Projects** on the left hand navigation

**Locate** the **EDB-ANSIBLE** project

**Click** the **EDB-ANSIBLE** project **Refresh Button**

## Create Credentials

### Create Cloud Credentials

Under **Resources** -> **Credentials**

**Click Credentials**

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** of the credential, for example: &quot;GCloud&quot;, &quot;AWS&quot; or &quot;Azure&quot;

**Select** the matching Cloud from the **Credential** **Type** **Dropdown**

_ **The next steps will vary depending on the Cloud Vendor you are utilizing** _

**Click** the **Green SAVE** **Button**

### Create Cloud Private Key Credentials

Under **Resources** -> **Credentials**

**Click Credentials**

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** of the credential, for example: &quot;GCloud – Private Key&quot;, &quot;AWS – Private Key&quot; or &quot;Azure – Private Key&quot;

**Select** the **Machine** from the **Credential** **Type** **Dropdown**

**Enter** the **username** for the credential, for example: &quot;centos&quot;, &quot;root&quot; or &quot;ec2-user&quot;

**Add** the **SSH PRIVATE KEY** for the credential by either **clicking** on the **Refresh Button** on the right hand side or **dragging and dropping** the **SSH PRIVATE KEY file** or its contents onto the **TextBox**

**Click** the **Green SAVE** **Button**

### Create the Cloud Inventory

Under **Resources** -> **Inventories**

**Click Projects**

**Enter** the **name** , for example: &quot;EDB - GCloud&quot;, &quot;EDB - AWS&quot; or &quot;EDB - Azure&quot;

**Click** the **Green SAVE** **Button**

**Click** the **SOURCES Button** on the top right

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** , for example: &quot;EDB – Gcloud - VMs&quot;, &quot;EDB – AWS - VMs&quot; or &quot;EDB – Azure - VMs&quot;

**Select** the **CLOUD SOURCE** from the **SOURCE** **Dropdown**

**Click** the **Green SAVE** ** Button**

**Locate** the **Cloud Inventory** recently created in the **SOURCES Grid**

**Click** the **EDB-ANSIBLE** project **Refresh Button**

**Click** the **HOST Button** on the top right next to the **SOURCE Button**

Verify that the List of Hosts matches the Cloud Virtual Machines in which EPAS/Postgres playbook will be executed upon

### Create the Hosts Inventory

**Create** a **GitHub Repository** in which you can upload/create a **HOSTS** file that contains the inventory to be utilized

The **HOSTS** file should match the format listed in **the Inventory file content** available at: [https://github.com/EnterpriseDB/edb-ansible](https://github.com/EnterpriseDB/edb-ansible)

Within Ansible Tower

Under **Resources** -> **Inventories**

**Click Inventories**

**Enter** the **name** , for example: &quot;HOSTS&quot;

**Click** the **Green SAVE** **Button**

**Click** the **SOURCES Button** on the top right

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** , for example: &quot;Source Host File&quot;

**Select** the **Sourced from a Project** from the **SOURCE** **Dropdown**

**Select** the **Project** from the **PROJECT Dropdown**

**Select** the **Inventory File** from the **INVENTORY FILE** **Dropdown**

**Check** **OVERWRITE** **CheckBox** from the **UPDATE OPTIONS**

**Check** **UPDATE ON LAUNCH** **CheckBox** from the **UPDATE OPTIONS**

**Click** the **Green SAVE** **Button**

**Click** the **Refresh Button** from the **SOURCES** Grid

**Click** the **HOST Button** on the top right next to the **SOURCE Button**

Verify that the List of Hosts matches the Host List content of the file in the GitHub Repo utilized for the Hosts File

## Projects

### Create Download locally the **edb\_devops.edb\_postgres** ansible galaxy collection

Within Ansible Tower

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

### Prepare a local Ansible Tower Ansible Project

**Open** a Terminal Window

**Type** :

sudo su

cd /var/lib/awx/projects

mkdir edb-ansible

cd edb-ansible

**Locate and notice a directory that contains the name of the project created in the steps above**

Back in the Terminal Window

**Type** :

mkdir edb-ansible

cd edb-ansible

cp -r ../\_\&lt;directory\_name\&gt;/collections/ .

cp -r ../\_\&lt;directory\_name\&gt;/plugins/ .

cp -r ../\_\&lt;directory\_name\&gt;/playbook.yml .

### Create the Ansible Tower **edb-ansible** Ansible Project

Within Ansible Tower

Under **Resources** -> **Projects**

**Click Projects**

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** , for example: &quot;EDB – Ansible&quot;

**Select** **Manual** from the **SCM TYPE** **Dropdown**

**Select** **Manual** from the **PLAYBOOK DIRECTORY** **Dropdown**

**Click** the **Green SAVE** **Button**

## Templates

### Create Template to deploy the Cluster

Within Ansible Tower

Under **Resources** -> **Templates**

**Click Templates**

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** , for example: &quot;EDB – Ansible - Template&quot;

**Select** **Run** from the **JOB TYPE** **Dropdown**

**Select** **Hosts** from the **INVENTORY Dropdown**

**Select** **EDB-ANSIBLE** from the **PROJECT Dropdown**

**Select** **playbook.yml** from the **PLAYBOOK** **Dropdown**

**Select** **<your cloud credentials>** from the **CREDENTIALS CheckBox**

**Select** **<your cloud private key file credentials>** from the ** CREDENTIALS CheckBox**

**Check** **ENABLE PRIVILEGE ESCALATION** from the **OPTIONS**

**Click** the **Green SAVE** **Button**

**Click** the **LAUNCH Button**
