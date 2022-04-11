# UFM Plugins Management


## Overview
This plugin is used to manage the UFM plugins.


## Init flow 
Local folder:  ufm_plugins.data/xxx (e.g. ufm_plugins.data/ndt)  will be mapped to /data in the container.
HA folder:  /opt/ufm/files/conf/plugins/xxx(e.g. /opt/ufm/files/conf/plugins/ndt) will be mapped to /config in the container . The Plugin should copy the HA replicated configuration into /config folder .
## RUN flow 
The /init.sh script in the container should do the following steps: 
1. Test UFM version if plugin can run with UFM. 
The UFM version will be supplied as input argument to the /init.sh script 
2. Update the /config folder: 
Generates if needed plugin configuration. (xxx.conf) 
Generates if needed http proxy configuration (xxx_httpd_proxy.conf) 
Generates if needed http proxy configuration (ufm_plugin_xxx_httpd.conf) 
Generates if needed additional mapping file (xxx_shared_volumes.conf) 
3. The container will exit once the init stage is done and Exit code will be checked 0 = sucsess
## Health  flow
Add to UFM Healt the follwing functionality:
1. Test if container is Enable  by using the  is-enable option.
2. Test if container is Runing  by using the  is-runnig option . If  not running , restart plugin by the start stop option
## Remove flow
The /deinit.sh script in the container should do the following steps: 
remove additional plugin data files (the container responsibility to remove data in additionalshared volumes) 
## Container Files Implementation notes
1. Container xxx_shared_volumes.conf format is: 
host_map1:container_map1 
host_map2:container_map2 
……. 
exsample: 
/opt/ufm/files/log:/log
/dev:/host_dev
2. Container xxx_httpd_proxy.conf format is:
 port=id
exsample: 
port=8980
3. Container ufm_plugin_ndt_httpd.conf format is:
 will be copy to /etc/httpd/conf.d/
exsample: 
<Location /ufmRest>
    SSLRenegBufferSize 52428800
</Location>
<Location /ufmRestV2>
    SSLRenegBufferSize 52428800

## Limitations 
1. On standby we cannot remove the files on Extra share volumes. There will be a message to tell the user to remove plugin on remote. 

