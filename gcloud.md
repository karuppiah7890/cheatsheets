# gcloud

This is my cheatsheet for anything related to `gcloud`

* How do I login to run gcloud commands to interact with GCP APIs as me?

```
$ gcloud auth login
```

It will open up your browser, then you can login to your google account that you
use for your GCP projects and then that's it! :) It's an interactive and easy
login

* How do I check the account that I'm currently using?

```
$ gcloud auth list
```

* How do I activate a service account using a key.json file?

```
$ gcloud auth activate-service-account --key-file <key-json-file-path>
```

* How do I check my current default config?

```
$ gcloud config list
```

* How do I check the list of projects that I have access to?

```
$ gcloud projects list
```

* How to limit the number of items / results when doing a list operation?

By default usually all list operations give complete or full results, meaning - there is
no limit to the size of the list. If there are 1000 items, all thousand are
shown.

If you want to limit the results - usually there's a `--limit` flag which you
can use to limit the results. Below is an example

```
$ gcloud projects list --limit 5
```

* How do I change the output format of the gcloud's output?

You can use the `--format` flag in the command. Possible values are `yaml`,
`json` and there are more! Like - `config`, `csv`, `default`, `diff`, `disable`,
`flattened`, `get`, `list`, `multi`, `none`, `object`, `table`, `text`, `value`.

```
$ gcloud auth list --format json
```

This would be pretty useful for programmatic access. To read more on the other
formats and how to use them, use

```
$ gcloud topic formats
```

* How do I mention / override the GCP project on a per command basis?

You can use the `--project` flag like this

```
$ gcloud --project <gcp-project-id> compute instances list
```

* How do I connect to my kubernetes cluster?

To connect to a kubernetes cluster, you will need a kubernetes config file which
has details on how to connect to the kubernetes API server. You can use the
below command to obtain your kubernetes config file! Depending on if it's a
zonal or regional cluster, you will need to specify `--zone` or `--region`
appropriately

The default kubernetes config file path is `$HOME/.kube/config`, if you want to
change it, set the `KUBECONFIG` environment variable

```
$ gcloud --project <gcp-project-id> container clusters get-credentials <gke-cluster-name> [--zone <zone-name> | --region <region-name>]
```

* How do I check / list the custom IAM roles in a project?

Usually GCP has some roles by default, like `viewer`, `editor`, `owner` and
more. You can also create custom IAM roles which you can list like this

```
$ gcloud --project <gcp-project-id> iam roles list
```

* How do I describe a custom IAM role?

```
$ gcloud --project <gcp-project-id> iam roles describe <role-name>
```

* How do I check the different GKE kubernetes clusters present in a GCP project?

```
$ gcloud --project <gcp-project-id> container clusters list
```

* How do I find the details about a GKE kubernetes cluster?

Depending on if it's a zonal or regional cluster, you will need to specify
`--zone` or `--region` appropriately

```
$ gcloud --project vn-gojek-production container clusters describe <gke-cluster-name> [--zone <zone-name> | --region <region-name>]
```

* How do I check the list of node pools present in a cluster? How do I check
a single node pool's details?

Using `describe`, you can check the `nodePools` field in it which gives a list
of node pools with each item having a lot of details (fields) like `name`,
`autoscaling` for auto-scaling related details, `podIpv4CidrSize` for pod IP v4
CIDR range, `config` for details like `machineType`

```
$ gcloud --project vn-gojek-production container clusters describe <gke-cluster-name> [--zone <zone-name> | --region <region-name>]
```

* How do I list the compute engine instances (VMs) in a project?

```
$ gcloud --project <gcp-project-id> compute instances list
```

* How to SSH into a machine?

For SSH key - Usually GCP takes care of creating a SSH key and adding it to the
VM. If that doesn't happen and if it doesn't work, do check about the ssh keys
and if it's present in the VM's ssh metadata or project ssh metadata and check
if your SSH public key is present in it.

If the VM is accessible through public IP that the VM has and the firewalls are
open to accept ssh connections at port 22, try the below.

```
$ gcloud --project <gcp-project-id> compute ssh [user@]<vm-name>
```

If the instance has a private IP and that's accessible (like, through a VPN),
then you can try the below.

```
$ gcloud --project <gcp-project-id> compute ssh [user@]<vm-name> --internal-ip
```

* How do I list the disks attached to a compute engine instance (VM)?

You will need `jq` for this

```
$ # find vm name first by listing VMs.
$ # to find all details about VM
$ gcloud --project <gcp-project-id> compute instances describe <vm-name>
$ # to find disks attached
$ gcloud --project <gcp-project-id> compute instances describe <vm-name> --json | jq '.disks'
```

* How do I check all the disks in a project?

This shows disk name and the zone it belongs to

```
$ gcloud --project <gcp-project-id> compute disks list
```

* How do I check the details about a disk?

```
$ gcloud --project <gcp-project-id> compute disks describe <disk-name> --zone <zone-name>
```

* How do I resize a disk attached to a VM?

```
$ gcloud --project <gcp-project-id> compute disks resize <disk-name> --size <new-disk-size> --zone <zone-name>
```

You also need to get into the VM that has this disk attached to it and run a command. To find the
VM having the disk use below command and check `users` field to know the node's link and hence
the name

