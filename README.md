# Polymer Bundler issue 489 repro

```bash
npm install -g polymer-bundler
# installs 2.2.0
mkdir -p out
rm -rf out/*
polymer-bundler \
  --out-dir out \
  --in-html entrypoint-1.html \
  --in-html entrypoint-2.html \
  --in-html entrypoint-3.html \
  --in-html entrypoint-4.html \
  --in-html shell.html \
  --shell shell.html
```

The results are in the out directory.

| Bundle            | Inlined Code           |
|:------------------|:-----------------------|
| entrypoint-1.html | -                      |
| entrypoint-2.html | Dep2.html              |
| entrypoint-3.html | -                      |
| entrypoint-4.html | -                      |
| shell.html        | Dep1.html, common.html |

The results above are what I would expect.  Please note that as of polymer-bundler 2.2.0, the bundles will not include `<link rel="import" href="shell.html">`.  This is because the shell model assumes the shell.html is imported from the main `index.html`.