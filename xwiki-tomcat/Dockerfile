FROM tomcat:8-jre8
MAINTAINER Denis GERMAIN <dt.germain@gmail.com> 
ENV POSTGRES_INSTANCE=xwiki-pgsql
ENV POSTGRES_PORT=5432
ENV POSTGRES_DB=xwiki
ENV POSTGRES_USER=xwiki
ENV POSTGRES_PASSWORD=xwiki

COPY setenv.sh bin/setenv.sh
COPY xwiki-tomcat-entrypoint.sh /

RUN sed -i "s/redirectPort=\"8443\" /redirectPort=\"8443\" URIEncoding=\"UTF-8\" /" conf/server.xml

RUN rm -rf webapps/* && \
    curl -L \
      'http://download.forge.ow2.org/xwiki/xwiki-enterprise-web-8.4.1.war' \
       -o xwiki.war && \
    unzip -d webapps/xwiki xwiki.war && \
    sed "s/<id>org.xwiki.enterprise:xwiki-enterprise-web/<id>org.xwiki.enterprise:xwiki-enterprise-docker-zwindler/" < webapps/xwiki/META-INF/extension.xed > webapps/xwiki/META-INF/extension2.xed && \
    mv webapps/xwiki/META-INF/extension2.xed webapps/xwiki/META-INF/extension.xed && \
    rm -f xwiki.war

RUN curl -L \
      'https://jdbc.postgresql.org/download/postgresql-9.4.1208.jar' \
      -o 'webapps/xwiki/WEB-INF/lib/postgresql-9.4-1208.jdbc42.jar' && \
    echo "environment.permanentDirectory=/usr/local/tomcat/work/xwiki" >> webapps/xwiki/WEB-INF/xwiki.properties

COPY hibernate.cfg.xml webapps/xwiki/WEB-INF/
COPY xwiki.cfg webapps/xwiki/WEB-INF/

VOLUME /usr/local/tomcat/work/xwiki

ENTRYPOINT ["/xwiki-tomcat-entrypoint.sh"]
