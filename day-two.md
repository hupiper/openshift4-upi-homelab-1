# OpenShift 4 UPI Home Lab Post Installation (Day 2)

Refer to this documentation for [initial lab installation].

## Configure your laptop

To view the console and oauth URLs from your laptop outside of the cluster, add the following entries to your laptop's `/etc/hosts`:
```
<your-laptop-ip> console-openshift-console.apps.<your-cluster-domain>
<your-laptop-ip> oauth-openshift.apps.<your-cluster-domain>
```

## Configure Operators

By following the [initial lab installation], your OpenShift cluster is complete.  Thus, the following instructions are entirely optional, but provide some guidance on day 2 configuration.

### 1. Configure image registry

In OpenShift 4.3, the image registry operator will start in a Removed state with the following note: "Image Registry has been removed. ImageStreamTags, BuildConfigs and DeploymentConfigs which reference ImageStreamTags may not work as expected. Please configure storage and update the config to Managed state by editing configs.imageregistry.operator.openshift.io."

Two quick options to configure the Image Registry operator are provided below to get started.  Please note that these are not recommended for production use.

#### 1a. Configure NFS storage

  Refer to these instructions to [configure NFS storage using your helper node].  Refer to the following for additional documentation to [configure NFS storage].

#### 1b. Configure ephemeral storage

  To configure ephemeral storage instead, you can run the following:
  ```
  oc patch configs.imageregistry.operator.openshift.io cluster --type merge --patch '{"spec":{"storage":{"emptyDir":{}}}}'
  ```

  Refer to the following for additional documentation to [configure ephemeral storage].


### 2. Configure additional operators

Refer to these instructions to configure additional operators
* [Local storage operator]
* [Prometheus operator with persistent storage]
* [Metering operator]
* [3scale operator]

### 3. Configure chrony time service

Refer to these instructions to configure chrony time service
* [Chrony time service]

## License
GPLv3

## Author
Kevin Chung

[initial lab installation]: README.md
[configure NFS storage using your helper node]: ./operator/image-registry/
[configure NFS storage]: https://docs.openshift.com/container-platform/4.3/registry/configuring-registry-storage/configuring-registry-storage-baremetal.html#registry-configuring-storage-baremetal_configuring-registry-storage-baremetal
[configure ephemeral storage]: https://docs.openshift.com/container-platform/4.3/registry/configuring-registry-storage/configuring-registry-storage-baremetal.html#installation-registry-storage-non-production_configuring-registry-storage-baremetal
[Local storage operator]: ./operator/local-storage/
[Prometheus operator with persistent storage]: ./operator/metrics/
[Metering operator]: ./operator/metering/
[3scale operator]: ./operator/3scale/
[Chrony time service]: ./machineconfig/chrony/
