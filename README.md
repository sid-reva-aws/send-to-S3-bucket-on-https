# send-to-S3-bucket-on-https
Send to S3 bucket on HTTPS website file upload
Deploy Flask app on EC2 using gunicorn WSGI HTTP server downloading the github package

Install gunicorn:
pip3 install gunicorn

run gunicorn:
gunicorn --bind 0.0.0.0:8000 library_site:app

Create a systemd Unit file under /etc/systemd/system:
sudo nano /etc/systemd/system/flaskapp.service

Unit file has different section. In this example we need Unit, Service and Install sections.
[Unit] section is used for defining metadata and dependencies.
[Service] section is used for specifying configurations. You can define user and group that the process will be run under.
[Install] section is used to define the behavior of a unit if it is disabled or enabled.
We tell the init system to only start this after the networking target has been reached with After=network.target .
We will define www-data group so that it can communicate easily with the Gunicorn processes.

start and enable Gunicorn service:
sudo systemctl start flaskapp
sudo systemctl enable flaskapp

Install and Configure Nginx:
sudo apt-get install nginx

Create a server configuration file in /etc/nginx/sites-available directory:
sudo nano /etc/nginx/sites-available/app
In server block defines ports on which they listen to and server name. With listen 80 line, nginx will listen to port 80. Location block located within server blocks.

delete default configuration file:
sudo rm -rf default

To start nginx service:
sudo systemctl start nginx

To enable nginx service:
sudo systemctl enable nginx 



