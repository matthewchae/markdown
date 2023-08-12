

## 소개

Github pages 블로그를 운영하는 중입니다. 회사라는 틀에 박혀 찍어내기식 프로그래밍에 지친 나머지 블로그에서만큼은 제가 하고 싶은 프로젝트를 진행하고 싶어 만들게 되었습니다. 
* AI, Data Science 중독자입니다. 
* 책을 읽고, 리뷰를 쓰고, 베타리딩 및 베타테스트에 참가하길 좋아합니다.
* 소소하지만 살면서 얻은 깨달음이나, 개발자로서 경험하고 배웠던 것들을 공유할 예정이니 가끔 들려주시면 감사하겠습니다. :)

[ssh](#ssh)
[core_dump](#core-dump)
[systemd](#systemd)
[systemd1](#systemd1)

[devtool,ffbuild](#devtool,ffbuild)

[boot command](#boot_command)

<a name="devtool,ffbuild"></a>  
### devtool/ ffbuild

devtool status : 빌드 상태 같은것들을 보여준다.

devtool modify basic-device-info 

ffbuild basic-device-info

ffbuild –deploy  root@192.168.0.90 basic-device-info

devtool deploy-target recording-indexer root@192.168.0.85

*Make some changes and compile just the package you have changed - fast iteration!
$ devtool build packagemanager-cgi

$ devtool deploy-target -S -p -c -s packagemanager-cgi root@192.168.0.90

*On target

$systemctl daemon-reload

$systemctl restart packagemanager-cgi



<a name="boot_command"></a>  
### boot command

다른 서비스 런 안시키는거

boot_axis -i fimage -c 'systemd.unit=debug-shell.service’

boot_axis -i fimage -c 'tp_printk trace_event=clk:*'

axis-update ip 만약 axis-update -f ip이면 factory default이다.

axis-update -f 172..   -f는 factory default

fwmgr status

dmesg –n 8

dmesg –n 1

Pr_info로 안 보이면 dmesg로 확인. 로그레벨에 의해서 필터가 돼서 안보일때는 dmesg 사용

boot_axis -i fimage -c 'tp_printk trace_event=clk:*'

많은 디버그 메시지가 나온다.

dpkg -i /n/axis_releases/tools/netboot/debian/axis-netboot_3.36.1_amd64.deb

잘은 모르겠지만 Debian 10 버전에 맞는 boot_axis가 필요한 듯 하다.

저 위치에 있는걸 설치 하나 보다.

sudo apt-get install axis-netboot


<a name="ssh"></a>  
### ssh

Ssh enable하는 법
http://192.168.0.90/axis-cgi/admin/param.cgi?action=update&Network.SSH.Enabled=yes
192.168.0.90/axis-cgi/param.cgi?action=update&root.Network.SSH.Enabled=yes

sshfs이용해서 ~/fractal에 마운트하기
sshfs christwo@10.92.172.87:/home/christwo/ ~/fractal -o nonempty

scp로 파일 전송하기
scp testfile root@192.168.123.123:/app/tmp/testdir
scp로 파일 전송받기
   ->Copy the perf.data from target using scp:
 -> scp root@192.168.0.90:/tmp/perf.data .


사용자 변경
su -s /usr/bin/sh sdk

ssh-agent 문제일때
   ssh-agent
   eval $(ssh-agent)
   ssh-add ~/.ssh/id_rsa 입력한다음에 비번인 chae2142입력

netstat -ntl 이게 열려 있는 포트를 보여준다.

