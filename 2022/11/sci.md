
### SCI Cluster
The new computing cluster of UMass Medical School is called Scientific Computing for Innovation Cluster or SCI Cluster. There is a detailed [Wiki](https://hpc.umassmed.edu) that all users should to read through. There are many differences compared to the old cluster (GHPCC) and it is important to get familiar with the new environment. Please make sure that you are clicking the __Expand__ buttons on the right side of different sections to reveal the important information contained within the sections.
#### Obtaining an account
SCI Cluster accounts are managed via the [HPC Portal](https://hpcportal.umassmed.edu). You will use your UMass username, typically lastnameFirstInitial and the password for your UMass accounts. Each user will need to apply for an account using the portal. Please follow the HPC wiki [section 2.1](https://hpc.umassmed.edu/wiki/index.php?title=Welcome_to_the_Scientific_Computing_for_Innovation_Cluster#Requesting_an_Account) (remember to __expand__ the section) for requesting an account. Principal investigators will need to approve their group members' account requests using the same portal. So essentially this is an automated process and there should be no need for help from the HPC admins.
#### Logging into the SCI cluster
SCI cluster will only work with SSH key pairs and will not allow password authentication. Please follow the HPC wiki [section 2.2](https://hpc.umassmed.edu/wiki/index.php?title=Welcome_to_the_Scientific_Computing_for_Innovation_Cluster#Authentication) to learn how to create a SSH key pair and how to send your public key to the SCI cluster. Once you successfully add your public key on the HPC portal, you will be able to log in to the new cluster using your favorite terminal software. Please note that both the host name of the new cluster (hpc.umassmed.edu) and user names (typically name.lastname-umw) are different from the old cluster. 
#### Data transfer from old cluster to the new cluster
[Section 4](https://hpc.umassmed.edu/wiki/index.php?title=Welcome_to_the_Scientific_Computing_for_Innovation_Cluster#Transferring_Data_to_SCI) of the wiki covers different ways to transfer data from the old cluster to the new. My preferred software is `rsync`. The usage of `rsync` is as follows:
```bash
rsync --options target_address destination_address
```

Follow the instructions below to use `rsync` to transfer your data. Please note that rsync will overwrite files if they already exist in the destination address.  
  1) Find the path of the data you want to copy from the old cluster (target address). For example, user Jane from John Doe's lab has two folders to transfer; one in the project space: `/project/umw_john_doe/jane/data` and the other in nearline: `/nl/umw_john_doe/data`
  2) Open your terminal software and connect to the new cluster. You will carry out rest of the commands on the new cluster using this connection:

        ```bash
        ssh jane.doe-umw@hpc.umassmed.edu
        ``` 
  4) Decide where you want to copy your files on the new cluster (destination address). For example, `/pi/john.doe-umw/jane/project_data` and `/pi/john.doe-umw/jane/nearline_data`. Note that the storage is mounted differently in the new cluster. The new cluster does not have `/project` and `/nl`; there is only `/pi` space instead.
  5) If the destination directories do not exist, you need to create them. One exception is the final directories in the destination paths, which can be created by rsync. For this example, `/pi/john.doe-umw/jane/` must exist but it is fine if `project_data` and `nearline_data` does not exist. So if `/pi/john.doe-umw/jane/` does not exist, create it with: 

        ```bash
        mkdir /pi/john.doe-umw/jane/
        ```

  7) Start the transfer for the project space data with the command below assuming that the user name for Jane in the __old cluster__ is jd12w:

        ```bash
        rsync -avzP jd12w@ghpcc08.umassrc.org:/project/umw_john_doe/jane/data/ /pi/john.doe-umw/jane/project_data
        ```
  
 An important concept in rsync usage is the trailing slash in the target address. In the above example, there is a forward slash (`/`) at the end of the target address: `jd12w@ghpcc08.umassrc.org:/project/umw_john_doe/jane/data/` When present, the trailing slash indicates that we want to copy the contents of this directory to the destination address, and not the directory itself. In the example command above, if the target directory contained a single file: `file.txt`, i.e. `/project/umw_john_doe/jane/data/file.txt`, after the rsync transfer we will end up with `/pi/john.doe-umw/jane/project_data/file.txt` in the destination. 
  
However, if we did not use the trailing slash in the target address:

```bash
rsync -avzP jd12w@ghpcc08.umassrc.org:/project/umw_john_doe/jane/data /pi/john.doe-umw/jane/project_data
```

we would copy the data directory with its contents and end up with `/pi/john.doe-umw/jane/project_data/data/file.txt`
  
  6) You will get a summary when the transfer finishes including whether there were any errors. If you notice any errors you can run the same rsync command and retry your transfer. Any files that have already been transferred successfully will not be transferred again, so it should be a quick run the second time around.
  7) Start the transfer of the nearline data

        ```bash
        rsync -avzP jd12w@ghpcc08.umassrc.org:/nl/umw_john_doe/jane/data/ /pi/john.doe-umw/jane/nearline_data
        ```
    

  

