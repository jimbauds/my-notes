# CoreOS Notes

```yaml
# basic cloud-config.yaml
coreos:
  etcd:
    # generate a new token for each unique cluster from https://discovery.etcd.io/new
    discovery: https://discovery.etcd.io/<token>
    # multi-region and multi-cloud deployments need to use $public_ipv4
    addr: $private_ipv4:4001
    peer-addr: $private_ipv4:7001
  units:
    - name: etcd.service
      command: start
    - name: fleet.service
      command: start
      
# basic cloud-config.yaml
coreos:
  units:
    - name: etcd.service
      command: start
    - name: fleet.service
      command: start
```

```sh
# hello.service under /home
[Unit]
Description=My Service
After=docker.service

[Service]
TimeoutStartSec=0
ExecStartPre=-/usr/bin/docker kill hello
ExecStartPre=-/usr/bin/docker rm hello
ExecStartPre=/usr/bin/docker pull busybox
ExecStart=/usr/bin/docker run --name hello busybox /bin/sh -c "while true; do echo Hello World; sleep 1; done"
ExecStop=/usr/bin/docker stop hello

fleetctl load hello.service
fleetctl start hello.service
fleetctl destroy hello.service

fleetctl list-units
fleetctl list-machines

gcutil --project=<project-id> addinstance --image=projects/coreos-cloud/global/images/coreos-stable-367-1-0-v20140724 --persistent_boot_disk --zone=us-central1-a --machine_type=n1-standard-1 --metadata_from_file=user-data:cloud-config.yaml core1 core2 core3
```

## etcd
```sh
# list keys and directory
etcdctl ls

# Delete directory that contain keys
curl -L http://127.0.0.1:4001/v2/keys/dir?recursive=true -XDELETE
```
