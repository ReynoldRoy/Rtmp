# Rtmp

sudo apt-get update
sudo apt-get upgrade
install nginx
sudo apt-get install nginx -y
sudo apt-get install libnginx-mod-rtmp -y
Edit nginx.conf
sudo nano /etc/nginx/nginx.conf

Add to the end of nginx config
rtmp {
        server {
                listen 1935;
                chunk_size 4096;

                application live {
                        live on;
                        record off;
                        push rtmp://127.0.0.1:1936/rtmp/<<Facebook persistent stream key >>;

                }
        }
}
restart nginx
sudo systemctl restart nginx


sudo apt install ffmpeg

video streamimg
ffmpeg -re -i a.mp4 -acodec libmp3lame -ar 44100 -b:a 128k -pix_fmt yuv420p -profile:v baseline -s 426x240 -bufsize 6000k -vb 400k -maxrate 1500k -deinterlace -vcodec libx264 -preset veryfast -g 30 -r 30 -f flv -flvflags no_duration_filesize  rtmp:192.168.1.9/live/bb213
