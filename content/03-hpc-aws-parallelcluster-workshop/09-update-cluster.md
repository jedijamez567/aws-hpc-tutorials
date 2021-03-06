+++
title = "h. Update your cluster"
date = 2019-09-18T10:46:30-04:00
weight = 100
tags = ["tutorial", "create", "ParallelCluster"]
+++

We have sucessfully built your cluster and ran your first MPI job.

Let's say you want to change your instance type to a different instance type in your compute fleet for example **c4.large** . In this lab, we will learn how to update your cluster with new instance type.


Go back to your AWS Cloud9 environment, and stop the cluster

```bash
pcluster list
```

```bash
pcluster stop hpclab-yourname
```

Edit your original config file and change `instance_type = c4.large`

```bash
vi my-cluster-config.ini 
```

```bash
[compute_resource default]
instance_type = c4.large
min_count = 0
max_count = 8
```

Then run a **pcluster update** command

```bash
pcluster update hpclab-yourname -c my-cluster-config.ini
```

Pay attention to the **old value** and **new value** fields. You will see a new instance type under new value field. The output will be similar to this. 


![ParallelCluster Update](/images/hpc-aws-parallelcluster-workshop/pc-update.png)


Start your cluster again after update process is completed.

```bash
pcluster start hpclab-yourname
```

You can now login to your cluster and run your helloworld job again

you can see that the cluster compute node has changed to c4.large

```bash
[ec2-user@ip-172-31-39-157 ~]$ sinfo
PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST 
compute*     up   infinite      8  idle~ compute-dy-c4large-[1-8] 
```

Now you have a better understanding on how AWS ParallelCluster operates. For more information, see the [Configuration](https://docs.aws.amazon.com/parallelcluster/latest/ug/configuration.html) section of the *AWS ParallelCluster User Guide*.
