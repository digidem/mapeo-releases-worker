## Mapeo Releases Redirect

This is a [Cloudflare Worker](https://developers.cloudflare.com/workers/) that
proxies our AWS S3 storage bucket where we store Mapeo releases for public
download.

Our CI release process generates/updates YAML files with the details of each release. This worker creates redirect URLs that read the YAML file and redirect to the latest release. E.g. https://releases.mapeo.app/desktop/latest-mac will read the file `desktop/latest-mac.yml` in our S3 bucket and redirect to download the file listed in the YAML file. Requests to S3 are proxied through the worker, so all downloads come from `https://releases.mapeo.app`.

### Development

[Install the Workers CLI](https://developers.cloudflare.com/workers/get-started/guide#2-install-the-workers-cli):

```sh
npm install -g @cloudflare/wrangler
```

Test the worker locally:

```sh
wrangler dev
```

Publish a staging version to https://mapeo-releases-worker.ddem.workers.dev

```sh
wrangler publish
```

Publish updated worker to https://releases.mapeo.app

```sh
wrangler publish --env production
```

### Download URLs

- Mapeo Desktop Windows: https://releases.mapeo.app/desktop/latest-win
- Mapeo Desktop Mac: https://releases.mapeo.app/desktop/latest-mac
- Mapeo Desktop Linux: https://releases.mapeo.app/desktop/latest-linux

- Mapeo for ICCAs Desktop Windows: https://releases.mapeo.app/desktop-icca/latest-win
- Mapeo for ICCAs Desktop Mac: https://releases.mapeo.app/desktop-icca/latest-mac
- Mapeo for ICCAs Desktop Linux: https://releases.mapeo.app/desktop-icca/latest-linux

Coming soon: Mapeo Mobile APK downloads
