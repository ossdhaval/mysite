# SUSE

## Difference between SLES, OpenSUSE Leap, OpenSUSE Tumbleweed

- https://www.suse.com/suse-defines/definition/opensuse-leap/

In essence, it starts with Tumbleweed(Free and managed by OpenSUSE), which is the most unstable but most frequently updated version. From this, the SLE (licensed and with paid support) and Leap(Free and managed by OpenSUSE) are created. Both are almost the same, with SLE being little more stable and certified for enterprises. 

## Onboarding to SUSE package hub



To onboard to suse package hub, you need to build your software on [SUSE Open Build System (OBS)](https://build.opensuse.org/)

Good information on how to build on OBS: https://openbuildservice.org/help/manuals/obs-user-guide/art.obs.bg.html

all user guides: https://openbuildservice.org/help/manuals/obs-user-guide/index.html



add java packages repo to fresh sles 15sp3

```
sudo zypper ar https://download.opensuse.org/repositories/Java:/packages/SLE_15_SP2/Java:packages.repo
sudo zypper refresh
zypper search --provides -v "mvn(io.prometheus:simpleclient_common)"
```

Output of last command above is 

```
S | Name                                | Type    | Version     | Arch   | Repository
--+-------------------------------------+---------+-------------+--------+-----------------------------------
  | prometheus-simpleclient-java-common | package | 0.8.0-17.66 | noarch | Factory Java packages (SLE_15_SP2)
    provides: mvn(io.prometheus:simpleclient_common) = 0.8.0
  | prometheus-simpleclient-java-common | package | 0.8.0-17.67 | noarch | Factory Java packages (SLE_15_SP2)
    provides: mvn(io.prometheus:simpleclient_common) = 0.8.0
  | prometheus-simpleclient-java-common | package | 0.8.0-17.69 | noarch | Factory Java packages (SLE_15_SP2)
    provides: mvn(io.prometheus:simpleclient_common) = 0.8.0
```

This means that package `prometheus-simpleclient-java-common` in repository `Factory Java packages (SLE_15_SP2)` provides `io.prometheus:simpleclient_common` maven dependency.


### imp commands

`zypper lr -u` to list all the repo
`zypper rr <repo_alias>` to delete repo

### links:

spec file guidelines: https://en.opensuse.org/openSUSE:Specfile_guidelines

packaging java: https://en.opensuse.org/openSUSE:Packaging_Java

About packaging: https://fedora-java.github.io/howto/latest/
