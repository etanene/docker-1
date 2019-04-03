FROM	ruby

RUN		gem install rails \
		&& apt-get update \
		&& apt-get install nodejs -y \
		&& apt-get autoclean

ONBUILD COPY	app/ /opt/app
ONBUILD WORKDIR /opt/app
ONBUILD RUN		bundle install \
				&& rake db:migrate \
				&& rake db:seed