# Ansible Tower Setup

## Download with browser locally

**Download** ansible tower gz file from:

https://releases.ansible.com/ansible-tower/setup/ansible-tower-setup-latest.tar.gz

## Download with &#39;wget&#39;:

wget https://releases.ansible.com/ansible-tower/setup/ansible-tower-setup-latest.tar.gz

##  Extraction

**Extract** the tar file:

tar xvzf ansible-tower-setup-latest.tar.gz

## Installation

**Navigate** towards the extracted directory

cd ansible-tower-setup-3.8.1-1

**Initiate** the Ansible Tower Setup:

./setup.sh

**Open** your browser and navigate to http://localhost

**Enter** your credentials:

Username: admin

Password: admin

# Preparation work on &quot;edb-ansible&quot; GitHub Repo

# Items to address for &quot;edb-ansible&quot; integration with Ansible Tower

## Preparation work on &quot;edb-ansible&quot; GitHub Repo

**Create** a folder named: &quot;collections&quot;

**Add** a file named: &quot;requirements.yml&quot; containing:

collections:

- name: edb\_devops.edb\_postgres

**Add** in the root folder a file named: &quot;hosts&quot;:

The content should be the same as the &quot;inventory.yml&quot; shown in the &quot;README.md&quot; of &quot;edb-ansible&quot; github repository

The content should not have the top line: &quot;---&quot;

## Credentials in the &quot;playbook.yml&quot;

Option 1:

Type them in the playbook.yml

Option 2:

Update the playbook.yml to handle &quot;vars&quot; section

Provide the variables in the extra vars section of the &quot;Templates&quot; for Ansible Tower

## Cluster details

Issue: The &quot;~/.edb&quot; is not stored nor available after the playbook execution

Options for resolution

1 - Display these details in the console. Drawback sensitive passwords will be stored in the log.

2 - Thoughts?

# Ansible Tower Configuration for &quot;edb-ansible&quot; usage

## Create a Project to download locally **edb\_devops.edb\_postgres** ansible galaxy collection

**Create** a **Project** that retrieves from the **edb-ansible GitHub Repository**

**Click**** Projects** on the left hand navigation

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** of the project, for example: &quot;EDB-ANSIBLE&quot;

**Select**** Git **from the** SCM TYPE ****Dropdown**

**Type** in the **SCM URL**** TextBox**:

https://github.com/EnterpriseDB/edb-ansible.git

**Check**** Clean ****CheckBox** from the **SCM UPDATE OPTIONS**

**Click** the **Green SAVE**** Button**

## Download locally the **edb\_devops.edb\_postgres** ansible galaxy collection

**Click**** Projects** on the left hand navigation

**Locate** the **EDB-ANSIBLE** project

**Click** the **EDB-ANSIBLE** project **Refresh Button**

## Create Credentials

### Create Cloud Credentials

Under **Resources** -\&gt; **Credentials**

**Click Credentials**

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** of the credential, for example: &quot;GCloud&quot;, &quot;AWS&quot; or &quot;Azure&quot;

**Select** the matching Cloud from the **Credential**** Type ****Dropdown**

_ **The next steps will vary depending on the Cloud Vendor you are utilizing** _

**Click** the **Green SAVE**** Button**

### Create Cloud Private Key Credentials

Under **Resources** -\&gt; **Credentials**

**Click Credentials**

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** of the credential, for example: &quot;GCloud – Private Key&quot;, &quot;AWS – Private Key&quot; or &quot;Azure – Private Key&quot;

**Select** the **Machine** from the **Credential**** Type ****Dropdown**

**Enter** the **username** for the credential, for example: &quot;centos&quot;, &quot;root&quot; or &quot;ec2-user&quot;

**Add** the **SSH PRIVATE KEY** for the credential by either **clicking** on the **Refresh Button** on the right hand side or **dragging and dropping** the **SSH PRIVATE KEY file** or its contents onto the **TextBox**

**Click** the **Green SAVE**** Button**

### Create the Cloud Inventory

Under **Resources** -\&gt; **Inventories**

**Click Projects**

**Enter** the **name** , for example: &quot;EDB - GCloud&quot;, &quot;EDB - AWS&quot; or &quot;EDB - Azure&quot;

