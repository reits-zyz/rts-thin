# rts-thin
reits chain thin node source code patch to bitcoin core v0.12.1

To play with rts thin node:

1, Clone bitcoin core;
    git clone https://github.com/bitcoin/bitcoin.git

2, Make a local branch from v0.12.1;
    cd bitcoin
    git checkout -b rts-thin v0.12.1

3, Apply the patch;
    git apply rts-thin.patch

4, Configure and make the command line executables;
    ./autogen.sh
    ./configure --with-gui=no --disable-debug --disable-tests
    make
    cp src/bitcoind ~/reitsd-thin
    cp src/bitcoin-cli ~/reits-cli

5, Start rts thin node;
    cd
    mkdir .reits
    ./reitsd projects/reits-test/src/bitcoind -rpcuser=user -rpcpassword=123456 -daemon -onlynet=ipv4 -listenonion=0 -rpcport=28333 -datadir=.reits -addnode=59.110.172.243:9555 -txindex -listen=0

6, Because rts is an opposite to a decentralized anonymous crypto currency system, you must have an secret key with an address authorized by the rts chain operator;
    Example:
        Authorized address: 1DxXtPEEZ71PoFbaoMScPeF1FxADfVtzhF
        Secret key wif: Ky1CCSRLVpgAGPDbm5c65vMwo21LcuACbzZ7SunK6zStP5sYDxBR

7, Import the authorized key pair as default key to the thin node;
    echo 'Ky1CCSRLVpgAGPDbm5c65vMwo21LcuACbzZ7SunK6zStP5sYDxBR 2017-08-24T06:57:54Z label=-defaultkey # addr=1DxXtPEEZ71PoFbaoMScPeF1FxADfVtzhF' > defaultkey.w
    ./reits-cli -datadir=.reits -rpcuser=user -rpcpassword=123456 -rpcconnect=127.0.0.1 -rpcport=28333 importwallet defaultkey.w

8, Now the thin node can connect to the rts network, data synchronization begin and you rock.
