ha-cluster-rgmanager
=========

Role for configuring basic rgmanager high-availability cluster on CentOS/RHEL 5/6 systems.

Requirements
------------

RHEL: It is expected that machines will already be registered and subscribed for access to 'High Availability' or 'Resilient storage' channels.
CentOS 5.xx: requires installation of python-simplejson.x86_64 package prior to ansible run.

Role Variables
--------------

  - user and group for ricci daemon (for most deployments doesn't need changing except password)

    ```
    cluster_user: ricci
    ```

    ```
    cluster_user_pass: testtest
    ```

    ```
    cluster_group: ricci
    ```

  - name of the cluster

    ```
    cluster_name: rgmanager
    ```

  - configuration of firewall for clustering, NOTE this replaces iptables configuration file!
  
    ```
    cluster_firewall: true
    ```

  - enable cluster on boot
  
    ```
    cluster_enable_service: true
    ```

  - configure cluster with fence_xvm fencing device ?
    This will copy /etc/cluster/fence_xvm.key to nodes and add fencing devices to cluster
    NOTE: you need to define 'hypervisor_hostname' in the inventory for each cluster node
  
    ```
    cluster_configure_fence_xvm: true
    ```

  - use custom multicast address for cluster communication (by default cluster generates
    multicast address based on cluster ID)
    ```
    multicast_address: 239.192.1.2
    ```

Example Playbook
----------------

Example playbook for creating cluster named 'test1' enabled on boot, with fence_xvm and firewall settings

    - hosts: servers
      roles:
         - { role: OndrejHome.ha-cluster-rgmanager, cluster_name: 'test1' }

Example for creating cluster named 'test2' without configuring firewalling and without fence_xvm.
For cluster to get properly authorize it is expected that firewall is already configured or disabled.

    - hosts: servers
      roles:
         - { role: OndrejHome.ha-cluster-rgmanager, cluster_name: 'test2', cluster_firewall: false, cluster_configure_fence_xvm: false }

License
-------

GPLv3

Author Information
------------------

WARNING: this is alpha-version quality proof-of-concept role that still needs some polishing. 
         This is suitable for testing purposes only.

To get in touch with author you can use email ondrej-xa2iel8u@famera.cz or create a issue on github when requesting some feature.
