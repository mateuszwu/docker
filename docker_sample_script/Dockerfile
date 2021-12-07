FROM ruby:2.5.1-slim
COPY . /app
WORKDIR /app
RUN apt-get update \
  && apt-get install -y \
     build-essential \
     patch \
     ruby-dev \
     libxml2-dev \
     libxslt-dev \
  && apt-get clean
RUN gem install pkg-config -v "~> 1.1"
RUN bundle config build.nokogiri --use-system-libraries
RUN bundle
CMD ruby sample_script.rb
