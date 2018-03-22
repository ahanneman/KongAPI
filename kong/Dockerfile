FROM kong

# get ContainerPilot release
ENV CONTAINERPILOT_VERSION 2.7.2
RUN export CP_SHA1=e886899467ced6d7c76027d58c7f7554c2fb2bcc \
    && curl -Lso /tmp/containerpilot.tar.gz \
         "https://github.com/joyent/containerpilot/releases/download/${CONTAINERPILOT_VERSION}/containerpilot-${CONTAINERPILOT_VERSION}.tar.gz" \
    && echo "${CP_SHA1}  /tmp/containerpilot.tar.gz" | sha1sum -c \
    && tar zxf /tmp/containerpilot.tar.gz -C /bin \
    && rm /tmp/containerpilot.tar.gz

# add ContainerPilot configuration
COPY containerpilot.json /etc/containerpilot.json
ENV CONTAINERPILOT=file:///etc/containerpilot.json

# kong config
COPY kong.conf /etc/kong/kong.conf
CMD /bin/containerpilot kong start --conf ./etc/kong/kong.conf

# copy over custom plugin for syslog
#RUN mkdir /usr/local/share/lua/5.1/kong/plugins/stdout-log
#COPY ./plugins/stdout-log/handler.lua /usr/local/share/lua/5.1/kong/plugins/stdout-log
#COPY ./plugins/stdout-log/scema.lua /usr/local/share/lua/5.1/kong/plugins/stdout-log

EXPOSE 8000 8443 8001 7946