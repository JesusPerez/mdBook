# mdBook with absoulte links via site-url

[![Build Status](https://github.com/rust-lang/mdBook/workflows/CI/badge.svg?event=push)](https://github.com/rust-lang/mdBook/actions?workflow=CI)
[![crates.io](https://img.shields.io/crates/v/mdbook.svg)](https://crates.io/crates/mdbook)
[![LICENSE](https://img.shields.io/github/license/rust-lang/mdBook.svg)](LICENSE)

mdBook is a utility to create modern online books from Markdown files.

> Code here is a [fix](#how-to-use-it) for Absolute Links with [**site-url**](https://rust-lang.github.io/mdBook/format/configuration/renderers.html?highlight=site-url#html-renderer-options) value setting in **book.toml** config.

Check out the **[User Guide]** for a list of features and installation and usage information.
The User Guide also serves as a demonstration to showcase what a book looks like.

If you are interested in contributing to the development of mdBook, check out the [Contribution Guide].

## How to use it

- Add **base_url** (base href) to rendered files with **site-url** value
- Replace **SUMMARY.md** entries to include **site-url**
- Replace **TOC** entries for each sidebar **chapter-item** to include **site-url**

To complement this fix:

- [mdBook Tera](https://github.com/avitex/mdbook-tera) preprocessor should be added, activated in **book.toml**
- **./context.toml** has to include **urlbase** with same **site-url** value  
- Markdown URLS or SRC in files has to start with **{{urlbase}}** prefix  

```markdown  
[Introduction]({{urlbase}}introduction.md)
![Image]({{urlbase}}image.jpg)
```

Script [build-dist.sh](build-dist.sh) automate builds by using:

- **templates** files for: **book.toml**, **index.hbs**, **head.hbs**
- [mdBook](https://github.com/rust-lang/mdBook.git) fix target build
- build rendered result to **dist** path rather than default **book**

<small>In case it is necessary, change settings values at script top</small>

> By using these procedures default **book development** should work as expected
> For distribution or publish [mdBooks](https://github.com/rust-lang/mdBook.git) follow above instructions or use a script to set __<u>absolute_path</u>__ in **book.toml** and **context.toml**

## License

All the code in this repository is released under the ***Mozilla Public License v2.0***, for more information take a look at the [LICENSE] file.

[User Guide]: https://rust-lang.github.io/mdBook/
[contribution guide]: https://github.com/rust-lang/mdBook/blob/master/CONTRIBUTING.md
[LICENSE]: https://github.com/rust-lang/mdBook/blob/master/LICENSE
