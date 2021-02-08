#
# This is a quick Dockerfile to build and run the
# WeatherFlow UDP listener via a Docker container.
#

FROM python:3.9.1-slim
RUN apt-get update \
    && apt-get install -y wget \
    && pip3 install influxdb paho-mqtt \
    && apt-get clean autoclean \
    && apt-get autoremove --yes \
    && rm -rf /var/lib/{apt,dpkg,cache,log}/

#--- to download a verbatim copy of the latest on github
RUN cd /root && wget https://raw.githubusercontent.com/vinceskahan/weatherflow-udp-listener/master/listen.py

#--- or to copy in an edited one from this directory
# ADD listen.py /root/listen.py

# uncertain if this is needed
EXPOSE 50222/udp

# run it for real, publishing known observations only

ENTRYPOINT ["python", "/root/listen.py", "-r", "--influxdb", "--influxdb_host=influxdb", "--influxdb_port=8086", "--influxdb_db=weatherflow"]
