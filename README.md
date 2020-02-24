docker run --rm -it chevdor/polkadot:latest polkadot --version


parity/polkadot

https://polkascan.io/pre/westend

docker run -d -p 30333:30333 -p 9933:9933 -v $PWD/data:/data chevdor/polkadot polkadot --chain westend


docker run --rm -it parity/polkadot --help

docker run --rm -it parity/polkadot --version

docker run --rm -it parity/polkadot --light --alice

/polkadot/.local/share/polkadot

