From rockylinux/rockylinux

RUN yum -y install openssh-server ed openssh-clients tlog glibc-langpack-en && yum clean all && systemctl enable sshd;
RUN sed -i 's/#Port.*$/Port 2022/' /etc/ssh/sshd_config && chmod 775 /var/run && rm -f /var/run/nologin
RUN mkdir /etc/systemd/system/sshd.service.d/ && echo -e '[Service]\nRestart=always' > /etc/systemd/system/sshd.service.d/sshd.conf

RUN adduser --system -s /bin/bash -u 1001 tester && \ #UID matching user uid on host
           adduser --system -s /usr/bin/tlog-rec-session -u 1000 tester2 && \
           adduser --system -s /usr/bin/tlog-rec-session -u 1002 tester3 -p y5utxaxUDNFII && \
           mkdir -p /home/tester/.ssh /home/tester2/.ssh /home/tester3/.ssh

RUN touch /home/tester/.ssh/authorized_keys /home/tester2/.ssh/authorized_keys /home/tester3/.ssh/authorized_keys && \
           chmod 700 /home/tester/.ssh /home/tester2/.ssh /home/tester3/.ssh && \
           chmod 600 /home/tester/.ssh/authorized_keys /home/tester2/.ssh/authorized_keys /home/tester3/.ssh/authorized_keys && \
           sed -i 's/1001/0/g' /etc/passwd && \ #Update UID with root UID
           echo ${ADMIN_PUBLIC_KEY} >> /home/tester/.ssh/authorized_keys && \
           echo ${TESTER2_PUBLIC_KEY} >> /home/tester2/.ssh/authorized_keys && \
           chown -R tester2:tester2 /home/tester2/ && chown -R tester3:tester3 /home/tester3/ && chown -R tester:tester /home/tester
Expose 2022