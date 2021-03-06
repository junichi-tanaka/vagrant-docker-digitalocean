#
# pre-requirement
#  $ vagrant plugin install vagrant-digitalocean
#  $ vagrant plugin install nugrant
#
#  $ cat ~/.vagrantuser
#  digitalocean:
#    hostname: 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
#    client_id: 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
#    api_key: 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
#    ssh_key_name: 'xxxxx'
#    ssh:
#      private_key_path: '~/.ssh/id_rsa'
#

Vagrant.configure('2') do |config|
  config.vm.hostname              = config.user.digitalocean.hostname     # 好きなhostnameに変更

  config.vm.provider :digital_ocean do |provider, override|
    provider.client_id            = config.user.digitalocean.client_id    # https://cloud.digitalocean.com/api_access
    provider.api_key              = config.user.digitalocean.api_key      # https://cloud.digitalocean.com/api_access
    provider.ssh_key_name         = config.user.digitalocean.ssh_key_name # https://cloud.digitalocean.com/ssh_keys

    override.ssh.private_key_path = config.user.digitalocean.ssh.private_key_path
    override.vm.box               = 'digital_ocean'
    override.vm.box_url           = "https://github.com/smdahlen/vagrant-digitalocean/raw/master/box/digital_ocean.box"

    provider.image                = 'Ubuntu 14.04 x64'
    provider.region               = 'San Francisco 1'
    provider.size                 = '1GB'
  end

  config.vm.provision :shell, :inline => <<-EOT
     export DEBIAN_FRONTEND=noninteractive
     apt-get update -qq
     apt-get -y install linux-image-extra-`uname -r`
     apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9
     echo "deb http://get.docker.io/ubuntu docker main" | tee /etc/apt/sources.list.d/docker.list
     apt-get update -qq
     apt-get -y install lxc-docker
  EOT

end
