# -*- mode: ruby -*-
# vi: set ft=ruby :

NNODES=6

$script = <<-SCRIPT
echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCy+J7+gdORdTsc12eLcPmhdOAyRKTKIq18ENBu6Ffn4LcwOjOtW5v3IG9UeQO0I1JzCJSyIX972P3QTKENpWY0c8pnhYYDP3o5Kvynwm9N04Lyt0qMByy2husNp4XUNnoxa4dB/uuct+oLT4LFE5HDafSgqU3Yfy3MJZQw8neOESZG8IS+Tt3OZtB5UlYeWLXSkg8t0aB6af0WVL0Oy7I19T/N1zJkATGQ2Ll5O6sGwbst5P/sD4pI9CMWKb/jWPven8DhafXaz5VK5G+NKR5s6oXg6OFrS00uvVBIC1S3vnQ1whzyEMeNJqyoaQ1gNrjozyLuqqOnY2nFB31gWdlKL7eBsemBI8IsWrexkr6apiq+rYjvEfWz2r9WMoFM3kJvThCq/AnAw7J+tikn5dUoOKK3w0dp+zjxMtS8s1GJWYu8/O3p3+Lg1GhDlQa2FWwm+pGB4q3m9n/RU9EdHDnG8DYfFBdI1hAEazDky0l4e6hY9KxVVvaBnbTQp7gZQdXqtQGgHDtb3MGAkdSYAIHPYa2xRfUL2+a/eYn5d4YRG7kRgTWHT5/RAEZE7N74rSvBY6XitEfWfDVqDWvVR0oJOm9W1sl2oKKMLOzrXfSymY9IASdqhP6g0byXSpKLF2D/IvbSwaXEEEw8iGkfMafPZ2IutZkhYQR3v/jCSROa1w== your_email@example.com" >> /home/vagrant/.ssh/authorized_keys
SCRIPT

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  (0..NNODES - 1).each do |i|
    config.vm.define "k8s-ubuntu-#{i}" do |node|
      #node.vm.box = "ubuntu/focal64"
      node.vm.box = "ubuntu/jammy64"
      node.vm.hostname = "k8s-ubuntu-#{i}"
      config.vm.provider "virtualbox" do |v|
          v.memory = 2048
          v.cpus = 2
      end
      node.vm.network "private_network", ip: "192.168.25.11#{i}"
      node.vm.provision "shell", inline: $script
      node.vm.provision "shell", inline: "echo hello from node #{i}"
    end
  end
end