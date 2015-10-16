FROM phusion/passenger-nodejs

# create user
RUN apt-get update
RUN useradd -ms /bin/bash deploy
RUN echo deploy:105191102 | chpasswd
RUN echo 'deploy  ALL=(ALL:ALL) ALL' >> /etc/sudoers

RUN su - deploy -c "cd && mkdir .ssh"
ADD config /home/deploy/.ssh/config
RUN chown deploy:deploy /home/deploy/.ssh/config

RUN rm /etc/nginx/sites-enabled/default
ADD webapp.conf /etc/nginx/sites-enabled/webapp.conf

# set locale utf8
RUN su - deploy -c "echo 'export LC_ALL=en_US.UTF-8' >> /home/deploy/.bash_profile"
RUN su - deploy -c "echo 'export LANG=en_US.UTF-8' >> /home/deploy/.bash_profile"
RUN su - deploy -c "echo 'export LANGUAGE=en_US.UTF-8' >> /home/deploy/.bash_profile"

# install rbenv
RUN apt-get install -y libssl-dev libreadline-dev zlib1g-dev
ADD ./rbenv.sh /home/deploy/rbenv.sh
RUN su - deploy -c "/bin/bash /home/deploy/rbenv.sh"
RUN sed -i 's|/usr/bin/ruby|/home/deploy/.rbenv/shims/ruby|g' /etc/nginx/nginx.conf

# install mysql
RUN apt-get install -y --force-yes mysql-client libmysqlclient-dev
# install sqlite
RUN apt-get install -y --force-yes sqlite3 libsqlite3-dev

# Enable nginx & ssh
RUN rm -f /etc/service/nginx/down
RUN rm -f /etc/service/sshd/down

EXPOSE 80 22
ENV HOME /root
CMD ["/sbin/my_init"]
