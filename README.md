# Python_Flask_WSGI_settings
On Debian Linux WSGI Settings

İnstall Apache Server and WSGI for Python 3

	sudo apt-get install apache2 libapache2-mod-wsgi-py3

/var/www/html/FlaskApp/__init__.py
```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
	return "Homepage Here"

@app.route('/about')
def about():
	return "About page is here."
	
if __name__=="__main__":
	app.run(debug=True)
```

/var/www/html/FlaskApp/FlaskApp.wsgi

	import sys
	sys.path.insert(0, ‘/var/www/html/FlaskApp’)
	from __init__ import app as application
	
Then create FlaskApp.conf file with nano editor

	sudo nano /etc/apache2/sites-available/FlaskApp.conf

	<VirtualHost *:80>
			ServerName 192.168.0.130
			ServerAdmin email@gmail.com
			WSGIDaemonProcess insta python-path=/home/pi/Public/insta:/home/pi/.virtualenvs/insta/lib/python3.5/site-packages
			WSGIProcessGroup insta
			WSGIScriptAlias / /home/pi/Public/insta/FlaskApp.wsgi
			<Directory /home/pi/Public/insta/>
				Order allow,deny
				Allow from all
			</Directory>
			Alias /static /home/pi/Public/insta/static
			<Directory /home/pi/Public/insta/static/>
				Order allow,deny
				Allow from all
			</Directory>
			ErrorLog /home/pi/Public/insta/logs/error.log
			LogLevel warn
			CustomLog ${APACHE_LOG_DIR}/access.log combined
	</VirtualHost>

<VirtualHost *:80>
	
Then reload the apache
	
	sudo service apache2 reload

Link .conf file to the Apache

	sudo /usr/sbin/a2ensite FlaskApp.conf
