# PowerMeter-server

OS-> raspbian lite

sudo apt-get update
sudo apt-get upgrade
enable ssh
192.168.1.200

Install docker
  https://phoenixnap.com/kb/docker-on-raspberry-pi
  
Run influxdb on docker
  docker pull influxdb:1.8
  docker run -d --volume=/var/influxdb:/data -p 8086:8086 influxdb:1.8
  
Run grafana
  docker pull grafana/grafana
  docker run -d -p 3000:3000 grafana/grafana
  
created db
  using influx cli
    create database powermeter
    insert current, host=diferencial value=0.1
    insert current, host=diferencial value=0.2 <timestamp>
add data using curl
  curl -i -XPOST 'http://192.168.1.200:8086/write?db=powermeter' --data-binary 'current,host=diferencial value=0.64'
  curl -i -XPOST 'http://192.168.1.200:8086/write?db=powermeter' --data-binary 'current,host=diferencial value=0.5 <timestamp>'
