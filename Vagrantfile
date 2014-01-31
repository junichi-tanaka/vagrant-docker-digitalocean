#
# pre-requirement
#  $ vagrant plugin install vagrant-digitalocean
#  $ vagrant plugin install nugrant
#
#  $ cat ~/.vagrantuser
#  digitalocean:
#    client_id: 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
#    api_key: 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
#    ssh_key_name: 'xxxxx'
#    ssh:
#      private_key_path: '~/.ssh/id_rsa'
#

Vagrant.configure('2') do |config|
  config.vm.hostname              = 'docker.jeeta.net'  # 好きなhostnameに変更

  config.vm.provider :digital_ocean do |provider, override|
    provider.client_id            = config.user.digitalocean.client_id    # https://cloud.digitalocean.com/api_access
    provider.api_key              = config.user.digitalocean.api_key      # https://cloud.digitalocean.com/api_access
    provider.ssh_key_name         = config.user.digitalocean.ssh_key_name # https://cloud.digitalocean.com/ssh_keys

    override.ssh.private_key_path = config.user.digitalocean.ssh.private_key_path
    override.vm.box               = 'digital_ocean'
    override.vm.box_url           = "https://github.com/smdahlen/vagrant-digitalocean/raw/master/box/digital_ocean.box"

    provider.image                = 'Ubuntu 13.04 x64'
    provider.region               = 'San Francisco 1'
    provider.size                 = '1GB'
  end

  config.vm.provision :shell, :inline => <<-EOT
     apt-get update
#     export LANGUAGE=en_US.UTF-8
#     export LANG=en_US.UTF-8
#     export LC_ALL=en_US.UTF-8
#     locale-gen en_US.UTF-8
#     dpkg-reconfigure -f noninteractive locales
     export DEBIAN_FRONTEND=noninteractive
     apt-get -y --force-yes -o 'Dpkg::Options::=--force-confnew' install linux-image-extra-`uname -r`
     apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9
     echo "deb http://get.docker.io/ubuntu docker main" | tee -a /etc/apt/sources.list.d/docker.list
     apt-get update
     apt-get -y --force-yes -o 'Dpkg::Options::=--force-confnew' install lxc-docker
  EOT

end
