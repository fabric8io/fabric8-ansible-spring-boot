# kansible resources

This folder contains the [kubernetes](http://kubernetes.io/) resources for [kansible](https://github.com/fabric8io/kansible).

There is a folder per ansible host which contains an `rc.yml` to define the [Replication Controller](http://kubernetes.io/v1.1/docs/user-guide/replication-controller.html) to run the kansible pods:

* [appservers/rc.yml](appservers/rc.yml)
