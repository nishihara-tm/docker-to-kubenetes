FROM ubuntu:16.04
ENV LANG C.UTF-8

RUN echo "echo etc" >> /etc/profile
RUN echo "echo profile" >> ~/.profile

#for Ruby 
RUN apt-get update
RUN apt-get upgrade
RUN apt-get install git build-essential libssl-dev libreadline-dev curl libmysqlclient-dev mysql-client imagemagick -y

RUN git clone https://github.com/sstephenson/rbenv.git /usr/local/rbenv
RUN git clone https://github.com/sstephenson/ruby-build.git /usr/local/rbenv/plugins/ruby-build

RUN echo 'eval "$(rbenv init -)"' >> ~/.profile

WORKDIR /usr/local/rbenv/plugins/ruby-build
RUN ./install.sh


ENV PATH /usr/local/rbenv/bin:$PATH
ENV RBENV_ROOT /usr/local/rbenv

RUN echo 'export RBENV_ROOT=/usr/local/rbenv' >> /etc/profile.d/rbenv.sh \
&&  echo 'export PATH=/usr/local/rbenv/bin:$PATH' >> /etc/profile.d/rbenv.sh \
&&  echo 'eval "$(rbenv init -)"' >> /etc/profile.d/rbenv.sh


#WORKDIR /
RUN rbenv install 2.4.2
RUN rbenv global 2.4.2
RUN rbenv rehash

#RUN . /etc/profile
ENV ENV="/etc/profile"
#RUN eval "$(rbenv init -)"
#RUN echo 'eval "$(rbenv init -)"' >> ~/.bashrc

WORKDIR /tmp
ADD Gemfile Gemfile
ADD Gemfile.lock Gemfile.lock
RUN bash -l -c "gem environment"
RUN bash -l -c "gem install bundler && bundle install"


#for Node
RUN git clone git://github.com/nodenv/nodenv.git /usr/local/nodenv
RUN git clone https://github.com/nodenv/node-build.git /usr/local/nodenv/plugins/node-build

WORKDIR /usr/local/nodenv/plugins/node-build
RUN ./install.sh

WORKDIR /
ENV PATH /usr/local/nodenv/bin:$PATH
ENV NODENV_ROOT /usr/local/nodenv

RUN echo 'eval "$(nodenv init -)"' >> ~/.profile
RUN nodenv install 6.12.0
RUN nodenv global 6.12.0
RUN nodenv rehash
RUN eval "$(nodenv init -)"





ENV APP_HOME /myapp
RUN mkdir -p $APP_HOME
WORKDIR $APP_HOME
ADD . $APP_HOME
