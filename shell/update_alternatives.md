```bash
ysdlb@ubuntu:~$ sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk-11.0.4/bin/java
update-alternatives: --install needs <link> <name> <path> <priority>

Use 'update-alternatives --help' for program usage information.
ysdlb@ubuntu:~$ sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk-11.0.4/bin/java 2
update-alternatives: using /usr/lib/jvm/jdk-11.0.4/bin/java to provide /usr/bin/java (java) in auto mode

ysdlb@ubuntu:~$ sudo update-alternatives --config java
There is only one alternative in link group java (providing /usr/bin/java): /usr/lib/jvm/jdk-11.0.4/bin/java
Nothing to configure.
ysdlb@ubuntu:~$ sudo update-alternatives --install /usr/bin/jar jar /usr/lib/jvm/jdk-11.0.4/bin/jar 2
update-alternatives: using /usr/lib/jvm/jdk-11.0.4/bin/jar to provide /usr/bin/jar (jar) in auto mode
ysdlb@ubuntu:~$ sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk-11.0.4/bin/ja
jaotc      jar        jarsigner  java       javac      javadoc    javap
ysdlb@ubuntu:~$ sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk-11.0.4/bin/javac 2
update-alternatives: using /usr/lib/jvm/jdk-11.0.4/bin/javac to provide /usr/bin/javac (javac) in auto mode
ysdlb@ubuntu:~$ java --version
java 11.0.4 2019-07-16 LTS
Java(TM) SE Runtime Environment 18.9 (build 11.0.4+10-LTS)
Java HotSpot(TM) 64-Bit Server VM 18.9 (build 11.0.4+10-LTS, mixed mode)
```
