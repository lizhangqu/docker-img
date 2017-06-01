FROM java:8-jdk

MAINTAINER Zhangqu Li <lizhangqu@weidian.com>

ENV DEBIAN_FRONTEND noninteractive

# install dependencies
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

# Download and untar SDK
ENV ANDROID_SDK_URL http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz
RUN curl -L "${ANDROID_SDK_URL}" | tar --no-same-owner -xz -C /usr/local

# set env
ENV ANDROID_HOME /usr/local/android-sdk-linux
ENV ANDROID_SDK /usr/local/android-sdk-linux
ENV PATH ${ANDROID_HOME}/tools:$ANDROID_HOME/platform-tools:$PATH

# install Android SDK components

COPY android_sdk_components.env /android_sdk_components.env
RUN (while :; do echo 'y'; sleep 3; done) | android update sdk --no-ui --all --filter "$(cat /android_sdk_components.env)"

# download gradle 
RUN wget http://downloads.gradle.org/distributions/gradle-2.11-all.zip
RUN mkdir -p /usr/local/gradle
RUN unzip gradle-2.11-all.zip -d /usr/local/gradle
RUN rm gradle-2.11-all.zip
ENV GRADLE_HOME /usr/local/gradle/gradle-2.11
ENV PATH $GRADLE_HOME/bin:$PATH

# support gradle
ENV TERM dumb
