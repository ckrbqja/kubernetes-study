
```shell
kubeadm token list

kubeadm token create --ttl 1h
> dksd23a.dfkdsl3fk

[root@node2 ~]# kubeadm reset
...
[root@node2 ~]# kubeadm join 192.168.56.30:6443 --token [토큰] --discovery-token-ca-cert-hash sha256:7205b3fd6030e47b74aa11451221ff3c77daa0305aad0bc4a2d3196e69eb42b7 
```