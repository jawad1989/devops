# install PostgreSQL 11 on Amazon Linux (Compile)

### Step 1: Prerequisites
There are a few prerequisites. Let’s install them before starting installing PostgreSQL.
```
yum install wget tar gcc make
```
### Step 2: Download the Archive
First of all, download the archive and untar it so we can compile it.
```
wget https://ftp.postgresql.org/pub/source/v11.5/postgresql-11.5.tar.gz
```
### Step 3: Extract the archive
Now, let’s extract the archive quickly using tax command.
```
tar -zxvf postgresql-11.5.tar.gz
```
### Step 4: Compile
So now we have extracted the archive so we can compile it.
```
cd postgresql-11.5/
./configure --without-readline --without-zlib
make
make install
```
### Step 5: Symlink
Now in the last step lets create a symlink
```
ln -s /usr/local/pgsql/bin/psql /usr/bin/psql
# psql --version
```
psql (PostgreSQL) 11.5
