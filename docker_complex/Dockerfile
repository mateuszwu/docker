FROM ruby:2.5.1

ENV BUNDLER=1.16.2
ENV NODE_VERSION=14.16.0

COPY . /app

WORKDIR /app

RUN apt-get update && apt-get install -y wget build-essential libpq5 postgresql-client
RUN wget http://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.xz
RUN tar -xJvf node-v$NODE_VERSION-linux-x64.tar.xz -C /usr/bin
RUN rm -f node-v$NODE_VERSION-linux-x64.tar.xz
ENV PATH "$PATH:/usr/bin/node-v$NODE_VERSION-linux-x64/bin/"
RUN gem install bundler:${BUNDLER}
RUN bundle lock --add-platform mingw, mswin, x64_mingw, jruby
RUN bundle config --local disable_platform_warnings true
# RUN bundle install
# RUN bin/rake assets:precompile
EXPOSE 3000

CMD ["rails", "s", "-p", "3000", "-b", "0.0.0.0"]
