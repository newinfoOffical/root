# Peernet Root Peer

The root peer client is a fork of the command line client. It adds statistics functionality and tracks the following KPIs:

* Daily active peers
* Weekly active peers [todo]
* Monthly active peers [todo]
* Full log of all new peers per day

Peers are counted uniquely based on their public key.

## Compile

To build:

```
go build
```

To cross compile from Windows to Linux and deploy:

```
set GOARCH=amd64
set GOOS=linux
go build

chmod +x ./root
nohup ./root &

ps -ef | grep -i ./root
kill [pid]
```

### Merge changes from Cmd

The changes from https://github.com/PeernetOfficial/Cmd should be merged regularly.

## Deploy

These are the files of a root peer:
* `root.exe` (or just `root` for linux)
* `Config.yaml` - autogenerated, but settings should be immediately adjusted after first run, especially static IP:Port settings.
* `Web Files\*` - folder for all web files if `WebListen` is set in config

### Settings

Add the following settings to `Config.yaml`:

```
WebListen: ["127.0.0.1:1234","[::1]:1234"]
UseSSL: true
CertificateFile: "n.peernet.network-crt.pem"
CertificateKey: "n.peernet.network-key.pem"

DatabaseFolder: "csv"
```

The tool win-acme from https://www.win-acme.com/ can create and renew Let's Encrypt certificates. Note that the certificate is not yet automatically refreshed and a restart of the root process is required upon renewal.
