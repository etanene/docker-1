FROM	debian

RUN		apt-get update && apt-get install -y \
		wget \
		bzip2

WORKDIR	/home/
RUN		wget https://files.teamspeak-services.com/releases/server/3.7.0/teamspeak3-server_linux_amd64-3.7.0.tar.bz2 \
		&& tar -xvf teamspeak3-server_linux_amd64-3.7.0.tar.bz2 \
		&& rm -rf teamspeak3-server_linux_amd64-3.7.0.tar.bz2 \
		&& apt-get -y purge \
		wget \
		bzip2 \
		&& apt-get -y autoremove  \
		&& apt-get autoclean

WORKDIR	/home/teamspeak3-server_linux_amd64/
RUN		touch .ts3server_license_accepted \
		&& chmod 755 ts3server_minimal_runscript.sh \
		&& chmod 755 ts3server_startscript.sh \
		&& chmod 755 ts3server

EXPOSE	9987/udp 30033 10011

CMD		["./ts3server_minimal_runscript.sh"]
