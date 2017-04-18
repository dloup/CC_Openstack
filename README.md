# CC_Openstack
Set of Heat templates to deploy Openstack using OS Puppet modules on Chameleon Cloud
There is 2 "type" of templates :
* Those using xp5k ( the tool used on Grid'5000 to depoy Openstack )
  * xp5k.yaml
  * xp5k_no_frontend.yaml
* Those using Heat agent and SoftwareConfig
  * liberty.yaml
  * liberty_mutlinodes.yaml
  * liberty_net_isolation.yaml
