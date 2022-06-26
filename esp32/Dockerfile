FROM debian:bullseye-slim

RUN apt-get update \
      && DEBIAN_FRONTEND=noninteractive apt-get install --yes --no-install-recommends \
            vim git wget \
            flex bison gperf python3 python3-venv cmake make \
            ninja-build ccache libffi-dev libssl-dev dfu-util libusb-1.0-0

RUN useradd --create-home --shell /bin/bash --uid 1000 viny

# Install ESP-IDF SDK with user 
USER viny

ENV LANG=C.UTF-8
ENV ESP_PATH=/home/viny/esp-idf

WORKDIR /home/viny

RUN git clone --recursive https://github.com/espressif/esp-idf.git \
      && cd esp-idf && ./install.sh esp32 \
      && echo "source /home/viny/esp-idf/export.sh" >> /home/viny/.bashrc

# Last switch to user
USER viny
WORKDIR /home/viny
