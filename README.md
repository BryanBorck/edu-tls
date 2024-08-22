# edu-tls

**Disclaimer: ZAP readme file => estou abrindo publico para voces aqui**

```
extension/
└── README.md
```

## Flow Chart

_need to finish_

## Installing and Running

There are 3 code components:

- **Local Extension:** Responsible for the client
- **Local Notary Server:** Responsible for the local notarization with less latency
- **Local Websocket:** Responsible for the proxy between server and client

### Extension Procedures:

1. Check if your [Node.js](https://nodejs.org/) version is >= **18**.
2. Clone this repository.
3. Run `npm install` to install the dependencies.
4. Run `npm start`, it will generate a `build` folder.
5. Load your extension on Chrome following:
   1. Access `chrome://extensions/`
   2. Check `Developer mode`
   3. Click on `Load unpacked extension`
   4. Select the `build` folder.
6. Now use Zap.

### Local Notary Procedures:

1. Fork this repository: [Notary Server](https://github.com/tlsnotary/tlsn)
2. Run `git checkout v0.1.0-alpha.5` to adjust the server version (⚠️ Important!!)
3. Disable tls in the `config/config.yaml` file (write `false` instead `true` - line 18)
4. Run `cargo run --release` in the root folder
5. See the logs.

### Local Websocket Procedures:

1. Fork this repository: [Local Proxy](https://github.com/novnc/websockify)
2. Run `./docker/build.sh` to build image using Docker
3. Choose a host to perform a proxy:
   1. Example: Notarize `api.x.com`
   2. Certify if the host is present on the whitelist domains of TLSN
   3. Run `docker run -it --rm -p 55688:80 novnc/websockify 80 api.x.com:443`
5. Use it

## Packing

After the development, run the command

```
$ NODE_ENV=production npm run build
```

Now, the content of `build` folder will be the extension ready to be submitted to the Chrome Web Store. 

Just take a look at the [official guide](https://developer.chrome.com/webstore/publish) to more infos about publishing.

## Resources:
