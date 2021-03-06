## Configuring access to ADLS  

Hortonworks Data Platform (HDP) supports reading and writing block blobs and page blobs from and to *Windows Azure Storage Blob (WASB)* object store, as well as reading and writing files stored in an *Azure Data Lake Storage (ADLS)* account. 

[Azure Data Lake Store (ADLS)](https://azure.microsoft.com/en-in/services/data-lake-store/) is an enterprise-wide hyper-scale repository for big data analytic workloads. ADLS is not supported as a default file system, but access to data in ADLS is possible via the adl connector. 

These steps assume that you are using an HDP version that supports the adl cloud storage connector (HDP 2.6.1 or newer).  


#### Prerequisites

If you would like to use ADLS to store your data, you must enable Azure subscription for Data Lake Store, and then create an Azure Data Lake Store [storage account](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-portal).


#### Configure access to ADLS 

To configure authentication with ADLS using the client credential, you must register a new application with Active Directory service and then give your application access to your ADL account. After you've performed these steps, you can provide your application's information when creating a cluster. 

**Steps**

1. Register an application and add it to the ADLS account, as described in *Step 1* and *Step 2* of [How to configure authentication with ADLS](https://community.hortonworks.com/articles/105994/how-to-configure-authentication-with-adls.html). 

    > Do not perform the *Step 3* described in this article. Cloudbreak automates this step.  
    
2. In Cloudbreak web UI, on the advanced **Cloud Storage** page of the create a cluster wizard, select **Use existing ADLS storage**.

3. Provide the following parameters for your registered application:    

    * **ADLS Account Name**: This is the ADL account that your application was assigned to.    
    * **Application ID**: You can find it in your application's settings. 
    * **Key**: This is the key that you generated for your application. If you did not copy the it, you must create a new key from the Keys page in your application's settings.   

Once your cluster is in the running state, you will be able to access the Azure blob storage account from the cluster nodes. 


#### Test access to ADLS

To tests access to ADLS, SSH to a cluster node and run a few hadoop fs shell commands against your existing ADLS account.

ADLS access path syntax is:

<pre>adl://<b>account_name</b>.azuredatalakestore.net/<b>dir/file</b></pre>

For example, the following Hadoop FileSystem shell commands demonstrate access to a storage account named "myaccount":

<pre>hadoop fs -mkdir adl://myaccount.azuredatalakestore.net/testdir</pre>

<pre>hadoop fs -put testfile adl://myaccount.azuredatalakestore.net/testdir/testfile</pre>

To use DistCp against ADLS, use the following syntax:
<pre>hadoop distcp
    [-D hadoop.security.credential.provider.path=localjceks://file/home/user/adls.jceks]
    hdfs://<b>namenode_hostname</b>:9001/user/foo/007020615
    adl://<b>myaccount</b>.azuredatalakestore.net/testDir/</pre>
    

For more information about configuring the ADLS connector and working with data stored in ADLS, refer to [Cloud Data Access](https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.5/bk_cloud-data-access/content/about.html) documentation.

**Related links**   
[Cloud Data Access](https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.2/bk_cloud-data-access/content/about.html) (Hortonworks)  
[How to configure authentication with ADLS](https://community.hortonworks.com/articles/105994/how-to-configure-authentication-with-adls.html) (Hortonworks)  
[Azure Data Lake Store](https://azure.microsoft.com/en-in/services/data-lake-store/) (External)     
[Create a storage account](https://docs.microsoft.com/en-us/azure/storage/common/storage-create-storage-account#create-a-storage-account) (External)     
[Get started with Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-portal) (External)  


#### Configure ADLS storage locations

After configuring access to ADLS, you can optionally use that ADLS storage account as a base storage location; this storage location is mainly for the Hive Warehouse Directory (used for storing the table data for managed tables).   

**Steps**

1. When creating a cluster, on the **Cloud Storage** page in the advanced cluster wizard view, select **Use existing ADLS storage** and select the instance profile to use, as described in [Configure access to ADLS](#configure-access-to-adls).    
2. Under **Storage Locations**, enable **Configure Storage Locations** by clicking the <img src="../images/cb_toggle.png" alt="On"/> button.   
3. Provide your existing directory name under **Base Storage Location**. 

    > Make sure that the directory exists within the account.
    
[Comment]: <> (Is this correct that this needs to be a directory name and that it needs to exist already?)    
    
4. Under **Path for Hive Warehouse Directory property (hive.metastore.warehouse.dir)**, Cloudbreak automatically suggests a location within the bucket. For example, if the directory that you specified is `my-test-dir` then the suggested location will be `my-test-adls-account.azuredatalakestore.net/my-test-dir/apps/hive/warehouse`. You may optionally update this path.        

    Cloudbreak automatically creates this directory structure in your bucket.  
    

<div class="next">
<a href="../azure-data-wasb/index.html">Next: Configure Access to WASB</a>
</div>