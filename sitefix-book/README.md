# SiteFix Book

- Create a **dist** path
- Run **mdbook** from this repo

```bash
../target/release/mdbook build --dest-dir dist/doc
``` 

**doc** is absolute=path declared in **book.toml**  as **site-url**

```toml
[output.html]
site-url = "/doc/"
```

**doc** is absolute=path declared in *context.toml** as {{urlbase}}

```toml
urlbase = "/doc/"
```


