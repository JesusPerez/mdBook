# mdBook with absolute links via site-url

[![Build Status](https://github.com/rust-lang/mdBook/workflows/CI/badge.svg?event=push)](https://github.com/rust-lang/mdBook/actions?workflow=CI)
[![crates.io](https://img.shields.io/crates/v/mdbook.svg)](https://crates.io/crates/mdbook)
[![LICENSE](https://img.shields.io/github/license/rust-lang/mdBook.svg)](LICENSE)

**mdBook** is a utility to create modern online books from Markdown files.

> Code here is a [fix](#how-to-use-it) for Absolute Links with [**site-url**](https://rust-lang.github.io/mdBook/format/configuration/renderers.html?highlight=site-url#html-renderer-options) value setting in **book.toml** config.

> This [fix](https://github.com/JesusPerez/mdBook) version has been reported to [mdBook source](https://github.com/rust-lang/mdBook/)  as [comment to issue 10802](https://github.com/rust-lang/mdBook/pull/1802#issuecomment-1552874669)

Check out the **[User Guide]** for a list of features and installation and usage information.
The User Guide also serves as a demonstration to showcase what a book looks like.

If you are interested in contributing to the development of mdBook, check out the [Contribution Guide].

## How to use it

**mdBook** has to be build and optionally installed

> Try **sitefix-book** as book example using **/doc/** as **site-url**  
> or use full absolute URL complete with hostnames and schemas ends with **/**
> for example: http://localhost:3000/doc/

In [sitefix-book/book.toml](sitefix-book/book.toml) add **base_url** (base href) to rendered files with **site-url** value, ends with **/**

In case relative path in **TOC** and **SUMMARY** is not fixed with **site-url** value:  

- Replace **SUMMARY.md** entries to include **site-url**
- Replace **TOC** entries for each sidebar **chapter-item** to include **site-url**

<small>see example below</small>

To complement this fix:

- [mdBook Tera](https://github.com/avitex/mdbook-tera) preprocessor should be added (installed) and activated in [book.toml](sitefix-book/book.toml)
- [context.toml](sitefix-book/context.toml) for [mdBook Tera](https://github.com/avitex/mdbook-tera) preprocessor has to include **urlbase** with same **site-url** value  
- Markdown **URLS** or **SRC** in book files has to start with **{{urlbase}}** prefix  

```markdown  
[Introduction]({{urlbase}}introduction.md)
![Image]({{urlbase}}image.jpg)
```

[my-theme/index.hbs](sitefix-book/my-theme/index.hbs) is used to set **urlbase** in **previous** and **next** navigation

You can use a script to automate builds:

- Take care of: **paths**, **book.toml**, **index.hbs**, etc.
- Use [mdBook](https://github.com/rust-lang/mdBook.git) to build rendered result to **dist** path rather than default **book**

if not installed add build target path to **mdbook** (../target/debug/)

```bash
mkdir -p /tmp/site/doc
mdbook build --dest-dir /tmp/site/doc
```

IMPORTANT: **site-url** only works with **mdbook build** with **serve** option has no sense as it is for development and **site-url** is overwritten with local path.

By using these procedures **sitefix-book** distribution build can be tested with

```bash
cd /tmp/site/doc
python3 -m http.server
```

Use a web-browser for: http://localhost:3000/doc

> For distribution or publish [mdBooks](https://github.com/rust-lang/mdBook.git) follow above instructions or use a script to set **<u>absolute_path</u>** in **book.toml** and **context.toml**

## License

All the code in this repository is released under the ***Mozilla Public License v2.0***, for more information take a look at the [LICENSE] file.

[User Guide]: https://rust-lang.github.io/mdBook/
[contribution guide]: https://github.com/rust-lang/mdBook/blob/master/CONTRIBUTING.md
[LICENSE]: https://github.com/rust-lang/mdBook/blob/master/LICENSE
