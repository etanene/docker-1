FROM	debian

RUN		apt-get update && apt-get install -y \
		wget \
		bzip2

WORKDIR	/home/
RUN		wget https://files.teamspeak-services.com/releases/server/3.7.0/teamspeak3-server_linux_amd64-3.7.0.tar.bz2 \
		&& mkdir ts3server \
		&& tar -xvf teamspeak3-server_linux_amd64-3.7.0.tar.bz2 -C ts3server \
		&& rm -rf teamspeak3-server_linux_amd64-3.7.0.tar.bz2

WORKDIR	/home/ts3server/
RUN		touch .ts3server_license_accepted \
		&& chmod 755 ts3server_minimal_runscript.sh \
		&& chmod 755 ts3server_startscript.sh \
		&& chmod 755 ts3server

ENTRYPOINT	./ts3server_startscript.sh
CMD			start