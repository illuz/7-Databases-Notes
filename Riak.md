Riak
===

Doc: http://docs.basho.com/riak/latest/  
A Little Riak Book: http://littleriakbook.com/  

### Install in Ubuntu

**Install with apt-get**  

```shell
# 1. retrieve the signing key
curl https://packagecloud.io/gpg.key | sudo apt-key add -

# 2. install the `apt-transport-https` package
#    in order to be able to fetch packages over HTTPS
sudo apt-get install -y apt-transport-https

# 3. add basho.list and update
sudo bash -c 'curl "https://packagecloud.io/install/repositories/basho/riak/config_file.list?os=Ubuntu&dist=trusty&name=illuz-ubuntu" > /etc/apt/sources.list.d/basho.list'
sudo apt-get update

# 4. install riak
sudo apt-get install riak
```

Dog Fxxxing GF\/\/! The `amazonaws.com` is unavailable even under VPN. ...  
**Then install Riak from package:**   

```shell
# PAM Library && SSL Library
sudo apt-get install libpam0g-dev libssl0.9.8

# get package and install
wget https://packagecloud.io/basho/riak/ubuntu/pool/trusty/main/r/riak/riak_2.1.0-1_amd64.deb # change to your distribution
sudo dpkg -i riak_2.1.0-1_amd64.deb
```

**Maybe can try to install from source**  
(Need to install Erlang first)  

```shell
# 1. install Erlang
# require lib
sudo apt-get install build-essential libncurses5-dev openssl libssl-dev fop xsltproc unixodbc-dev
# If you'll be using a graphical environment, install packages for graphics support
# sudo apt-get install libwxbase2.8 libwxgtk2.8-dev libqt4-opengl-dev
# build
wget http://s3.amazonaws.com/downloads.basho.com/erlang/otp_src_R16B02-basho5.tar.gz
tar zxvf otp_src_R16B02-basho5.tar.gz
cd otp_src_R16B02-basho5
./configure && make && sudo make install

# 2. install from source
# basic require
sudo apt-get install build-essential libc6-dev-i386 git

# build
wget http://s3.amazonaws.com/downloads.basho.com/riak/2.1/2.1.0/riak-2.1.0.tar.gz
tar zxvf riak-2.1.0.tar.gz
cd riak-2.1.0
make rel
```

---
*(Updating)*
