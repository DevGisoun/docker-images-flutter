FROM ghcr.io/devgisoun/android-sdk:35

LABEL org.opencontainers.image.source=https://github.com/DevGisoun/docker-images-flutter
USER root

ARG flutter_version

ENV FLUTTER_HOME=${HOME}/sdks/flutter \
    FLUTTER_VERSION=$flutter_version
ENV FLUTTER_ROOT=$FLUTTER_HOME

ENV PATH=${PATH}:${FLUTTER_HOME}/bin:${FLUTTER_HOME}/bin/cache/dart-sdk/bin

# stable을 포함한 $FLUTTER_VERSION 에 해당하는 버전의 Flutter SDK 설치.
RUN git clone --depth 1 --branch ${FLUTTER_VERSION} https://github.com/flutter/flutter.git ${FLUTTER_HOME}

# stable 버전을 설치하여 $FLUTTER_VERSION 에 해당하는 버전으로 변경.
# 이미지 설치 후 컨테이너 내에서 Flutter 버전 변경 필요 시 해당 스크립트를 사용. 
# RUN git clone --branch stable https://github.com/flutter/flutter.git ${FLUTTER_HOME} \
#     && if [ "$FLUTTER_VERSION" != "stable" ]; then \
#         cd ${FLUTTER_HOME} && git checkout ${FLUTTER_VERSION}; \
#     fi

RUN yes | flutter doctor --android-licenses \
    && flutter doctor \
    && chown -R root:root ${FLUTTER_HOME}

RUN flutter precache --android