FROM fedora:31

LABEL summary="The open-vm-tools guest agent" \
      io.k8s.description="The open-vm-tools agent is providing information about the virtual machine and allows to restart / shutdown the machine via VMware products. This image is intended to be used with virtual machines running Centos Atomic Host." \
      io.k8s.display-name="open-vm-tools guest agent" \
      architecture="x86_64" \
      BZComponent="open-vm-tools" \
      maintainer="davis phillips <dphillip@redhat.com>"

ENV SYSTEMD_IGNORE_CHROOT=1
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en

RUN dnf -y --setopt=tsflags=nodocs --setopt=override_install_langs=en_US.utf8 --setopt=install_weak_deps=False install file open-vm-tools net-tools iproute systemd -x gcc && \ 
dnf clean all 

COPY service.template config.json.template /exports/

LABEL RUN="docker run  --privileged -v /proc/:/hostproc/ -v /sys/fs/cgroup:/sys/fs/cgroup  -v /var/log:/var/log -v /run/systemd:/run/systemd -v /sysroot:/sysroot -v=/var/lib/sss/pipes/:/var/lib/sss/pipes/:rw -v /etc/passwd:/etc/passwd -v /etc/shadow:/etc/shadow -v /tmp:/tmp:rw -v /etc/sysconfig:/etc/sysconfig:rw -v /etc/resolv.conf:/etc/resolv.conf:rw -v /etc/nsswitch.conf:/etc/nsswitch.conf:rw -v /etc/hosts:/etc/hosts:rw -v /etc/hostname:/etc/hostname:rw -v /etc/localtime:/etc/localtime:rw -v /etc/adjtime:/etc/adjtime --env container=docker --net=host  --pid=host IMAGE"

CMD /usr/bin/vmtoolsd
