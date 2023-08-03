# markuplint-overwrite-rules

A reproduction of (something may be) a bug in [markuplint](https://markuplint.dev/).

# prepare

```bash
$ pnpm install
```

# run

## errors occur with rules (expected behaviour)

1. modify the ".markuplintrc" as lint follows:

```json
{
  "extends": [
    "markuplint:recommended"
  ]
}
```

2. run `pnpm lint:html` and you will see something like the following errors.

```bash
% pnpm run lint:html                                                        

> markuplint-override-rules@1.0.0 lint:html /path/to/markuplint-overwrite-rules
> markuplint **/*.html

<markuplint> error: Require doctype (doctype) /path/to/markuplint-overwrite-rules/index.html:1:1
  1: <html></html>
  2: 
<markuplint> error: Require an element. (Need "title") (permitted-contents) /path/to/markuplint-overwrite-rules/index.html:1:7
  1: <html>headml>
  2: 
<markuplint> error: The "html" element expects the "lang" attribute (required-attr) /path/to/markuplint-overwrite-rules/index.html:1:1
  1: <html></html>
  2: 
<markuplint> error: Require the "meta[charset="UTF-8" i]" element (required-element) /path/to/markuplint-overwrite-rules/index.html:1:7
  1: <html>headml>
  2: 
<markuplint> error: Require the "h1" element (required-h1) /path/to/markuplint-overwrite-rules/index.html:1:1
  1: <html></html>
  2: 
 ELIFECYCLE  Command failed with exit code 1.
```

## overrides one of the errors and no error occurs (unexpected behaviour)

1. modify the ".markuplintrc" as lint follows:

```json
{
  "extends": [
    "markuplint:recommended"
  ],
  "overrides": {
    "./index.html": {
      "rules": {
        "doctype": false
      }
    }
  }
}
```

2. run `pnpm lint:html` and you won't see any error.

### what I expected

I just mean to override the "doctype" rule. Even in the same file, I still want to apply the other rules, such as "permitted-contents", "required-attr" and so on.
