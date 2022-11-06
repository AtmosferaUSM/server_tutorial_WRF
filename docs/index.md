
<!--- 

[atmosfera website](https://atmosfera.usm.my/)

**Bold Text** 

> following points:
- list
- list

{--deleted--}
{++added++}
{~~one~>a single~~}
{==Highlighting==}
{>>and comments can be added inline<<}
---> 

# Create Cluster

We have to create a computer cluster on AWS to install and run WRF. The links to AWS and PCluster Managers are below. Go to the PCluster link to create the cluster after having a account on AWS.

* Link to AWS
* Link to PCluster Manager
* Create Cluster

![Alt Text](images/Create cluster/1.png)

## **Upload YML file**

```
HeadNode:
  InstanceType: c5a.xlarge
  Ssh:
    KeyName: PClusterManager
  Networking:
    SubnetId: subnet-0412e7315562aa1da
  LocalStorage:
    RootVolume:
      VolumeType: gp3
      Size: 50
  Iam:
    AdditionalIamPolicies:
      - Policy: arn:aws:iam::aws:policy/AmazonSSMManagedInstanceCore
      - Policy: arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess
  Dcv:
    Enabled: true
Scheduling:
  Scheduler: slurm
  SlurmQueues:
    - Name: queue0
      ComputeResources:
        - Name: queue0-hpc6a48xlarge
          MinCount: 0
          MaxCount: 10
          InstanceType: hpc6a.48xlarge
          Efa:
            Enabled: true
            GdrSupport: true
          DisableSimultaneousMultithreading: true
      Networking:
        SubnetIds:
          - subnet-01a39ae1f7194644a
        PlacementGroup:
          Enabled: true
      ComputeSettings:
        LocalStorage:
          RootVolume:
            VolumeType: gp3
            Size: 50
      Iam:
        AdditionalIamPolicies:
          - Policy: arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess
Region: us-east-2
Image:
  Os: alinux2
SharedStorage:
  - Name: Ebs0
    StorageType: Ebs
    MountDir: /shared
    EbsSettings:
      VolumeType: gp3
      DeletionPolicy: Delete
      Size: '200'
      Encrypted: false
```

## **Create Cluster**

![Alt Text](images/Create cluster/2.png)

* Dry Run

{==Request would have succeeded, but DryRun flag is set.==}

    Request would have succeeded, but DryRun flag is set.

* Create

## **Create in Progress**

![Alt Text](images/Create cluster/5.png)

## **Create Complete**
 
![Alt Text](images/Create cluster/7.png)

* Click on Shell
* Login to your AWS account 
