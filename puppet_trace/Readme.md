This folder contains Puppet logs with the execution time of each steps. To have this measure, replace
`/opt/puppetlabs/bin/puppet agent -t --server ${controller_name}.openstacklocal > /root/puppet.log 2>&1 || true`<br/>
with<br/>
`/opt/puppetlabs/bin/puppet agent -t --server ${controller_name}.openstacklocal --evaltrace > /root/puppet.log 2>&1 || true`<br/>
in heat templates.

We have 3 log files:
 - controller_base_image.log        :  Puppet log from the controller node when using the OS-Liberty-Puppet_base image
 - controller_controller_image.log  :  Puppet log from the controller node when using the OS-Liberty-Puppet_controller image (default for liberty.yaml )
 - compute_base_image.log           :  Puppet log from the compute node when using the OS-Liberty-Puppet_base image (default for liberty.yaml)

These logs can be used to optimize futur deployment by adding more content in the base image.

Here are some usefull commands to have more readable logs :
Show only lines that show "evaluated time" and only when this time is > 1 sec :<br/>
`cat controller_base_image.log | grep "Evaluated in [1-9]\+\.[0-9]\+ seconds"`

Show only times concerning packages ( which seems to be the only part we can optimize by generating a new image )<br/>
`cat controller_base_image.log | grep "Package.*Evaluated"`


By comparing the total time difference between controller_base_image.log and controller_controller_image.log,
we can see that we gain **249 sec** with the **OS-Liberty-Puppet_controller image**.

*Note : All the logs comes from deployment on UC.*
