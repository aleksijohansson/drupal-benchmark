# Drupal Benchmark

This project is simply based on the [Wunder template for Drupal projects](https://github.com/wunderio/drupal-project) and meant for benchmarking a local Drupal development environment with the [Apache HTTP server benchmarking tool](https://httpd.apache.org/docs/2.4/programs/ab.html). See the before mentioned template for a more detailed documentation.

## Getting started

- Clone the project locally
- Optionally checkout a specific version, for example: `git checkout tags/v0.1`
- Start your environment and build Drupal
- Login to Drupal in your browser and copy the session cookie from the browser
- Run a benchmark with ab

This project comes with [Lando](https://lando.dev/) and [DDEV](https://ddev.com/) environments preconfigured. Please find more detailed examples for running the benchmark in these environments below.

### Lando

```sh
lando start && lando drush si --existing-config -y
lando drush uli
ab -C [session-cookie-name-here]=[session-cookie-value-here] -n 50 -l https://drupal-benchmark.lndo.site/admin/modules
```

### DDEV

```sh
ddev start && ddev composer install && ddev drush si --existing-config -y
ddev drush uli
ab -C [session-cookie-name-here]=[session-cookie-value-here] -n 50 -l https://drupal-benchmark.ddev.site/admin/modules
```

Ps. [DDEV comes with Mutagen for file syncing built in](https://ddev.readthedocs.io/en/latest/users/performance/), which can make an environment on macOS multiple times faster. You can enable Mutagen for your local DDEV globally with `ddev config global --mutagen-enabled`.
