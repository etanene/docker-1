FROM	ruby

RUN		gem install rails \
		&& apt-get update \
		&& apt-get install nodejs -y \
		&& apt-get autoclean

ONBUILD COPY	app1/ /opt/app
ONBUILD WORKDIR /opt/app
ONBUILD RUN		bundle install \
				&& bundle exec rake db:migrate \
				&& bundle exec rake db:seed