```
$ gcloud --project <gcp-project-id> compute disks describe <disk-name> --zone <zone-name>
```

SSH into the VM and find the dev id at which the disk is mounted. It will look something like
this `/dev/sda`. To find the dev id run the below in the VM, replace `<disk-name>` with
the name of the disk!

```
$ readlink /dev/disk/by-id/google-<disk-name>
```

Now, run this in the VM

```
$ resize2fs <dev-id>
```

* How do I check the kubernetes cluster operations happening in a project's clusters?

This shows operations like updating cluster details, changing the size of the
node pools in the cluster, upgrading kubernetes master, upgrading node pools

```
$ gcloud --project <gcp-project-id> container operations list
```

* How do I describe a cluster operation using the operation ID?

```
$ gcloud --project <gcp-project-id> container operations describe <operation-id>
```

* How do I cancel a cluster operation using the operation ID?

As of this writing, the feature is still in `beta`. This is helpful when you
want to cancel any operation, for example to cancel an unexpected node pool
upgrade

```
$ gcloud --project <gcp-project-id> beta container operations cancel <operation-id>
```

* How do I find the different kinds / types of machines present in GCP?

```
$ gcloud compute machine-types list --limit 10
```

For the full list

```
$ gcloud compute machine-types list
```

* How to find configuration of a given machine type?

First use list to see all types (check above) and find the name of the machine
type you want to know about. If you don't specify zone in command, it will give a big list
of zones to choose from, in an interactive manner :)

```
$ gcloud compute machine-types describe <machine-type-name> --zone <zone-name>
```

* How to find the maximum number of disks that can be attached to a node? And
the maximum total size of all the disks attached to a node?

The `describe` command above gives these details in the fields
`maximumPersistentDisks` and `maximumPersistentDisksSizeGb`

```
$ gcloud compute machine-types describe <machine-type-name> --zone <zone-name>
```

* How to look for new features in the gcloud command?

Always keep the `gcloud` version updated. Usually `gcloud` gives information
about updates and the command to update the version is

```
$ gcloud components update
```

and check for new features - like new commands, by using the `alpha` and `beta`
features using `gcloud alpha` and `gcloud beta` :) Make sure you know what a
command does before you run it and check about the stability of it if possible
as these are alpha and beta features and there's a reason it's not in the
stable (without alpha, beta) yet! :)

* How to list all the service accounts in a project?

This gives the service account names and their email IDs
```
$ gcloud --project <gcp-project-id> iam service-accounts list
```

* How to describe a service account in a project?

```
$ gcloud --project <gcp-project-id> iam service-accounts describe <service-account-email-id>
```

* How to create a service account?

```
$ gcloud --project <gcp-project-id> iam service-accounts create <service-account-name> --display-name <aesthetic-display-name> --description <description-about-the-service-account>
```

* How to list all the keys for a service account?

This is lists the Key IDs and when the key was created at and when it expires
at.

```
$ gcloud --project <gcp-project-id> iam service-accounts keys list --iam-account <service-account-email-id>
```

* How to create and download the key.json / credentials file for a service
account?

```
$ gcloud --project <gcp-project-id> iam service-accounts keys create <path-to-download-key-json-file> --iam-account <service-account-email-id>
```

* How to create a role?

```
$ gcloud --project <gcp-project-id> iam roles create <role-name> --permissions <list-of-permissions>
```

You can get permission names from here https://cloud.google.com/iam/docs/permissions-reference

An example for the command is

```
$ gcloud --project some-project-id-01 iam roles create a-new-role --permissions compute.snapshots.create,compute.disks.createSnapshot,compute.disks.list,container.clusters.list,container.clusters.get
```

* How to assign a role to a service account?

`<role>` can be a custom role or a default role that GCP provides. If it's a
custom role created by the user, then this is how the role needs to be referred
to - `projects/<gcp-project-id>/roles/<role-name>`. If it's a built in role,
for example `Viewer`, use `roles/viewer` and that should work!

There are two ways to do this. One way is -

```
$ gcloud projects add-iam-policy-binding <gcp-project-id> --member serviceAccount:<service-account-email-id> --role <role>
```

Another way is -

```
$ gcloud iam service-accounts add-iam-policy-binding --member serviceAccount:<service-account-email-id> --role <role>
```

* How to assign a role to a user?

This is similar to assigning a role to service account, instead this time,
instead of mentioning `serviceAccount`, use `user` to denote it's a user and
then use the user's email ID. See below on how to do this

```
$ gcloud projects add-iam-policy-binding <gcp-project-id> --member user:<service-account-email-id> --role <role>
```

* How to take disk snapshots in a project?

You can take snapshots of multiple disks like this

```
$ gcloud --project <gcp-project-id> compute disks snapshot <disk-name-1> <disk-name-2> <disk-name-3> --snapshot-names <snapshot-name-1>,<snapshot-name-2>,<snapshot-name-3>
```

* How to list disk snapshots in a project?

```
$ gcloud --project <gcp-project-id> compute snapshots list
```

* How to delete disk snapshots in a project?

```
$ gcloud --project <gcp-project-id> compute snapshots delete <snapshot-name>
```
