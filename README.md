# cf-redirect

Small app to redirect traffic from one domain to another.

## Usage

In `manifest.yml`, change `TARGET_DOMAIN` to the domain you want to redirect _to_. Change `host` to the domain you want to redirect _from_.


    $ cf push -f manifest.yml

That's it!


## Conventions

Instead of forking this repo to simply have a redirect to your app, you can copy
these files to a `redirects/<redirect-from-domain>` dir in the app you're
redirecting _to_. This way all the redirects to your app are stored in a single
repo.

Then you can add a `path` property to the manifest file to make deployments easy.

```
---
memory: 64MB
name: cf-redirect
host: redirect-from-domain.example.com
path: ./redirects/redirect-from-domain.example.com
env:
  TARGET_DOMAIN: redirect-to-domain.example.com
```

Now you can deploy like so.

    $ cf push -f redirects/redirect-from-domain.example.com/manifest.yml
