### Working on project


#### Setup

* Create virtualenv `mkvirtualenv backend`
* Install Django `1.11` `pip3 install Django`

* Create project dir `django-admin startproject backend`

* Edit `backend/settings.py`

* Create dirs `mkdir templates && mkdir static`

* Create database.

* Create needed modules with `pip3`

```textmate
pip3 install django
pip3 install mysqlclient
```
* Run migrate `python3 manage.py migrate`

* Check if this working `python3 manage.py runserver 0.0.0.0:9160`. Access `http://192.168.99.100:9160/` to see.

*  Create admin `python3 manage.py createsuperuser` and using `root/tieungao/quan.dm@teko.vn`

* Access `http://192.168.99.100:9160/admin/`.

* Copy `.gitignore` files

```textmate
cp /var/www/html/python_polls/.gitignore .
cp /var/www/html/python_polls/static/.gitignore static/
```
* Generation `pip3 freeze > requirements.txt` for later using `pip3 install -r requirements.txt`.

#### For deploy to host

* Edit `deploy` files.

* Commit to github.

* On the host, run below 

```textmate
mkvirtualenv backend
pip3 install -r requirements.txt
python3 manage.py collectstatic
ln -s /var/www/html/backend/deploy/backend.ini /etc/uwsgi/sites/backend.ini
ln -s /var/www/html/backend/deploy/local.backend.vn /etc/nginx/sites-enabled/local.backend.vn
mysql -uroot -ptieungao -e "create database python_backend"
python3 manage.py migrate
python3 manage.py createsuperuser
deactivate
sudo systemctl restart uwsgi
service nginx restart
```
* Edit local `hosts` file 
```textmate
42.112.31.173 local.backend.vn
```
And access `http://local.backend.vn/admin/` to see everything is ok.

#### Google Auth is shit so stop at this.

