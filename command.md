
[ssh](#ssh)

[systemd](#systemd)

[core_dump](#core_dump)
 
[devtool,ffbuild](#devtool,ffbuild)

[boot command](#boot_command)

[find](#find)

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


<a name="core_dump"></a>  
### core dump

Core dump 발생하는거 기다리고 있기.
https://gittools.se.axis.com/gerrit/plugins/gitiles/apps/dbox/+/refs/heads/master/
-> 옛날 버전에서는 하기 사용
wget -T0 -O core 'http://root:pass@192.168.0.90/axis-cgi/debug/debug.cgi?listen'
여기서 debug.cgi대신 debug.tgz 사용

Core dump 발생시키기
-> 타겟에서 dbox segfault하면 에러 발생

/usr/local/syslog.log   persistent이다. core dump되면 여기에 로그가 남는다.

<a name="find"></a>  
### find

find tmp | grep busybox | grep .config$

find /ect/systemd/system/ -type d -name “want*”

repo grep meson | grep inherit | grep meta-axis

find /home/matthewc/project/q1656-dle3/q1656-dle/builds/q1656-dle/workspace/sources/busybox | grep defconf

ls meta*/recipes*/*/*.bb | grep basic-device

ls */ - List subdirectories in the current directory:

find . -name “*.mp3” | xargs rm -rf

Xargs가 pipe 이전의 명령 수행 결과 문자열을 그대로 rm으로 전달 해준다.

근데 이 명령은 결과에 공백이나 줄바꿈 문자들이 있으면 그것들은 실행이 안된다.

그래서 -print0를 추가하면 find 명령어에 의해 검색된 모든 검색 결과의 마지막에 널 문자를 넣어줌

즉, mp3 뒤에 널이 추가됨. 그래서 파일의 시작과 끝을 구별할 수 있음.

find . -name “*.mp3”  -print0 | xargs -0 rm -rf

이렇게 하면 null 문자로 분리 된 검색 결과를 전달 받아서 

Xarg가 분리 된 단어로 rm으로 전달 해 준다.

Find 조건 -exec 실행시킬 명령어

Find로 찾은것을 exec로 어떤 명령을 실행시켜라

cat /etc/passwd | grep basic

<a name="systemd"></a>  
### systemd
systemd-analyze time
systemctl restart systemd-journald
$systemctl daemon-reload
$systemctl restart packagemanager-cgi

systemctl status init-pkcs11-token : 서비스 확인

systemctl list-units | grep radar-autotracking
systemctl list-units radar*
systemctl list-unit-files | grep radar-autotracking
systemctl list-unit-files radar*

systemctl mask 서비스 이렇게 해야 완전히 정지한다.

systemctl list-dependencies radar-scene-provider
systemctl list-dependencies --reverse radar-scene-provider

systemctl mask radar-autotracking.service
systemctl mask chronyd
systemctl mask upnp
systemctl mask video-object-detection.service
systemctl mask larod
systemctl mask geolocationd.service
systemctl mask policykit-parhand.service

systemctl unmask policykit-parhand.service unmassk하고
다시 시작하려면 mask하고 restart해줘라.
systemctl cat radar-autotracking.service

systemctl list-dependencies –reverse radar-scene-provider.service

Systemd로 부팅 plot을 만드는 법
On target: systemd-analyze plot > /etc/httpd/html/plot.svg
In browser: http://<AXIS_TARGET_IP>/local/plot.svg

journalctl -f 하면 로그가 실시간으로 나온다.

busctl,

