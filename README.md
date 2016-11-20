# mongoDB

[Download PEAR]
	curl -O http://pear.php.net/go-pear.phar
	sudo php -d detect_unicode=0 go-pear.phar

[Configure and Install PEAR]
You should now be at a prompt to configure PEAR.

1. Type 1 and press return.
2. Enter:

	/usr/local/pear
3. Type 4 and press return.
4. Enter:

	/usr/local/bin
5. Press return

[Verify PEAR]
You should be able to type:

	pear version

[MongoDB Monitoring]
Robomongo - Management Tool / Windows Supported
MUNIN - Nagios
MMS - Local & AWS Supported
MongoVUE - Management Tool / Windows Supported / ssh key Supported

Pandora FMS (Plug-in)

Command Base (http://docs.mongodb.org/manual/administration/monitoring/)
Gagila
mTop

[Matrix]
opcounters - count / sec
memory - mapped : sum of files on disk
virtual memory : 2 x mapped (j) + process overhead
Lock % - Amount of time spent in the write lock
Background flush - Flush every 1min.
Page faults 
	- Disk IO
	- Readahead
		I/O 와 CPU 연산을 동시에 수행해 그 수행 성능을 최대로 만들어 보겠다 라는 최적화 알고리즘이다.
		상식적으로 읽고 연산 해야 하지만, "미리 쓰일것 같아, 먼저 읽어 두겠다." 는 것이고, 그로 인해 연산을 먼저 시작할 수 있으므로 성능은 더 낳아진다. 라는 이론이다. 하지만 side effect 로 영원히 읽지 않아도 되는 것을 미리 읽어 I/O 성능을 갉아 먹을 수 있는 역 기능을 수행 할 수도 있다.

		미리읽기는 IAM 을 이용하는 방법과 index 의 non-leaf 를 이용하는 방법이 있다. 이것의 작동 방식은 BOL에 상세히 나와 있다. 조금만 살펴 본다면, IAM 이 bit 단위로 extents 할당 단위를 표현하고 있고, 이 IAM 1Byte를 읽어 (8 extents = 64K * 8 = 512K) 씩 물리적 방향에 맞게 ASync 방식으로 읽을수 있다. 또 Index 의 경우,  index 의 non-leaf 를 읽어 모여있는 페이지를 몇개를 Async 로 순서에 맞게 읽을 수 있으므로, 그 성능을 좋게 할 수 있다. 핵심은 역시 I/O 와 CPU 연산을 동시에 할 수 있다는 것이 가장 크다. SQL Server EE 의 경우 미리 읽기를 더 잘 할 수 있다.
