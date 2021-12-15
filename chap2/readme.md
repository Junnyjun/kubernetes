### 테스트 환경 구성하기

코드형 인프라로 인프라 환경을 일정하게 유지하고 구성 ( 코드형 인프라 ) 



>  Vagrant & Virtual Box 설치



> Vagrant 

사용자의 요구에 맞게 시스템 자원을 할당 배치 배포해 두었다가 필요할 때 시스템을 사용할 수 있는 상태로 만들어 준다 = 프로비저닝 

| 명령                | 설명                              |
| ----------------- | ------------------------------- |
| vagrant init      | 프로비저닝을 위한 기초 파일 생성              |
| vagrant up        | Vagarantfile을 읽어 들여 프로비저닝을 진행   |
| vagrant halt      | Vagrant의 가상머신을 종료               |
| vagrant destroy   | vagrant의 가상머신을 삭제               |
| vagrant ssh       | vagrant에 ssh로 접속                |
| vagrant provision | vagrant에서 관리하는 가상머신에 변경된 설정을 적용 |



> Vagrantfile

[Vagrant 기본 파일](./Vagrantfile_1) 

```ruby
# -*- mode: ruby -*- 
# vi: set ft=ruby :  // 현재 파일이 ruby임을 인식
Vagrant.configure("2") do |config| 0
  config.vm.define "m-k8s" do |cfg|
    cfg.vm.box = "sysnet4admin/CentOS-k8s"
    cfg.vm.provider "virtualbox" do |vb|
      vb.name = "m-k8s(github_SysNet4Admin)"
      vb.cpus = 2
      vb.memory = 2048
      vb.customize ["modifyvm", :id, "--groups", "/k8s-SM(github_SysNet4Admin)"]
    end
    cfg.vm.host_name = "m-k8s"
    cfg.vm.network "private_network", ip: "192.168.1.10"
    cfg.vm.network "forwarded_port", guest: 22, host: 60010, auto_correct: true, id: "ssh"
    cfg.vm.synced_folder "../data", "/vagrant", disabled: true
  end
end
```



###### IP 등록 정보를 확인 

```bash
[vagrant@k8s ~]$ ip addr show eth1
3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:ac:94:59 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.10/24 brd 192.168.1.255 scope global noprefixroute eth1
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:feac:9459/64 scope link
       valid_lft forever preferred_lft forever
```



###### VM에 추가 패키지 설치

[Vagrant 2](./Vagrantfile_2)   ##  fg.vm.provision "shell", path: "install_pkg.sh" 추가 

> install_pkg.sh

```sh
#!/usr/bin/env bash

# install packages 
yum install epel-release -y
yum install vim-enhanced -y
```



###### EPEL 패키지 확인

```bash
[vagrant@m-k8s ~]$ yum repolist
Loaded plugins: fastestmirror
Determining fastest mirrors
 * base: mirror.navercorp.com
 * epel: ftp.riken.jp
```

---

#### 가상 서버 3개 운용 

> [Vagrant 3 (가상서버 3개 ) ](./Vagrantfile_3) 



> Ping 테스트

```sh
# ping 3 times per nodes
ping 192.168.1.101 -c 3
ping 192.168.1.102 -c 3
ping 192.168.1.103 -c 3
```



> Config 파일

```sh
#!/usr/bin/env bash
# modify permission  
chmod 744 ./ping_2_nds.sh
```

