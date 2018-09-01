# jmdictdb-howto

# Download source
1. Download and extract
```
mkdir jmdictdb && cd jmdictdb
wget http://www.edrdg.org/~smg/cgi-bin/hgweb-jmdictdb.cgi/archive/tip.tar.gz
tar -xvzf tip.tar.gz
rsync -vua --delete-after JMdictDB-Mercurial-Repository-61238fcafb31/ .
```

# Prerequisites

Important installations notes: <br/>
http://www.edrdg.org/~smg/cgi-bin/hgweb-jmdictdb.cgi/file/tip/README.txt
<br/><br/>

1. Install pip for Python 3
``` 
sudo apt-get install software-properties-common
sudo apt-add-repository universe
sudo apt-get update
sudo apt-get install python3-pip
```  

2. Install JMDictDB python script dependencies
```
pip3 install psycopg2
pip3 install ply
pip3 install lxml
pip3 install jinja2
```  

3. Install Postgres
```
sudo apt install postgresql postgresql-contrib
```    

4. Configure Postgres (for the scripts to work)
```
sudo pico /etc/postgresql/10/main/pg_hba.conf
```
Change the following line
```
# "local" is for Unix domain socket connections only
local   all             all                                     peer
```
to
```
# "local" is for Unix domain socket connections only
local   all             all                                     trust
```
and restart Postgres
```
sudo /etc/init.d/postgresql restart
```  
5. Install Japanese locale
```
sudo dpkg-reconfigure locales
```
Pick your system locale (likely en_US.UTF8 and ja_JP.UTF8 in the list of locales to be generated).  

7. Fix the script python/xresolv.py by moving the SAVEPOINT statement into the for loop
```
            for x in xrefs:
                dbh.execute ("SAVEPOINT sp1;")
```  
8. Follow the 'installation procedure steps' as described in JMDictDBs README.txt

# Setup remote access to the postgres via SSH
1. Configure Postgres
```
/etc/postgresql/10/main/postgresql.conf 
```
Change to
```
listen_addresses = '*'
```
and restart Postgres
```
sudo /etc/init.d/postgresql restart
```  

2. OpenSSH
```
sudo apt-get install openssh-server
```
Enable ssh
```
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.factory-defaults
```
And restart ssh
```
sudo systemctl restart ssh
```  
