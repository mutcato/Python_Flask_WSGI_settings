# Python_Flask_WSGI_settings
On Debian Linux WSGI Settings

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

	ServerName 192.168.0.127
	ServerAdmin youemail@email.com
	WSGIScriptAlias / /var/www/html/FlaskApp/FlaskApp.wsgi

	Order allow,deny
	Allow from all

	Alias /static /var/www/html/FlaskApp/static

	Order allow,deny
	Allow from all

	ErrorLog /var/www/html/FlaskApp/logs/error.log
	LogLevel warn
	CustomLog ${APACHE_LOG_DIR}/access.log combined
	
	sudo service apache2 reload
	sudo /usr/sbin/a2ensite FlaskApp.conf
