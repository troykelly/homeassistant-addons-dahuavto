# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM
FROM $BUILD_FROM

ARG DAHUA_BRANCH="master"

# Execute during the build of the image
ARG TEMPIO_VERSION BUILD_ARCH
RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"

RUN apk add --no-cache --update python3 && \
apk add --no-cache --virtual .build-dependencies git && \
python3 -m ensurepip --upgrade

RUN git clone https://gitlab.com/elad.bar/DahuaVTO2MQTT.git --branch ${DAHUA_BRANCH} --depth 1 /app && \
pip3 install -r /app/requirements.txt && \
chmod +x /app/DahuaVTO.py && \
echo "{ \"version\": \"$(date +'%Y.%m.%d').$(( $(date +"%s") - $(date -d "$today 0" "+%s") ))\" }" > /app/data/version.json && \
apk del .build-dependencies

# Copy root filesystem
COPY rootfs /
