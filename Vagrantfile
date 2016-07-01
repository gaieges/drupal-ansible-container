# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.synced_folder ".", "/vagrant"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
  end


  config.vm.provision "shell", inline: <<-SHELL
    # xenial has some more invasive apt cron jobs that start on boot ..
    while ! apt-get update >/dev/null 2>&1; do
      echo 'waiting for apt lock to clear, then performing apt-get update ..'
      sleep 5
    done;

    apt-get install apt-transport-https -y


    apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D

    echo deb https://apt.dockerproject.org/repo ubuntu-xenial main > /etc/apt/sources.list.d/docker.list

    cat - <<EOF | tee /etc/systemd/system/docker.service
[Service]
ExecStart=/usr/bin/docker daemon -H 0.0.0.0:2375
EOF

    systemctl daemon-reload

    apt-get update && apt-get install docker-engine python python-pip libffi-dev libssl-dev python-dev git virtualbox-guest-utils -y

    git clone https://github.com/ansible/ansible-container.git /tmp/ansible-container

    cd /tmp/ansible-container
    python setup.py install

    echo export DOCKER_HOST="tcp://10.0.2.15:2375" >> /etc/profile.d/docker.sh
  SHELL
end
