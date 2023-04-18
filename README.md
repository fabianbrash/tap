```TAP gotchas and everything else```

#### To create the secret follow the docs


[https://docs.vmware.com/en/VMware-Tanzu-Application-Platform/1.4/tap/scc-git-auth.html](https://docs.vmware.com/en/VMware-Tanzu-Application-Platform/1.4/tap/scc-git-auth.html)


[https://docs.vmware.com/en/VMware-Tanzu-Application-Platform/1.4/tap/scc-building-from-source.html](https://docs.vmware.com/en/VMware-Tanzu-Application-Platform/1.4/tap/scc-building-from-source.html)

```Generate new SSH keypair```


````
ssh-keygen -t ecdsa -b 521 -C "" -f "identity" -N ""

````

##### The above creates identity and identity.pub


##### Gather public keys from Github, again we could change the below to gitlab.com, or anywhere else


````
ssh-keyscan github.com > ./known_hosts

````


##### Don't forget to add it to our default serviceaccount in the desired namespace(s)

##### Example of a workload.yaml file using a private repo

[https://github.com/fabianbrash/tap-java-functions/blob/main/config/workload.yaml](https://github.com/fabianbrash/tap-java-functions/blob/main/config/workload.yaml)

##### The key piece here is the git URL


````
apiVersion: carto.run/v1alpha1
kind: Workload
metadata:
  name: java-function
  labels:
    apps.tanzu.vmware.com/workload-type: web
    app.kubernetes.io/part-of: java-function
  namespace: backend
spec:
  source:
    git:
      url: ssh://git@github.com:fabianbrash/tap-java-functions.git
      ref:
        branch: main
  build:
    env:
      - name: BP_FUNCTION
        value: functions.Handler

````
