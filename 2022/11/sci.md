
### SCI Cluster
The new computing cluster of UMass Medical School is called Scientific Computing for Innovation Cluster or SCI Cluster. There is a detailed [Wiki](https://hpc.umassmed.edu) that all users are encouraged to read through. There are many differences compared to the old cluster (GHPCC).
#### Obtaining an account
SCI Cluster accounts are managed via the [HPC Portal](https://hpcportal.umassmed.edu). You will use your UMass username, typically lastnameFirstInitial and the password for your UMass accounts. Each user will need to apply for an account using the portal. Please follow the HPC wiki [section 2.1](https://hpc.umassmed.edu/wiki/index.php?title=Welcome_to_the_Scientific_Computing_for_Innovation_Cluster#Requesting_an_Account) for requesting an account. PIs will need to approve their group members' account requests. So essentially this is an automated process and there should be no need for help from the HPC admins.
#### Logging into the SCI cluster
SCI cluster will only work with SSH key pairs and will not allow password authentication. Please follow the HPC wiki [section 2.2](https://hpc.umassmed.edu/wiki/index.php?title=Welcome_to_the_Scientific_Computing_for_Innovation_Cluster#Authentication) to learn how to create a SSH key pair and how to send your public key to the SCI cluster. Once you successfully add your public key on the HPC portal, you will be able to log in to the new cluster using your favorite terminal software. Please note that both the host name of the new cluster (hpc.umassmed.edu) and user names (typically name.lastname-umw) are different from the old cluster. 
#### Data transfer from old cluster to the new cluster
[Section 4](https://hpc.umassmed.edu/wiki/index.php?title=Welcome_to_the_Scientific_Computing_for_Innovation_Cluster#Transferring_Data_to_SCI) of the wiki covers different ways to transfer data from the old cluster to the new. My preferred software is `rsync`  

Follow the instructions below to use `rsync` to transfer your data:  
  1) Find the path of the data you want to copy from the old cluster. For example, user Jane from John Doe's labe has two folders to transfer; one in the project space: `/project/umw_john_doe/jane/project_data` and the other in nearline: `/nl/umw_john_doe/nearline_data`
  2) Decide where you want to copy it on the new cluster. For example, `/pi/john.doe-umw/jane/project_data` and `/pi/john.doe-umw/jane/nearline_data`. Note that the storage is mounted differently in each cluster. The new cluster does not have `/project` and `/nl`; there is only `/pi` space instead.
