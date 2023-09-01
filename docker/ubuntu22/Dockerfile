FROM ubuntu:22.04
RUN apt-get update
RUN apt upgrade -y
# ip ping nslookup traceroute
RUN apt install iproute2 iputils-ping bind9-dnsutils traceroute -y
RUN apt install cron -y
RUN apt install curl git less unzip vim wget -y
RUN apt install sudo -y
RUN apt install gpg -y
RUN apt install lsb-release -y
RUN apt install bash-completion -y
