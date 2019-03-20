## tnsnames.oraのtemplates反映を例に、j2の動きをちょろちょろと。
sandbox dockerテスト用  
```
　　[root@localhost git]# cat hosts
    [docker]
    hpb-queue-listener-docker
    [root@localhost git]#
    [root@localhost git]#
    [root@localhost git]# cat playbook.yml
    - hosts: docker
      connection: docker
      gather_facts: no
      tasks:
      - name: ping check
        ping:
      roles:
        - j2-vars-for-sentence
```
ファイル階層  
    `git/j2-vars-for-sentence`

実行後はこうなります。    
```
root@0d0fcdfbfb2a:/# cat /etc/tnsnames.ora
    netsrvicename01 =
    (DESCRIPTION =
      (ENABLE = BROKEN)
      (ADDRESS_LIST =
        (ADDRESS = (PROTOCOL = TCP)(HOST = ipaddr)(PORT = port))
        (ADDRESS = (PROTOCOL = TCP)(HOST = ipaddr)(PORT = port))
        (LOAD_BALANCE = ON or OFF)
        (FAILOVER = ON or OFF)
      )
      (CONNECT_DATA =
         (SERVICE_NAME = servicename01)
         (SERVER = DEDICATED or SHARED)
      )
    )
    netsrvicename02 =
    (DESCRIPTION =
      (ENABLE = BROKEN)
      (ADDRESS_LIST =
        (ADDRESS = (PROTOCOL = TCP)(HOST = ipaddr)(PORT = port))
        (ADDRESS = (PROTOCOL = TCP)(HOST = ipaddr)(PORT = port))
        (LOAD_BALANCE = ON or OFF)
        (FAILOVER = ON or OFF)
      )
      (CONNECT_DATA =
         (SERVICE_NAME = servicename02)
         (SERVER = DEDICATED or SHARED)
      )
    )
    netsrvicename03 =
    (DESCRIPTION =
      (ENABLE = BROKEN)
      (ADDRESS_LIST =
        (ADDRESS = (PROTOCOL = TCP)(HOST = ipaddr)(PORT = port))
        (ADDRESS = (PROTOCOL = TCP)(HOST = ipaddr)(PORT = port))
        (LOAD_BALANCE = ON or OFF)
        (FAILOVER = ON or OFF)
      )
      (CONNECT_DATA =
         (SERVICE_NAME = servicename03)
         (SERVER = DEDICATED or SHARED)
      )
    )
```
