# Rancher Notes

[Difference between Rancher and RKE](https://www.suse.com/c/rancher_blog/rancher-vs-rke-what-is-the-difference/)


## Troubleshooting

#### after installing openebs chart on a Rancher cluster (`rancher on a single docker container`), the openebs-ndm pod doesn't come up. It stays in `creatingcontainer` state.

- root cause:
  -   on rancher dashboard if you go to `apps -> openebs -> openebs-ndm(daemonset) -> 	recent events` it'll show you errors like `MountVolume.SetUp failed for volume "udev" : hostPath type check failed: /run/udev is not a directory ` and `Unable to attach or mount volumes: unmounted volumes=[udev], unattached volumes=[procmount devmount basepath sparsepath kube-api-access-tskml config udev]: timed out waiting for the condition`
-   Solution: is to create a `udev` directory under `/run` on the docker container
  -   find the docker container ID by running this command on host os:
      ```
      docker ps
      ```
   -  Copy the container id and open bash of that container
      ```
      docker exec -ti 373a506bcf20 bash
      ```
   - create the directory `mkdir /run/udev`
