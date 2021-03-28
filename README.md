# Container_CAP_Explotation

There is time that containers run with excesive privileges. To check them (within the container you can run) “capsh –print”.

Excesive linux capabilities like (cap_net_raw, cap_sys_admin, cap_setuid, cap_sys_module, cap_sys_ptrace, cap_dac_read_search, dac_override) can be abused. In this repository I will put some of them. 

The default capabilities are:

SETPCAP	Allow a process to change it's own capabilities set (within the set it is already allowed). Should not be dangerous in practice.
MKNOD	Allows creation of special devices. Almost all containers will receive the devices they need automatically, so this is almost never needed.
AUDIT_WRITE	Allow the container to write records to the underlying kernel auditing log. This is generally used for things like ssh login. It is a better practice to keep all container logs within the container and drain them, rather than allow the container to write to the host log files.
CHOWN	Allow the container process to change file permissions. This should generally never be needed in production.
NET_RAW	Allows RAW and PACKET sockets, which can be used to spy on networks or create nasty packets. Some applications may need this, but most won't.
DAC_OVERRIDE	Allows the root user to bypass normal file permission checks. No container should ever need this.
FOWNER	Bypass permission checks on operations that normally require the UID of the process to match the UID of the file.
FSETID	Don’t clear set-user-ID and set-group-ID permission bits when a file is modified. This should only be needed by installations, so generally not in production. Allowing this can let a user modify privileged programs.
KILL	Allow the root user to send kill signals to non-root processes. Not generally needed if keeping one container per process, but not too dangerous in general.
SETUID	Allows running of setuid binaries, which allows a process to change it's effective user id. This is required for some processes that require privileged ports (less than 1024) and by some processes like Apache to start. It should only be given to containers that need it.
SETGID	Just like setuid above, but for group ids.
NET_BIND_SERVICE	Bind to ports less than 1024. Enable this if your container runs a service that listens in the this port range only.
SYS_CHROOT	Allows use of the chroot command. Enable only if your process actively uses chroot to change the root directory.
SETFCAP	Allows the container to set file capabilities. Sometimes this is needed during a software install, but generally should not be needed by a running container in production.

https://mexicanpentester.com/2021/03/06/container-security-en-espanol/
