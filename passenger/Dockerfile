FROM phusion/passenger-nodejs

# create user
RUN apt-get update
RUN useradd -ms /bin/bash deploy
RUN echo deploy:105191102 | chpasswd
RUN echo 'deploy  ALL=(ALL:ALL) ALL' >> /etc/sudoers


RUN rm /etc/nginx/sites-enabled/default
ADD webapp.conf /etc/nginx/sites-enabled/webapp.conf

# install rbenv
RUN apt-get install -y libssl-dev libreadline-dev zlib1g-dev
ADD ./rbenv.sh /home/deploy/rbenv.sh
RUN su - deploy -c "/bin/bash /home/deploy/rbenv.sh"

# Enable nginx & ssh
RUN rm -f /etc/service/nginx/down
RUN rm -f /etc/service/sshd/down

EXPOSE 80 22
ENV HOME /root
CMD ["/sbin/my_init"]
