##把本地文件的公钥copy到112.126.69.94
	 cat ~/.ssh/id_rsa.pub | ssh root@112.126.69.94 "cat - >> ~/.ssh/authorized_keys"

ssh 无密码登录要使用公钥与私钥。linux下可以用用ssh-keygen生成公钥/私钥对，下面我以CentOS为例。

有机器A(192.168.1.155)，B(192.168.1.181)。现想A通过ssh免密码登录到B。
首先以root账户登陆为例。


##1.在A机下生成公钥/私钥对。

[root@A ~]# ssh-keygen -t rsa -P ''

-P表示密码，-P '' 就表示空密码，也可以不用-P参数，这样就要三车回车，用-P就一次回车。
该命令将在/root/.ssh目录下面产生一对密钥id_rsa和id_rsa.pub。

一般采用的ssh的rsa密钥:
id_rsa     私钥
id_rsa.pub 公钥
下述命令产生不同类型的密钥
ssh-keygen -t dsa
ssh-keygen -t rsa
ssh-keygen -t rsa1

##2.把A机下的/root/.ssh/id_rsa.pub 复制到B机的 /root/.ssh/authorized_keys文件里，先要在B机上创建好 /root/.ssh 这个目录，用scp复制（注意如果有authorized_keys会丢失其他已有的权限）。

	[root@A ~]# scp /root/.ssh/id_rsa.pub root@192.168.1.181:/root/.ssh/authorized_keys
	root@192.168.1.181's password:
	id_rsa.pub                                    100%  223     0.2KB/s   00:00
##追加权限
	[root@A ~]#  cat ~/.ssh/id_rsa.pub | ssh root@112.126.69.94 "cat - >> ~/.ssh/authorized_keys"

由于还没有免密码登录的，所以要输入一次B机的root密码。

##3.authorized_keys的权限要是600!!!

[root@B ~]# chmod 600 /root/.ssh/authorized_keys



##4.A机登录B机。

[root@A ~]# ssh -l root 192.168.1.181
The authenticity of host '192.168.1.181 (192.168.1.181)' can't be established.
RSA key fingerprint is 00:a6:a8:87:eb:c7:40:10:39:cc:a0:eb:50:d9:6a:5b.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.1.181' (RSA) to the list of known hosts.
Last login: Thu Jul  3 09:53:18 2008 from root
[root@B ~]#

第一次登录是时要你输入yes。

现在A机可以无密码登录B机了。

小结：登录的机子可有私钥，被登录的机子要有登录机子的公钥。这个公钥/私钥对一般在私钥宿主机产生。上面是用rsa算法的公钥/私钥对，当然也可以用dsa(对应的文件是id_dsa，id_dsa.pub)

想让A，B机无密码互登录，那B机以上面同样的方式配置即可。

 

 

 

#SSH-KeyGen 的用法

 

假设 A 为客户机器，B为目标机；

要达到的目的：
A机器ssh登录B机器无需输入密码；
加密方式选 rsa|dsa均可以，默认dsa

做法：
1、登录A机器
2、ssh-keygen -t [rsa|dsa]，将会生成密钥文件和私钥文件 id_rsa,id_rsa.pub或id_dsa,id_dsa.pub
3、将 .pub 文件复制到B机器的 .ssh 目录， 并 cat id_dsa.pub >> ~/.ssh/authorized_keys
4、大功告成，从A机器登录B机器的目标账户，不再需要密码了；

 

 

 

ssh-keygen做密码验证可以使在向对方机器上ssh ,scp不用使用密码.
具体方法如下:
ssh-keygen -t rsa
然后全部回车,采用默认值.

这样生成了一对密钥，存放在用户目录的~/.ssh下。
将公钥考到对方机器的用户目录下，并拷到~/.ssh/authorized_keys中。

要保证.ssh和authorized_keys都只有用户自己有写权限。否则验证无效。（今天就是遇到这个问题，找了好久问题所在），其实仔细想想，这样做是为了不会出现系统漏洞。