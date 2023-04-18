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
