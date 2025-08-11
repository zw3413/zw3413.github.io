FROM postgres:17

ENV PG_APP_HOME="/etc/docker-postgresql" \
    PG_VERSION=17 \
    PG_USER=postgres \
    PG_HOME=/var/lib/postgresql/17 \
    PG_RUNDIR=/run/postgresql \
    PG_LOGDIR=/var/log/postgresql \
    PG_CERTDIR=/etc/postgresql/certs \
    ORAFCE_VERSION=4_14_4 \
    PLDEBUGGER_VERSION=1.5 \
    POSTGRES_PASSWORD=postgres \
    PGDATA=/var/lib/postgresql/data \
    PATH=$PATH:/var/lib/postgresql/bin \
    POSTGRES_HOST_AUTH_METHOD=password

RUN apt  -y update \ 
&& apt install -y make wget gcc postgresql-server-dev-17  postgresql-17-pldebugger vim


#COPY ./pg_hba.conf /${PGDATA}/pg_hba.conf
 
#install 4_10_3 postgresql-15-orafce
RUN cd /tmp \ 
&&  wget  https://codeload.github.com/orafce/orafce/tar.gz/refs/tags/VERSION_${ORAFCE_VERSION} -O orafce.tar.gz \
&& tar xvzf orafce.tar.gz \
&& mv /tmp/orafce-VERSION_${ORAFCE_VERSION} /usr/share/postgresql/17/extension/ 

RUN cd /usr/share/postgresql/17/extension/orafce-VERSION_${ORAFCE_VERSION} \
&& make \
&& make install 


VOLUME /var/lib/postgresql/data

ENTRYPOINT ["docker-entrypoint.sh"]
EXPOSE 5432
CMD ["postgres"]



# build and start pg17 with orafce
# docker build -t pg17_orafce .
# docker run -d -p 5432:5432 --name=pg17_orafce pg17_orafce

# start pure pg17
# docker run -d -p 5433:5432 --name=pg17 -e POSTGRES_PASSWORD=postgres postgres:17
