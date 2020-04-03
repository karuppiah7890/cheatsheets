# gcloud

This is my cheatsheet for anything related to `gcloud`

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
$  gcloud config list
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

Depending on if it's a zonal or regional cluster, you will need to specify
`--zone` or `--region` appropriately

```
$ gcloud --project <gcp-project-id> container clusters get-credentials <gke-cluster-name> [--zone <zone-name> | --region <region-name>]
```

* How do I check / list the custom IAM roles in a project?

Usually GCP has some roles by default, like `viewer`, `editor`, `owner` and
more. You can also create custom IAM roles which you can list like this

```
$ gcloud --project <gcp-project-id> iam roles list
```

* How do I describe an IAM role?

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

* How do I list the disks attached to a compute engine instance (VM)?

* How do I resize a disk?

(include resize2fs command too)

* How to SSH into a machine?

(public IP)

(private IP)

* How do I check the kubernetes cluster operations happening in a project's clusters?

* How do I describe an operation using the operation ID?

* How do I cancel an operation using the operation ID?

* How do I check the list of node pools present in a cluster?

* How do I describe a single node pool to check it's details?

* How to find the total number of disks that can be attached to a node?