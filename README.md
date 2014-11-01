# Reagent Documentation



## Developing Locally

With Bundler:

    bundle install --binstubs

### How to run a development server

    ./bin/jekyll serve --watch

then navigate to [localhost:4000](http://localhost:4000)

### How to regenerate the site

    ./bin/jekyll build

## Developing With Docker

If you don't have ruby toolsets available on your machine, you can run this project in Docker with [Fig](http://www.fig.sh).

### Running a local development server

```
fig up
```

Then navigate to [localdocker:4000](http://localdocker:4000).

### Regenerating the site

```
fig run web jekyll build
```

## License & Copyright

Copyright (C) 2014 The Reagent Team

Distributed under the Eclipse Public License, the same as Clojure.