**Click** the **Green SAVE**** Button**

**Click** the **SOURCES Button** on the top right

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** , for example: &quot;EDB – Gcloud - VMs&quot;, &quot;EDB – AWS - VMs&quot; or &quot;EDB – Azure - VMs&quot;

**Select** the **CLOUD SOURCE** from the **SOURCE**** Dropdown**

**Click** the **Green SAVE**** Button**

**Locate** the **Cloud Inventory** recently created in the **SOURCES Grid**

**Click** the **EDB-ANSIBLE** project **Refresh Button**

**Click** the **HOST Button** on the top right next to the **SOURCE Button**

Verify that the List of Hosts matches the Cloud Virtual Machines in which EPAS/Postgres playbook will be executed upon

### Create the Hosts Inventory

**Create** a **GitHub Repository** in which you can upload/create a **HOSTS** file that contains the inventory to be utilized

The **HOSTS** file should match the format listed in **the Inventory file content** available at: [https://github.com/EnterpriseDB/edb-ansible](https://github.com/EnterpriseDB/edb-ansible)

Within Ansible Tower

Under **Resources** -\&gt; **Inventories**

**Click Inventories**

**Enter** the **name** , for example: &quot;HOSTS&quot;

**Click** the **Green SAVE**** Button**

**Click** the **SOURCES Button** on the top right

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** , for example: &quot;Source Host File&quot;

**Select** the **Sourced from a Project** from the **SOURCE**** Dropdown**

**Select** the **Project** from the **PROJECT Dropdown**

**Select** the **Inventory File** from the **INVENTORY FILE**** Dropdown**

**Check**** OVERWRITE ****CheckBox** from the **UPDATE OPTIONS**

**Check**** UPDATE ON LAUNCH ****CheckBox** from the **UPDATE OPTIONS**

**Click** the **Green SAVE**** Button**

**Click** the **Refresh Button** from the **SOURCES** Grid

**Click** the **HOST Button** on the top right next to the **SOURCE Button**

Verify that the List of Hosts matches the Host List content of the file in the GitHub Repo utilized for the Hosts File

## Projects

### Create Download locally the **edb\_devops.edb\_postgres** ansible galaxy collection

Within Ansible Tower

Under **Resources** -\&gt; **Projects**

**Click Projects**

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** , for example: &quot;EDB – Ansible - Galaxy&quot;

**Select**** Git **from the** SCM TYPE ****Dropdown**

**Type** in the **SCM URL**** TextBox**:

https://github.com/EnterpriseDB/edb-ansible.git

**Type** in the **SCM URL**** TextBox**:

https://github.com/EnterpriseDB/edb-ansible.git

**Check**** Clean ****CheckBox** from the **SCM UPDATE OPTIONS**

**Click** the **Green SAVE**** Button**

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

Under **Resources** -\&gt; **Projects**

**Click Projects**

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** , for example: &quot;EDB – Ansible&quot;

**Select**** Manual **from the** SCM TYPE ****Dropdown**

**Select**** Manual **from the** PLAYBOOK DIRECTORY ****Dropdown**

**Click** the **Green SAVE**** Button**

## Templates

### Create Template to deploy the Cluster

Within Ansible Tower

Under **Resources** -\&gt; **Templates**

**Click Templates**

**Click** the **Green Plus Sign** on the right hand side of the browser

**Enter** the **name** , for example: &quot;EDB – Ansible - Template&quot;

**Select**** Run **from the** JOB TYPE ****Dropdown**

**Select**** Hosts **from the** INVENTORY Dropdown**

**Select**** EDB-ANSIBLE **from the** PROJECT Dropdown**

**Select**** playbook.yml **from the** PLAYBOOK ****Dropdown**

**Select**** \&lt;your cloud credentials\&gt; **from the** CREDENTIALS CheckBox**

**Select**** \&lt;your cloud private key file credentials\&gt; **from the** CREDENTIALS CheckBox**

**Check**** ENABLE PRIVILEGE ESCALATION **from the** OPTIONS**

**Click** the **Green SAVE**** Button**

**Click** the **LAUNCH Button**
