FROM alpine:3.16

RUN apk update \
      && apk add --no-cache \
          make build-base cmake git python3 bash doas \
          gcc-arm-none-eabi newlib-arm-none-eabi \
          libc-dev bsd-compat-headers libusb-dev

RUN adduser -D -k /dev/null -s /bin/bash -u 1000 viny

COPY doas.conf /etc/doas.d/doas.conf

# Install Pico SDK with user 
USER viny

ENV PICO_SDK_PATH=/home/viny/pico/pico-sdk
ENV PICO_PLATFORM=rp2040

RUN mkdir /home/viny/pico
WORKDIR /home/viny/pico

RUN git clone -b master https://github.com/raspberrypi/pico-sdk \
      && cd pico-sdk && git submodule update --init

RUN git clone -b master https://github.com/raspberrypi/pico-extras \
      && cd pico-extras && git submodule update --init

# SDK examples
RUN git clone -b master https://github.com/raspberrypi/pico-examples

# Tools
RUN git clone -b master https://github.com/raspberrypi/picotool \
      && cd picotool \
      && mkdir build && cd build \
      && cmake .. && make -j

RUN git clone -b master https://github.com/raspberrypi/picoprobe

# Install tools under /user/local/bin (to avoid to be required to type full path when using doas)
USER root
RUN cp /home/viny/pico/picotool/build/picotool /usr/local/bin \
     && chown root:root /usr/local/bin/picotool

# Last switch to user
USER viny
WORKDIR /home/viny
