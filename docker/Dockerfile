FROM ruby:2.7.0

RUN apt-get update -qq
RUN apt-get install -y build-essential libpq-dev curl default-libmysqlclient-dev
RUN curl -sL https://deb.nodesource.com/setup_13.x | bash -
RUN apt-get install -y nodejs
RUN npm install npm@latest -g
RUN npm install yarn -g

RUN CHROME_DRIVER_VERSION=`curl -sS chromedriver.storage.googleapis.com/LATEST_RELEASE` && \
    wget -N http://chromedriver.storage.googleapis.com/$CHROME_DRIVER_VERSION/chromedriver_linux64.zip -P ~/ && \
    unzip ~/chromedriver_linux64.zip -d ~/ && \
    rm ~/chromedriver_linux64.zip && \
    mv ~/chromedriver /usr/bin/chromedriver && \
    sh -c 'wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -' && \
    sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list' && \
    apt-get update && apt-get install -y google-chrome-stable

ENV APP_ROOT /rails_app
RUN mkdir $APP_ROOT
WORKDIR $APP_ROOT

ADD ./Gemfile Gemfile
ADD ./Gemfile.lock Gemfile.lock

RUN bundle config set path 'vendor/bundle' && \
    bundle install
RUN yarn install

ADD . $APP_ROOT
