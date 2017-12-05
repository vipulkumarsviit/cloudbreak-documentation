## Cloudbreak CLI Reference  

This section will help you get started with the Cloudbreak CLI after you have [installed and configured it](cli-install.md).


### Command Structure

The CLI command can contain multiple parts. The first part is a set of global options. The next part is the command. The next part is a set of command options and arguments which could include sub-commands.

<pre>cb [global options] command [command options] [arguments...]</pre>


### Command Output

You can control the output from the CLI using the --output argument. The possible output formats include:

* JSON (`json`)
* YAML (`yaml`)
* Formatted table (`table`)

For example:

<pre>cb cluster list --output json</pre>

<pre>cb clusters list --output yaml</pre>

<pre>cb cluster list --output table</pre>


### Commands

Configure CLI:  

* [configure](#configure)  


Cloud Provider:

* [cloud availability-zones](cloud-availability-zones)  
* [cloud regions](cloud-regions)       
* [cloud volumes](cloud-volumes)   
* [cloud instances](cloud-instances)   
 
 
Credential:  

* [credential create](#credential-create)   
* [credential delete](#credential-delete)        
* [credential describe](#credential-describe)        
* [credential list](#credential-list)         
 

Blueprint:   
       
* [blueprint create](#blueprint-create)  
* [blueprint delete](#blueprint-delete)           
* [blueprint describe](#blueprint-describe)         
* [blueprint list](#blueprint-list)           
 

Cluster: 
       
* [cluster change-ambari-password](#cluster-change-ambari-password)   
* [cluster create](#cluster-create) 
* [cluster delete](#cluster-delete)              
* [cluster describe](#cluster-describe)    
* [cluster generate-template](#cluster-generate-template)   
* [cluster generate-reinstall-template](#cluster-generate-reinstall-template)  
* [cluster list](#cluster-list)    
* [cluster repair](#cluster-repair)             
* [cluster scale](#cluster scale)      
* [cluster start](#cluster-start)        
* [cluster stop](#cluster-stop)              
* [cluster sync](#cluster-sync)             
       

Recipe:  
       
* [recipe create](#recipe-create)     
* [recipe delete](#recipe-delete)            
* [recipe describe](#recipe-describe)            
* [recipe list](#recipe-list)              
            











__________________________________

#### blueprint create 

Adds a new blueprint from a file or from a URL.

**Sub-commands**

**`from-url`** Creates a blueprint by downloading it from a URL location  
**`from-file`** Creates a blueprint by reading it from a local file

**Required Options**

**`from-url`** 

**`--name <value>`** Name of the blueprint  
**`--url <value>`** URL location of the Ambari blueprint JSON file

**`from-file`** 

**`--name <value>`** Name of the blueprint  
**`--file <value>`** Location of the Ambari blueprint JSON file on the local machine


**Options**

**`--description <value>`**  Description of the resource  
**`--public`**  Public in account  
**`--server <value>`** Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`** User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]  
**`--profile <value>`** Selects a config profile to use [$CB_PROFILE] 


**Examples**

Adds a blueprint from a URL:

<pre>cb blueprint create from-url --url https://someurl.com/test.bp --name test1</pre>

Adds a blueprint from a local file:

<pre>cb blueprint create from-file --file /Users/test/Documents/blueprints/test.bp --name test2</pre>


**Related Links**

[Blueprints](blueprints.md)









__________________________________

#### blueprint delete

Deletes an existing blueprint.

**Required Options**

**`--name <value>`** Name of the blueprint 

**Options**

[comment]: <> (This also has "--output option", which I believe should not be there.)

**`--server <value>`** Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`** User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]  
**`--profile <value>`** Selects a config profile to use [$CB_PROFILE] 

**Examples**

<pre>cb blueprint delete --name "testbp"</pre>

**Related Commands**

[blueprint list](#blueprint-list)














__________________________________

#### blueprint describe

Describes an existing blueprint.

**Required Options**

**`--name <value>`** Name of the blueprint 

**Options**

**`--server <value>`** Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`** User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]  
**`--profile <value>`** Selects a config profile to use [$CB_PROFILE]  
**`--output <value>`**  Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]

**Examples**

<pre>cb blueprint describe --name "Data Science: Apache Spark 2.1, Apache Zeppelin 0.7.0"
{
  "Name": "Data Science: Apache Spark 2.1, Apache Zeppelin 0.7.0",
  "Description": "Data Science: Apache Spark 2.1, Apache Zeppelin 0.7.0",
  "HDPVersion": "2.6",
  "HostgroupCount": "3",
  "Tags": "DEFAULT"
}</pre>

**Related Commands**

[blueprint list](#blueprint-list)













__________________________________

#### blueprint list

Lists available blueprints.

**Required Options**

Nome

**Options**

**`--server <value>`** Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`** User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]  
**`--profile <value>`** Selects a config profile to use [$CB_PROFILE]  
**`--output <value>`** Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]  

**Examples**

<pre>cb blueprint list
[
  {
    "Name": "Data Science: Apache Spark 2.1, Apache Zeppelin 0.7.0",
    "Description": "Data Science: Apache Spark 2.1, Apache Zeppelin 0.7.0",
    "HDPVersion": "2.6",
    "HostgroupCount": "3",
    "Tags": "DEFAULT"
  },
  {
    "Name": "EDW-ETL: Apache Hive 1.2.1, Apache Spark 2.1",
    "Description": "EDW-ETL: Apache Hive 1.2.1, Apache Spark 2.1",
    "HDPVersion": "2.6",
    "HostgroupCount": "3",
    "Tags": "DEFAULT"
  },
  {
    "Name": "26EDW-ETL: Apache Hive 1.2.1, Apache Spark 1.6",
    "Description": "26EDW-ETL: Apache Hive 1.2.1, Apache Spark 1.6",
    "HDPVersion": "2.6",
    "HostgroupCount": "3",
    "Tags": "DEFAULT"
  },
  {
    "Name": "Data Science: Apache Spark 1.6, Apache Zeppelin 0.7.0",
    "Description": "Data Science: Apache Spark 1.6, Apache Zeppelin 0.7.0",
    "HDPVersion": "2.6",
    "HostgroupCount": "3",
    "Tags": "DEFAULT"
  },
  {
    "Name": "BI: Druid 0.9.2 (Technical Preview)",
    "Description": "BI: Druid 0.9.2 (Technical Preview)",
    "HDPVersion": "2.6",
    "HostgroupCount": "3",
    "Tags": "DEFAULT"
  },
  {
    "Name": "EDW-Analytics: Apache Hive 2 LLAP, Apache Zeppelin 0.7.0",
    "Description": "EDW-Analytics: Apache Hive 2 LLAP, Apache Zeppelin 0.7.0",
    "HDPVersion": "2.6",
    "HostgroupCount": "3",
    "Tags": "DEFAULT"
  },
  {
    "Name": "EDW-ETL: Apache Hive 1.2.1, Apache Spark 1.6",
    "Description": "EDW-ETL: Apache Hive 1.2.1, Apache Spark 1.6",
    "HDPVersion": "2.6",
    "HostgroupCount": "3",
    "Tags": "DEFAULT"
  }
]</pre>


**Related Commands**

[blueprint describe](#blueprint-describe)






__________________________________

#### cloud availability-zones

Lists the available availability zones in a region. 

**Required Options**

**`--credential <value>`**  Name of the credential  
**`--region <value>`**   Name of the region  
   
**Options**

**`--server <value>`**  Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`**  User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]   
**`--profile <value>`**  Selects a config profile to use [$CB_PROFILE]   
**`--output <value>`**  Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]  

**Examples**

Lists availability zones in the us-west-2 (Oregon) region on the AWS account identified by the credential called "aws-cred":

<pre>cb cloud availability-zones --credential aws-cred --region us-west-2
[
  {
    "Name": "us-west-2a"
  },
  {
    "Name": "us-west-2b"
  },
  {
    "Name": "us-west-2c"
  }
]</pre>


  
  
  
  
  
  
__________________________________

#### cloud regions  

Lists available regions. 

**Required Options**

**`--credential <value>`**  Name of the credential  
   
**Options**

**`--server <value>`**  Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`**  User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]   
**`--profile <value>`**  Selects a config profile to use [$CB_PROFILE]   
**`--output <value>`**  Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]  

**Examples**

Lists regions available on the AWS account identified by the credential called "aws-cred":

<pre>cb cloud regions --credential aws-cred
[
  {
    "Name": "ap-northeast-1",
    "Description": "Asia Pacific (Tokyo)"
  },
  {
    "Name": "ap-northeast-2",
    "Description": "Asia Pacific (Seoul)"
  },
  ...</pre>





__________________________________     

#### cloud volumes

Lists the available volume types. 

**Sub-commands**

**`aws`**     Lists the available aws volume types  
**`azure`**   Lists the available azure volume types  
**`gcp`**     Lists the available gcp volume types  

**Required Options**

None
   
**Options**

**`--server <value>`**  Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`**  User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]   
**`--profile <value>`**  Selects a config profile to use [$CB_PROFILE]   
**`--output <value>`**  Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]  

**Examples**

Lists volumes available on AWS:

<pre>cb cloud volumes aws
[
  {
    "Name": "ephemeral",
    "Description": "Ephemeral"
  },
  {
    "Name": "gp2",
    "Description": "General Purpose (SSD)"
  },
  {
    "Name": "st1",
    "Description": "Throughput Optimized HDD"
  },
  {
    "Name": "standard",
    "Description": "Magnetic"
  }
]</pre>





  
__________________________________ 

#### cloud instances 
 
Lists the available instance types.

**Required Options**

**`--credential <value>`**  Name of the credential  
**`--region <value>`**   Name of the region  
  

**Options**

**`--server <value>`**  	Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`**  	User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** 	Password [$CB_PASSWORD]   
**`--profile <value>`**  	Selects a config profile to use [$CB_PROFILE]   
**`--availability-zone <value>`**  Name of the availability zone   
**`--output <value>`**  	Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT] 

**Examples**

Lists instance types available in the us-west-2 (Oregon) region on the AWS account identified by the credential called "aws-cred":

<pre>cb cloud instances --credential aws-cred --region us-west-2

  {
    "Name": "c3.2xlarge",
    "Cpu": "8",
    "Memory": "15.0",
    "AvailabilityZone": "us-west-2b"
  },
  {
    "Name": "c3.4xlarge",
    "Cpu": "16",
    "Memory": "30.0",
    "AvailabilityZone": "us-west-2b"
  },
  ...</pre>






__________________________________

#### cluster change-ambari-password

Changes Ambari password.

**Required Options**

**`--name <value>`**  Cluster name  
**`--old-password <value>`** Old Ambari password   
**`--new-password <value>`**  New Ambari password    
**`--ambari-user`**  Ambari user   

**Options**

**`--server <value>`**  Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`**  User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]  
**`--profile <value>`**  Selects a config profile to use [$CB_PROFILE]  
**`--output <value>`**  Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]

**Examples**

Changes password for Ambari user called "admin" for a cluster called "test1234":

<pre>cb cluster change-ambari-password --name test1234 --old-password 123456 --new-password Ambari123456 --ambari-user admin</pre>








__________________________________

#### cluster create 

Creates a new cluster based on a JSON template.

**Required Options**

**`--name <value>`**  Name for the cluster  
**`--cli-input-json <value>`**  User provided file in JSON format  

**Options**

**`--description <value>`**  Description of resource   
**`--public`**  Public in account   
**`--input-json-param-password <value>`**  Password for the cluster and Ambari   
**`--wait`**  Wait for the operation to finish. No argument is required   
**`--server <value>`**   Server address   [$CB_SERVER_ADDRESS]   
**`--username <value>`**  User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`**  Password [$CB_PASSWORD]  
**`--profile <value>`**  Selects a config profile to use [$CB_PROFILE]  

**Examples**

Creates a cluster called "testcluster" based on a local JSON file called "mytemplate.json" located in the /Users/test/Documents directory:   

<pre>cb cluster create --name testcluster --cli-input-json /Users/test/Documents/mytemplate.json</pre>


**Related Commands**

[cluster generate-template](#cluster-generate-template) 








__________________________________

#### cluster delete

Deletes an existing cluster. 

**Required Options**

**`--name <value>`**  Cluster name

**Options**

**`--force`**  Force the operation  
**`--wait`**  Wait for the operation to finish. No argument is required  
**`--server <value>`**  Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`**  User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]  
**`--profile <value>`**  Selects a config profile to use [$CB_PROFILE]   

**Examples**

<pre>cb cluster delete --name test1234</pre>

**Related Commands**

[cluster list](#cluster-list)









__________________________________

#### cluster describe 

Describes an existing cluster.

**Required Options**

**`--name <value>`**  Cluster name

**Options**

**`--server <value>`**  Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`**  User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`**  Password [$CB_PASSWORD]  
**`--profile <value>`**  Selects a config profile to use [$CB_PROFILE]  
**`--output <value>`**  Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]  

**Examples**

Returns a JSON file describing an existing cluster called "test1234":

<pre>./cb cluster describe --name test1234</pre>

The command returns JSON output which due to space limitation was not captured in the example.

**Related Commands**

[cluster list](#cluster-list)









__________________________________

#### cluster generate-template

Generates a provider-specific cluster template in JSON format.

**Sub-commands**

**`aws new-network`** Generates an AWS cluster JSON template with new network  
**`aws existing-network`** Generates an AWS cluster JSON template with existing network  
**`aws existing-subnet`** Generates an AWS cluster JSON template with existing network and subnet  

**`azure new-network`** Generates an Azure cluster JSON template with new network  
**`azure existing-subnet`** Generates an Azure cluster JSON template with existing network and subnet  

**`gcp new-network`** Generates an GCP cluster JSON template with new network  
**`gcp existing-network`** Generates an GCP cluster JSON template with existing network   
**`gcp existing-subnet`** Generates an GCP cluster JSON template with existing network and subnet  
**`gcp legacy-network`** Generates an GCP cluster JSON template with legacy network without subnets    
 
**`openstack new-network`** Generates an OS cluster JSON template with new network   
**`openstack existing-network`** Generates an OS cluster JSON template with existing network   
**`openstack existing-subnet`** Generates an OS cluster JSON template with existing network and subnet   

**Examples**

<pre>cb cluster generate-template aws new-network</pre>

**Related Commands**

[cluster create](#cluster-create) 






__________________________________

#### cluster generate-reinstall-template

Generates a cluster template that you can use to reinstall the cluster if installation went fail. 



**Required Options**

**`--blueprint-name <value>`**  Name of the blueprint 


**Options**

**`--server <value>`**  Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`**  User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]  
**`--profile <value>`**  Selects a config profile to use [$CB_PROFILE]  
**`--output <value>`**  Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]

**Examples**

<pre>cb cluster generate-reinstall-template --blueprint-name "EDW-ETL: Apache Hive 1.2.1, Apache Spark 2.1"</pre>






__________________________________

#### cluster list

Lists all clusters which are currently associated with the Cloudbreak instance.

**Required Options**

None

**Options**

**`--server <value>`**  Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`**  User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]  
**`--profile <value>`**  Selects a config profile to use [$CB_PROFILE]  
**`--output <value>`**  Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]

**Examples**

Lists available clusters: 

<pre>cb cluster list
[
  {
    "Name": "test1234",
    "Description": "",
    "CloudPlatform": "AZURE",
    "StackStatus": "UPDATE_IN_PROGRESS",
    "ClusterStatus": "REQUESTED"
  }
]</pre>

Lists available clusters, with output in a table format:

<pre>cb cluster list --output table
+----------+-------------+---------------+--------------------+---------------+
|   NAME   | DESCRIPTION | CLOUDPLATFORM |    STACKSTATUS     | CLUSTERSTATUS |
+----------+-------------+---------------+--------------------+---------------+
| test1234 |             | AZURE         | UPDATE_IN_PROGRESS | REQUESTED     |
+----------+-------------+---------------+--------------------+---------------+</pre>

**Related Commands**

[cluster list](#cluster-list)










__________________________________

#### cluster repair

Repairs a cluster if cluster installation failed.

**Required Options**

**`--name <value>`**  Cluster name

**Options**

**`--wait`**  Wait for the operation to finish. No argument is required  
**`--server <value>`**  Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`**  User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]  
**`--profile <value>`**  Selects a config profile to use [$CB_PROFILE]  
**`--output <value>`**  Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]

**Examples**

<pre>cb cluster repair --name test1234</pre>

**Related Commands**

[cluster list](#cluster-list)







__________________________________

#### cluster scale

Scales a cluster by adding or removing nodes.

**Required Options**

**`--name <value>`**  Name of the cluster
**`--group-name <value>`**  Name of the group to scale
**`--desired-node-count <value>`**  Desired number of nodes

**Options**

**`--wait`**  Wait for the operation to finish. No argument is required  
**`--server <value>`**  Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`**  User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]  
**`--profile <value>`**  Selects a config profile to use [$CB_PROFILE]  
**`--output <value>`**  Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]  

**Examples**

<pre>cb cluster scale --name test1234 --group-name worker --desired node-count 3</pre>

**Related Commands**

[cluster list](#cluster-list)




__________________________________

#### cluster start

Starts a cluster which has previously been stopped.

**Required Options**

**`--name <value>`**  Cluster name

**Options**

**`--wait`**  Wait for the operation to finish. No argument is required  
**`--server <value>`**  Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`**  User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]  
**`--profile <value>`**  Selects a config profile to use [$CB_PROFILE]  
**`--output <value>`**  Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]

**Examples**

<pre>cb cluster start --name test1234</pre>

**Related Commands**

[cluster list](#cluster-list)




__________________________________

#### cluster stop

Stops a cluster.

**Required Options**

**`--name <value>`**  Cluster name

**Options**

**`--wait`**  Wait for the operation to finish. No argument is required  
**`--server <value>`**  Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`**  User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]  
**`--profile <value>`**  Selects a config profile to use [$CB_PROFILE]  
**`--output <value>`**  Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]

**Examples**

<pre>cb cluster stop --name test1234</pre>

**Related Commands**

[cluster list](#cluster-list)





__________________________________

#### cluster sync

Synchronizes a cluster with the cloud provider.

**Required Options**

**`--name <value>`**  Cluster name

**Options**

**`--server <value>`**  Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`**  User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]  
**`--profile <value>`**  Selects a config profile to use [$CB_PROFILE]  
**`--output <value>`**  Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]


**Examples**

<pre>cb cluster sync --name test1234</pre>








__________________________________

#### configure

Configures the Cloudbreak server address and credentials used to communicate with this server.

**Required Options**

**`--server value`**  Server address [$CB_SERVER_ADDRESS]  
**`--username value`**	 User name (e-mail address) [$CB_USER_NAME]  

**Options**

**`--password value`**  Password [$CB_PASSWORD]  
**`--profile value`**  Select a config profile to use [$CB_PROFILE]   
**`--output value`**  Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]  

**Examples**

This example configures the server address with username and password:

<pre>cb configure --server https://ec2-11-111-111-11.compute-1.amazonaws.com --username admin@hortonworks.com --password MySecurePassword123</pre>

This example configures the server address with username but without a password:

<pre>cb configure --server https://ec2-11-111-111-11.compute-1.amazonaws.com --username admin@hortonworks.com</pre>


**Related Links**

[Configure CLI](cli-install.md#configure-the-cli)






__________________________________

#### credential create 

Creates a new Cloudbreak credential.

**Sub-commands**

**`aws role-based`**  Creates a new AWS credential  
**`aws key-based`**  Creates a new AWS credential  
**`azure app-based`** Creates a new app-based Azure credential  
**`gcp`** Creates a new gcp credential  
**`openstack keystone-v2`** Creates a new OpenStack credential  
**`openstack keystone-v3`** Creates a new OpenStack credential 

**Required Options**

**`aws role-based`** 

**`--name <value>`**  Credential name  
**`--role-arn <value>`** IAM Role ARN of the role used for Cloudbreak credential  

**`aws key-based`** 

**`--name <value>`**  Credential name  
**`--access-key <value>`**  AWS Access Key  
**`--secret-key <value>`**  AWS Secret Key  

**`azure app-based`** 

**`--name <value>`**  Credential name  
**`--subscription-id <value>`**  Subscription ID from your Azure Subscriptions  
**`--tenant-id <value>`**  Directory ID from your Azure Active Directory > Properties      
**`--app-id <value>`**  Application ID of your app from your Azure Active Directory > App Registrations            
**`--app-password <value>`**  Your application key from app registration's Settings > Keys  

**`gcp`** 

**`--name <value>`**  Credential name   
**`--project-id <value>`**  Project ID from your GCP account                        
**`--service-account-id <value>`**  Your GCP Service account ID from IAM & Admin > Service accounts                 
**`--service-account-private-key-file <value>`**  P12 key from your GCP service account  

**`openstack keystone-v2`**  

**`--name <value>`**  Credential name  
**`--tenant-user <value>`**  OpenStack user name     
**`--tenant-password <value>`**  OpenStack password  
**`--tenant-name <value>`**  OpenStack tenant name      
**`--endpoint <value>`**   OpenStack endpoint   

**`openstack keystone-v3`** 

**`--name <value>`**  Credential name  
**`--tenant-user <value>`**  OpenStack user name     
**`--tenant-password <value>`**  OpenStack password  
**`--user-domain <value>`**  OpenStack user domain      
**`--endpoint <value>`**   OpenStack endpoint  


**Options**

**`--description <value>`**  Description of the resource  
**`--public`**  Public in account  
**`--server <value>`** Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`** User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]  
**`--profile <value>`** Selects a config profile to use [$CB_PROFILE]  

Additionally, the following option is available for OpenStack Keystone2 and Keystone3:

**`--facing <value>`** API facing. One of: public, admin, internal

Additionally, the following option is available for OpenStack Keystone3:

**`--keystone-scope <value>`** OpenStack keystone scope. One of: default, domain, project 


**Examples**

Creates a role-based credential on AWS:

<pre>cb credential create aws role-based --name my-credential1 --role-arn arn:aws:iam::517127065441:role/CredentialRole</pre>

Creates a key-based credential on AWS:

<pre>cb credential create aws key-based --name my-credential2 --access-key ABDVIRDFV3K4HLJ45SKA --secret-key D89L5pOPM+426Rtj3curKzJEJL3lYoNcP8GvguBV</pre>

Creates an app-based credential on Azure:

<pre>cb credential create azure app-based --name my-credential3 --subscription-id b8e7379e-568g-55d3-na82-45b8d421e998 --tenant-id  c79n5399-3231-65ba-8dgg-2g4e2a40085e --app-id 6d147d89-48d2-5de2-eef8-b89775bbfcg1 --app-password 4a8hBgfI52s/C8R5Sea2YHGnBFrD3fRONfdG8w7F2Ua=</pre>

Creates a credential on Google Cloud:

<pre>cb credential create gcp --name my-credential4 --project-id test-proj --service-account-id test@test-proj.iam.gserviceaccount.com --service-account-private-key-file /Users/test/3fff57a6f68e.p12</pre>


Creates a role-based credential on OpenStack with Keystone-v2:

<pre>cb credential create openstack keystone-v2 --name my-credential5 --tenant-user test --tenant-password MySecurePass123 --tenant-name test --endpoint http://openstack.test.organization.com:5000/v2.0</pre>


**Related Links**

[Create Credential on AWS](aws-launch.md#create-credential)  
[Create Credential on Azure](azure-launch.md#create-credential)  
[Create Credential on GCP](gcp-launch.md#create-credential)  
[Create Credential on OpenStack](os-launch.md#create-credential)  







__________________________________

#### credential delete

Deletes an existing Cloudbreak credential.

**Required Options**

**`--name <value<`**  Name of the credential 

**Options**

**`--server <value>`** Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`** User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]  
**`--profile <value>`** Selects a config profile to use [$CB_PROFILE] 

**Examples**

<pre>cb credential delete --name test-cred</pre>

**Related Commands**

[credential list](#credential-list)





__________________________________

#### credential describe

Describes an existing credential.

**Required Options**

**`--name <value>`**  Name of the credential 

**Options**
  
**`--server <value>`** Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`** User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]  
**`--profile <value>`** Selects a config profile to use [$CB_PROFILE]  
**`--output <value>`**  Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]

**Examples**

<pre>cb credential describe --name testcred
{
  "Name": "testcred",
  "Description": "",
  "CloudPlatform": "AZURE"
}</pre>

**Related Commands**

[credential list](#credential-list)







__________________________________

#### credential list

Lists existing Cloudbreak credentials.

**Required Options**

None

**Options**

**`--server <value>`** Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`** User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`** Password [$CB_PASSWORD]  
**`--profile <value>`** Selects a config profile to use [$CB_PROFILE]  
**`--output <value>`**  Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]

**Examples**

Lists credentials:

<pre>cb credential list 
[
  {
    "Name": "testcred",
    "Description": "",
    "CloudPlatform": "AZURE"
  }
]
</pre>

Lists credentials, with output formatted in a table format:

<pre>cb credential list --output table
+---------+-------------+---------------+
|  NAME   | DESCRIPTION | CLOUDPLATFORM |
+---------+-------------+---------------+
| armcred |             | AZURE         |
+---------+-------------+---------------+</pre>

**Related Commands**

[credential describe](#credential-describe)








__________________________________

#### recipe create

Adds a new recipe from a file or from a URL.

**Sub-commands**

**`from-url`**  Creates a recipe by downloading it from a URL location  
**`from-file`**  Creates a recipe by reading it from a local file  

**Required Options**

**`from-url`**  

**`--name <value>`**  Name for the recipe   
**`--execution-type <value>`**  Type of execution [pre, post]  
**`--url <value>`**  URL location of the Ambari blueprint JSON file  

  
**`from-file`** 

**`--name <value>`**  Name for the recipe  
**`--execution-type <value>`**  Type of execution [pre, post]  
**`--file <value>`**  Location of the Ambari blueprint JSON file  

**Options**

**`--description <value>`**  Description for the recipe   
**`--public`**   Public in account  
**`--server <value>`**  Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`**  User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`**  Password [$CB_PASSWORD]  
**`--profile <value>`**  Selects a config profile to use [$CB_PROFILE]  

**Examples**


Adds a new recipe called "test1" from a URL:

<pre>cb recipe create from-url --name "test1" --execution post --url http://some-site.com/test.sh</pre>

Adds a new recipe called "test2" from a file:

<pre>cb recipe create from-url --name "test2" --execution post --file /Users/test/Documents/test.sh</pre>

**Related Links**

[Recipes](recipes.md)







__________________________________
 
#### recipe delete

Deletes an existing recipe.

**Required Options**

**`--name <value>`**  Name for the recipe  

**Options**

**`--server <value>`**  Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`**  User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`**  Password [$CB_PASSWORD]  
**`--profile <value>`**  Selects a config profile to use [$CB_PROFILE]  
**`--output <value>`**  Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]

**Examples**

<pre>cb recipe delete --name test</pre>

**Related Commands**

[recipe list](#recipe-list)








__________________________________

#### recipe describe

Describes an existing recipe.

**Required Options**

**`--name <value>`**  Name for the recipe    

**Options**

**`--server <value>`**  Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`**  User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`**  Password [$CB_PASSWORD]  
**`--profile <value>`**  Selects a config profile to use [$CB_PROFILE]  
**`--output <value>`**  Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]


**Examples**

Describes a recipe called "test":

<pre>cb recipe describe --name test
{
  "Name": "test",
  "Description": "",
  "ExecutionType": "POST"
}</pre>

Describes a recipe called "test", with output presented in a table format:

<pre>cb describe-recipe --name test --output table
+------+-------------+----------------+
| NAME | DESCRIPTION | EXECUTION TYPE |
+------+-------------+----------------+
| test |             | POST           |
+------+-------------+----------------+</pre>

**Related Commands**

[recipe list](#recipe-list)









__________________________________

#### recipe list

Lists all available recipes.

**Required Options**

None

**Options**

**`--server <value>`**  Server address [$CB_SERVER_ADDRESS]  
**`--username <value>`**  User name (e-mail address) [$CB_USER_NAME]  
**`--password <value>`**  Password [$CB_PASSWORD]  
**`--profile <value>`**  Selects a config profile to use [$CB_PROFILE]  
**`--output <value>`**  Supported formats: json, yaml, table (default: "json") [$CB_OUT_FORMAT]

**Examples**

Lists existing recipes:

<pre>cb recipe list
[
  {
    "Name": "test",
    "Description": "",
    "ExecutionType": "POST"
  }
]</pre>

Lists existing recipes, with output presented in a table format:

<pre>cb recipe list --output table
+------+-------------+----------------+
| NAME | DESCRIPTION | EXECUTION TYPE |
+------+-------------+----------------+
| test |             | POST           |
+------+-------------+----------------+
</pre>

**Related Commands**

[recipe describe](#recipe-describe)





__________________________________

### Debugging

To use debugging mode, pass the `--debug` option. 


### Checking CLI Version

To check CLI version, use `cb --version`.






