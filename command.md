

## 소개

Github pages 블로그를 운영하는 중입니다. 회사라는 틀에 박혀 찍어내기식 프로그래밍에 지친 나머지 블로그에서만큼은 제가 하고 싶은 프로젝트를 진행하고 싶어 만들게 되었습니다. 
* AI, Data Science 중독자입니다. 
* 책을 읽고, 리뷰를 쓰고, 베타리딩 및 베타테스트에 참가하길 좋아합니다.
* 소소하지만 살면서 얻은 깨달음이나, 개발자로서 경험하고 배웠던 것들을 공유할 예정이니 가끔 들려주시면 감사하겠습니다. :)

[SSH](#ssh)
[core_dump](#core-dump)
[systemd](#systemd)
[systemd1](#systemd1)
[devtool,ffbuild](#devtool,ffbuild)

#ssh
Ssh enable하는 법
http://192.168.0.90/axis-cgi/admin/param.cgi?action=update&Network.SSH.Enabled=yes
192.168.0.90/axis-cgi/param.cgi?action=update&root.Network.SSH.Enabled=yes

sshfs이용해서 ~/fractal에 마운트하기
sshfs christwo@10.92.172.87:/home/christwo/ ~/fractal -o nonempty
Scp로 파일 전송하기
scp testfile root@192.168.123.123:/app/tmp/testdir
Scp로 파일 전송받기
   ->Copy the perf.data from target using scp:
 -> scp root@192.168.0.90:/tmp/perf.data .

netstat -ntl


#core dump
Core dump 발생하는거 기다리고 있기.
https://gittools.se.axis.com/gerrit/plugins/gitiles/apps/dbox/+/refs/heads/master/
-> 옛날 버전에서는 하기 사용
wget -T0 -O core 'http://root:pass@192.168.0.90/axis-cgi/debug/debug.cgi?listen'
여기서 debug.cgi대신 debug.tgz 사용

Core dump 발생시키기
-> 타겟에서 dbox segfault하면 에러 발생

/usr/local/syslog.log   persistent이다. core dump되면 여기에 로그가 남는다.


#systemd 

systemd-analyze time
systemctl restart systemd-journald
$systemctl daemon-reload
$systemctl restart packagemanager-cgi


#systemd1 

systemd-analyze time
systemctl restart systemd-journald
$systemctl daemon-reload
$systemctl restart packagemanager-cgi

#systemd4 

systemd-analyze time
systemctl restart systemd-journald
$systemctl daemon-reload
$systemctl restart packagemanager-cgi

#systemd5 

systemd-analyze time
systemctl restart systemd-journald
$systemctl daemon-reload
$systemctl restart packagemanager-cgi 


#systemd6 

systemd-analyze time
systemctl restart systemd-journald
$systemctl daemon-reload
$systemctl restart packagemanager-cgi 


#systemd7 

systemd-analyze time
systemctl restart systemd-journald
$systemctl daemon-reload
$systemctl restart packagemanager-cgi 




<a name="devtool,ffbuild"></a>  
#### devtool/ ffbuild

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



