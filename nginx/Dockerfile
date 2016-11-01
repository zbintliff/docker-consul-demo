FROM centos:6

ENV CONSUL_TEMPLATE_VERSION=0.16.0

ADD http://nginx.org/packages/rhel/6/x86_64/RPMS/nginx-1.8.1-1.el6.ngx.x86_64.rpm /tmp/

RUN yum install -y initscripts && \
    rpm -ivh /tmp/nginx-1.8.1-1.el6.ngx.x86_64.rpm && \
    rm /tmp/nginx-1.8.1-1.el6.ngx.x86_64.rpm


ADD https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip /

RUN yum install -y unzip && \
  unzip /consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip \
   && mv /consul-template /usr/local/bin/consul-template \
   && rm -rf /consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip

RUN mkdir -p /etc/consul-template/config.d /etc/consul-template/template.d

ADD consul.cfg /etc/consul-template/config.d/consul.cfg
ADD nginx-consul.cfg /etc/consul-template/config.d/nginx.cfg
ADD nginx.tmpl /etc/consul-template/template.d/nginx.tmpl
ADD launch.sh /launch.sh

EXPOSE 80

CMD ["/launch.sh"]
