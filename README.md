## Search backend for Wagtail CMS using Whoosh engine.

[![Build Status](https://travis-ci.org/wagtail/wagtail-whoosh.svg?branch=master)](https://travis-ci.org/wagtail/wagtail-whoosh)

## How to use

* `0.1.x` work with `wagtail>=2.0,<2.2`
* `0.2.x` work with `wagtail>=2.2`

`pip install wagtail-whoosh`

After installing this package, add `wagtail_whoosh` to INSTALLED_APPS. And then config `WAGTAILSEARCH_BACKENDS`

```python
WAGTAILSEARCH_BACKENDS = {
    'default': {
        'BACKEND': 'wagtail_whoosh.backend',
        'PATH': str(ROOT_DIR('search_index')),
        'SEARCH_CONFIG': 'fr',
    },
}
```

Set `./manage.py update_index` as cron job

## Features

### Score support

```
results = Page1.objects.search(query).annotate_score("_score").results()
result += Page2.objects.search(query).annotate_score("_score").results()
return sorted(results, key=lambda r: r._score)
```

### Language support

Whoosh includes pure-Python implementations of the Snowball stemmers and stop word lists for various languages adapted from NLTK.

`('ar', 'da', 'nl', 'en', 'fi', 'fr', 'de', 'hu', 'it', 'no', 'pt', 'ro', 'ru', 'es', 'sv', 'tr')`

You can choose one and config in `SEARCH_CONFIG`

## NOT-Supported features

1. `boosting` is not supported.
2. `facet` is not supported.
3. `autocomplete` is not supported.

## Sponsor

[Tomas Walch](https://github.com/tjwalch)
