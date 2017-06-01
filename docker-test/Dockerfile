FROM java:8-jdk

ENV DEBIAN_FRONTEND noninteractive

# Install dependencies
RUN dpkg --add-architecture i386 && \
    apt-get update && \
    apt-get install -yq libstdc++6:i386 zlib1g:i386 libncurses5:i386 --no-install-recommends && \
    apt-get -y install --reinstall locales && \
    apt-get install -y git curl zip vim&& \
    dpkg-reconfigure locales && \
    echo 'ja_JP.UTF-8 UTF-8' >> /etc/locale.gen && \
    locale-gen ja_JP.UTF-8 && \
    localedef --list-archive && locale -a &&  \
    update-locale &&  \
    apt-get clean

ENV TERM dumb

# add a user
RUN useradd -d /home/lizhangqu lizhangqu -m
RUN echo "lizhangqu:lizhangqu" | chpasswd  
RUN echo "lizhangqu   ALL=(ALL)       ALL" >> /etc/sudoers 


# git 
USER lizhangqu
RUN mkdir /home/lizhangqu/.git
RUN git config --global user.name "lizhangqu"
RUN git config --global user.email "lizhangqu@weidian.com"
RUN ssh-keygen -t rsa -f /home/lizhangqu/.ssh/id_rsa

User lizhangqu
RUN touch /home/lizhangqu/trace.log
ENTRYPOINT ["tail", "-f", "/home/lizhangqu/trace.log"]
