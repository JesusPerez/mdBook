# mdBook with absolute links via site-url

[![Build Status](https://github.com/rust-lang/mdBook/workflows/CI/badge.svg?event=push)](https://github.com/rust-lang/mdBook/actions?workflow=CI)
[![crates.io](https://img.shields.io/crates/v/mdbook.svg)](https://crates.io/crates/mdbook)
[![LICENSE](https://img.shields.io/github/license/rust-lang/mdBook.svg)](LICENSE)

mdBook is a utility to create modern online books from Markdown files.

> Code here is a [fix](#how-to-use-it) for Absolute Links with [**site-url**](https://rust-lang.github.io/mdBook/format/configuration/renderers.html?highlight=site-url#html-renderer-options) value setting in **book.toml** config.

> This [fix](https://github.com/JesusPerez/mdBook) version has been reported to [mdBook source](https://github.com/rust-lang/mdBook/)  as [comment to issue 10802](https://github.com/rust-lang/mdBook/pull/1802#issuecomment-1552874669)

Check out the **[User Guide](https://rust-lang.github.io/mdBook/)** for a list of features and installation and usage information.
The User Guide also serves as a demonstration to showcase what a book looks like.

If you are interested in contributing to the development of mdBook, check out the [Contribution Guide](https://github.com/rust-lang/mdBook/blob/master/CONTRIBUTING.md).

## How to use it

Look at [sitefix-book](sitefix-book) example

- Set **site-url** value in **book.toml** section [output.html]

```toml
[output.html]
site-url = "/ABSOLUTE-ROOT-PATH/"
```

- Add **base_url** (base href) to rendered files with **site-url** value
- Replace **SUMMARY.md** entries to include **site-url**
- Replace **TOC** entries for each sidebar **chapter-item** to include **site-url**

To complement this fix:

- [mdBook Tera](https://github.com/avitex/mdbook-tera) preprocessor should be added, activated in **book.toml**
- **./context.toml** has to include **urlbase** with same **site-url** value  
- Add new <u>theme path</u> to **book.toml** 
  
```toml
[output.html]
theme = "NEW-THEME-PATH"
```

- In **index.hbs** fix <u>previous</u> and <u>next</u> templates by using **{{urlbase}}**

```handlebars
FROM:
  
<a rel="prev" href="{{ path_to_root }}{{link}}" ...
TO:
<a rel="prev" href="{{urlbase}}{{link}}" ...
```

- Markdown URLS or SRC in files has to start with **{{urlbase}}** prefix  

- Create a <u>theme path</u> and copy at least **src/index.hbs** inside.

```markdown
[Introduction]({{urlbase}}introduction.md)
![Image]({{urlbase}}image.jpg)
```

Script to automate builds:

- Take care of: **book.toml**, **index.hbs**, **head.hbs**
- Use [mdBook](https://github.com/rust-lang/mdBook.git) to build rendered result to **dist** path rather than default **book**

> By using these procedures default **book development** should work as expected
> For distribution or publish [mdBooks](https://github.com/rust-lang/mdBook.git) follow above instructions or use a script to set __<u>absolute_path</u>__ in **book.toml** and **context.toml**

## License

All the code in this repository is released under the ***Mozilla Public License v2.0***, for more information take a look at the [LICENSE](https://github.com/JesusPerez/mdBook/blob/master/LICENSE)

[User Guide]: https://rust-lang.github.io/mdBook/
[contribution guide]: https://github.com/rust-lang/mdBook/blob/master/CONTRIBUTING.md
[LICENSE]: https://github.com/rust-lang/mdBook/blob/master/LICENSE
