FROM	ubuntu

RUN		apt-get update \
		&& apt-get install -y \
			curl \
			openssh-server \
			ca-certificates \
			apt-transport-https \
			tzdata

RUN		curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash \
		&& apt-get install gitlab-ce \
		&& apt-get -y purge \
			curl \
		&& apt-get -y autoremove \
		&& apt-get autoclean

RUN		echo "external_url 'https://192.168.99.100'" \
			> /etc/gitlab/gitlab.rb \
		&& echo "nginx[ 'redirect_http_to_https' ] = true" \
			>> /etc/gitlab/gitlab.rb \
		&& echo "nginx[ 'ssl_certificate' ] = '/etc/gitlab/ssl/192.168.99.100.crt'" \
			>> /etc/gitlab/gitlab.rb \
		&& echo "nginx[ 'ssl_certificate_key' ] = '/etc/gitlab/ssl/192.168.99.100.key'" \
			>> /etc/gitlab/gitlab.rb \
		&& mkdir -p /etc/gitlab/ssl \
		&& chmod 700 /etc/gitlab/ssl \
		&& openssl req -new -x509 -days 365 -nodes \
			-out /etc/gitlab/ssl/192.168.99.100.crt \
			-keyout /etc/gitlab/ssl/192.168.99.100.key \
			-subj "/C=AU/ST=Some-State/L=Some-city/O=Some-Company/CN=Some-Unit"

EXPOSE	80 443 22

CMD		service ssh restart \
		&& (/opt/gitlab/embedded/bin/runsvdir-start &) \
		&& gitlab-ctl reconfigure \
		&& tail -f /dev/null

# docker run -it -p 8080:80 -p 8443:443 -p 8222:22 --privileged gitlab
# GIT_SSL_NO_VERIFY=true git clone https://192.168.99.100:8443/root/hello.git
# git clone ssh://git@192.168.99.100:8222/root/hello.git