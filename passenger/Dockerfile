FROM phusion/passenger-ruby22

# create user
RUN apt-get update
RUN useradd -ms /bin/bash deploy
RUN echo deploy:105191102 | chpasswd
RUN echo 'deploy  ALL=(ALL:ALL) ALL' >> /etc/sudoers


RUN rm /etc/nginx/sites-enabled/default
ADD webapp.conf /etc/nginx/sites-enabled/webapp.conf

# Enable nginx & ssh
RUN rm -f /etc/service/nginx/down
RUN rm -f /etc/service/sshd/down

EXPOSE 80 22
ENV HOME /root
CMD ["/sbin/my_init"]
