```
sudo apt install build-essential autoconf python3 python3-dev wget postgresql postgresql-postgis git libxml2-dev libxslt1-dev zlib1g-dev libpq-dev python3-dev gcc python3-pip
sudo pip install virtualenv
sudo mkdir -p /srv/umap
sudo mkdir -p /etc/umap
sudo useradd -N umap -d /srv/umap/
sudo chown umap:users /etc/umap
sudo chown umap:users /srv/umap
sudo -u postgres createuser umap
sudo -u postgres createdb umap -O umap
sudo -u postgres psql umap -c "CREATE EXTENSION postgis"
```

```
sudo -u umap -i
virtualenv /srv/umap/venv --python=/usr/bin/python3.9
. /srv/umap/venv/bin/activate
pip install umap-project
nano /etc/umap/umap.conf
```

Changer les lignes suivantes

```
STATIC_ROOT = '/srv/umap/var/static'
MEDIA_ROOT = '/srv/umap/var/data'
```

```
umap migrate
umap collectstatic
umap createsuperuser
umap runserver 0.0.0.0:8000
```
