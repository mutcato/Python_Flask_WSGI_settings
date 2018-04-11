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
