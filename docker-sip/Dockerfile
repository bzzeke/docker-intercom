FROM raspbian/stretch:latest

ENV DEBIAN_FRONTEND noninteractive

WORKDIR /app
RUN apt-get update && apt-get --assume-yes install python python-pip supervisor libasound2 libv4l-0 libx11-6 libxv1 libtheora0 python-opencv python-rpi.gpio

RUN apt-get install --assume-yes git
ADD config /etc/

RUN git clone https://github.com/bzzeke/intercom.git /app/intercom
RUN rm -fr /app/intercom/.git
RUN pip install /app/intercom/lib/linphone4raspberry-3.11.1_1_g79a8f905c-cp27-none-any.whl
RUN chmod 755 /app/intercom/intercom.py
RUN mkdir /app/snapshots

ENTRYPOINT ["supervisord", "--nodaemon", "--configuration", "/etc/supervisord/supervisord.conf"]
