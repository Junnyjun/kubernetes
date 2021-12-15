##### 테스트 환경 구성하기

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

