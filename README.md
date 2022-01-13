# Stream-games-with-pc-and-laptop
Stream Games on PC then use Laptop to have high resolution and quality


# Requirements
  - Nginx 1.7.11.3 Gryphon.zip (http://nginx-win.ecsds.eu/download/nginx%201.7.11.3%20Gryphon.zip) 
  - OBS both PC and Laptop (https://cdn-fastly.obsproject.com/downloads/OBS-Studio-27.1.3-Full-Installer-x64.exe)
  - VLC for stream test (https://get.videolan.org/vlc/3.0.16/win64/vlc-3.0.16-win64.exe)
  
  
## Extract Nginx

## Create Bat file inside and save as start.bat and stop.bat
```
# start.bat
@echo off
nginx.exe -s quit
start nginx.exe

# stop.bat
@echo off
nginx.exe -s quit

```

## Create configuration file nginx.conf
```
#user  nobody;
# multiple workers works !
worker_processes  2;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
	worker_connections  8192;
	# max value 32768, nginx recycling connections+registry optimization = 
	#   this.value * 20 = max concurrent connections currently tested with one worker
	#   C1000K should be possible depending there is enough ram/cpu power
	# multi_accept on;
}

rtmp {
	server {
		listen 1935;
		chunk_size 4096;

		application live {
			live on;

			record off;
			# record all;
			# record_path /recordings;

			# To push to multiple platforms, uncomment lines below and substitute in your RTMP URI and stream key
      # Dont enable this to your gaming unit
      # This must be enabled to your streaming unit if you desired to multi platform streaming like fb, twitch, youtube
			# push rtmp://server/path/streamkey;
			# push rtmp://server/path/streamkey;

			# HLS options below
			#hls on;
			#hls_path /http/directory/;
			#hls_fragment 3;
			#hls_playlist_length 60;
			#hls_continuous on;
		}
	}
}

```


# To learn more about multi platform streaming
Tutorial (https://github.com/ohmcodes/Multistream-WSL-Ubuntu-Stunnel4-Nginx-OBS-Win10)

# Run start.bat or to stop run stop.bat

# Configure OBS

