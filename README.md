dvgamer/ums:6.6.0 [![Build Status](https://travis-ci.org/dvgamer/docker-ums.svg?branch=6.6.0)](https://travis-ci.org/dvgamer/docker-ums)
============

Introduction
-------------
Dockerfile to build a [Universal Media Server](http://www.universalmediaserver.com/) (UMS) container image. based on ubuntu:16.04  
README is written in Thai Only.


Installation
--------------
	$ mkdir -p /ums && cd /ums

	$ git clone https://github.com/dvgamer/docker-ums.git .
	
	$ docker build -t dvgamer/ums .
	   or
	$ docker-compose up -d

Quick Start
--------------

Example usage:

	$ docker run -d --net=host --restart=always \
	  -p 5001:5001 -p 9001:9001 \
	  -v /path/to/your/mediavolume:/media \
	  --name ums dvgamer/ums

หรือถ้า interface `eth0` ไม่ใช่ค่าพื้นฐานของระบบ:

	$ docker run -d --net=host --restart=always \
	  -p 5001:5001 -p 9001:9001 \
	  -v /anime:/media \
	  -e X_UMS_NETWORK_INTERFACES=ens33
	  --name ums dvgamer/ums

ตั้งค่า Interface ได้จาก env `X_UMS_NETWORK_INTERFACES`

คุณสามารถแก้ไขไฟล์ `docker-compose` ได้เลยหากต้องการเปลี่ยนแปลงการตั้งค่า

Restriction
--------------
- การใช้งานบน PlayStation 3 or 4 อาจจะจำเป็นต้องเพิ่งการตั้งค่าเล็กน้อยเพื่อให้สามารถรับรองการใช้งานของ PlayStation ได้
- การลบการตั้งค่าบางตัวของ `UMS.conf` ไม่ได้ืำให้เกิดปัญหาในการืำงานแต่อย่างใด เนื่อจากระบบมีการกำหนดค่าพื้นฐานให้อยู่แล้ว


Configuration
--------------
การตั้งค่าใหม่ให้กับ `UMS.conf` และ `WEB.conf` เช่น

	docker run -d \
	  -v /path/to/your/mediavolume:/media \
	  -v /path/to/yourhost/conf:/srv/ums/conf \  # <--this line
	  --name ums exlair/ums:6.5.0


### Available Configuration Parameters
Below is the list of parameters that can be set using environment variables.

* **X_UMS_FOLDERS**: default "`/media`"
* **X_UMS_NETWORK_INTERFACES**: default "`eth0`"
* **X_UMS_SKIP_NETWORK_INTERFACES**: default "`tap,vmnet,vnic`"
* **X_UMS_ENGINES**: default "`ffmpegvideo,mencoder,tsmuxer,ffmpegaudio,tsmuxeraudio,ffmpegwebvideo,vlcwebvideo,vlcvideo,mencoderwebvideo,vlcaudio,ffmpegdvrmsremux,rawthumbs`"


References
--------------
- [Universal Media Server](http://www.universalmediaserver.com/) - Official site
	- [UniversalMediaServer/INSTALL.txt at master · UniversalMediaServer/UniversalMediaServer · GitHub](https://github.com/UniversalMediaServer/UniversalMediaServer/blob/master/INSTALL.txt)
	- [UniversalMediaServer/UMS.conf at master · UniversalMediaServer/UniversalMediaServer · GitHub](https://github.com/UniversalMediaServer/UniversalMediaServer/blob/master/src/main/external-resources/UMS.conf)
- [progrium/entrykit: Entrypoint tools for elegant, programmable containers][entrykit]


[entrykit]: https://github.com/progrium/entrykit "progrium/entrykit: Entrypoint tools for elegant, programmable containers"
