FROM bitnami/ruby:2.7.8

ENV LANG=en_us.UTF-8
ENV LC_ALL=C.UTF-8
ENV RACK_ENV=production

RUN apt-get update \
&& apt-get install libpq-dev zlib1g-dev -y \
&& rm -rf /var/lib/apt/lists/*

RUN gem install sinatra \
&& gem install redis

RUN gem install pg \
&& gem install aws-sdk-dynamodb pg

COPY yelb-appserver.rb yelb-appserver.rb 
COPY Gemfile Gemfile
COPY modules modules

ENV REDIS_SERVER_ENDPOINT=redis-server
ENV YELB_DB_SERVER_ENDPOINT=yelb-db
ENV YELB_DB_SERVER_PORT=5432
ENV YELB_DB_NAME=yelbdatabase
ENV YELB_DB_NAME=postgres

EXPOSE 4567

CMD ["ruby", "/app/yelb-appserver.rb", "-o", "0.0.0.0"]
