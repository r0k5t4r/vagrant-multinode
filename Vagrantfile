#
#  Multi machine, essential options Vagrant file example. (documentation removed)
#
nodes = {
   "k8s-master" => ["bento/centos-7", 2, 4096, 21 ],
   "k8s-node1" 	=> ["bento/centos-7", 2, 2048, 22 ],
   "k8s-node2" 	=> ["bento/centos-7", 2, 2048, 22 ],
   "k8s-node3" 	=> ["bento/centos-7", 2, 2048, 22 ],
}

Vagrant.configure(2) do |config|
  nodes.each do | (name, cfg) |
    box, numvcpus, memory, storage = cfg

    config.vm.define name do |machine|
      machine.vm.box   = box
	  #machine.vm.box = 'esxi_clone/dummy'
      machine.vm.hostname = name
      machine.vm.synced_folder('.', '/Vagrantfiles', type: 'rsync')
	  machine.vm.synced_folder('.', '/vagrant', type: 'nfs', disabled: true)

      machine.vm.provider :vmware_esxi do |esxi|
        esxi.esxi_hostname         = '192.168.2.10'
        esxi.esxi_username         = 'root'
        esxi.esxi_password         = 'file:'
        esxi.esxi_virtual_network  = "VM Network"
        esxi.guest_numvcpus        = numvcpus
        esxi.guest_memsize         = memory
        esxi.guest_storage         = storage
        #esxi.clone_from_vm        = box
		esxi.esxi_resource_pool = "/"
        esxi.local_allow_overwrite = 'True'
		esxi.guest_nic_type = 'vmxnet3'
		#esxi.esxi_disk_store = 'DS_001'
		#esxi.debug = 'true'

      end
    end
  end
end