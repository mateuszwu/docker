FROM ruby:2.5.1

ENV BUNDLER=1.16.2
ENV NODE_VERSION=14.16.0

RUN apt-get update -qq && \
  apt-get install -y \
    wget \
    # ca-certificates \
    # apt-transport-https \
    lsb-release && \
    # update-ca-certificates && \
    sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list' && \
    wget --no-check-certificate -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
RUN apt-get update -qq && \
  apt-get install -y \
    build-essential \
    libpq5 \
    postgresql-client-11
RUN wget http://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.xz
RUN tar -xJvf node-v$NODE_VERSION-linux-x64.tar.xz -C /usr/bin
ENV PATH "$PATH:/usr/bin/node-v$NODE_VERSION-linux-x64/bin/"

RUN rm -f node-v$NODE_VERSION-linux-x64.tar.xz

WORKDIR /app

COPY Gemfile ./Gemfile
COPY Gemfile.lock ./Gemfile.lock
RUN gem install bundler:${BUNDLER}
RUN bundle lock --add-platform mingw, mswin, x64_mingw, jruby
RUN bundle config --local disable_platform_warnings true
RUN bundle install

COPY . /app

CMD ["rails", "s", "-p", "3000", "-b", "0.0.0.0"]
