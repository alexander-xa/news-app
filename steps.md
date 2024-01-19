RUN apt install -y default-jdk
RUN apt install -y default-jre
RUN apt-get install -y libc6-dev-i386 lib32z1
RUN apt-get install -y wget
RUN cd /flutter/bin
RUN mkdir android-sdk
RUN cd android-sdk
RUN wget https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip
RUN unzip commandlinetools-linux-11076708_latest.zip
RUN cmdline-tools/bin/sdkmanager --update --sdk_root=.
RUN cmdline-tools/bin/sdkmanager "platforms;android-25" "build-tools;25.0.2" "extras;google;m2repository" "extras;android;m2repository" --sdk_root=.
RUN y | cmdline-tools/bin/sdkmanager --licenses --sdk_root=.
ENV ANDROID_SDK_ROOT=/flutter/bin/android-sdk
ENV PATH=$PATH:$ANDROID_SDK_ROOT/tools
RUN apt install -y python3
RUN apt install -y python3.11-venv