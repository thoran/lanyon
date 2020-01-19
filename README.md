Lanyon
======

Lanyon serves your Jekyll site as a Rack application.

Lanyon is a good friend of [Jekyll][jekyll], the static site generator,
and transforms your website into a [Rack][rack] application.

## Getting Started

Assuming you already have a Jekyll project that can be built and
served using the `jekyll` command line tool, then converting it
to a Rack application is very simple.

 1. Add a `config.ru` file in your project's root directory,
    with the following content:

    ``` ruby
    require "lanyon"

    run Lanyon.application
    ```

    You can specify additional Rack middleware in this file.

 2. At the command prompt, build the site and start the web server with

    ``` sh
    rackup config.ru
    ```

You can find an example site in the `demo` directory.

Note that Lanyon does not watch for site changes.
Auto-regeneration similar to Jekyll's `serve` command is
not supported, and there are no plans to add this feature.

Lanyon applications can be served with WEBrick, Thin, Unicorn and many
other web servers, and they can be deployed to services like e.g. Heroku.

## Installation

You can install the Lanyon gem from RubyGems.org with

``` sh
gem install lanyon
```

## Configuration

### Options

Jekyll configuration options can be specified in a `_config.yml` file
or as Lanyon initialization options in `config.ru`.

Example:

``` ruby
run Lanyon.application(destination: "mysite")
```

This will set a custom destination path, overriding the default (`_site`)
and settings from a config file.
See Jekyll's documentation for more settings.

Additional Lanyon initialization options:

    :config       - use given config file (default: "_config.yml")
    :skip_build   - whether to skip site generation at startup
                    (default: false)

Note that on read-only filesystems a site build will fail,
so you must set `skip_build: true` in these cases.

### Custum 404 Page

You can provide a custom `404.html` file in your site's root directory.
This can also be a file generated by Jekyll from e.g. Markdown sources.

## Requirements

- [Ruby][ruby] 2.0.0 or higher

- Gem dependencies (runtime): `jekyll`, `rack`

## How URLs are resolved

Lanyon maps URLs to corresponding files as follows:

 1. a `path/` with a trailing slash is changed to `path/index.html`,
 2. then, Lanyon checks for an exactly corresponding file,
 3. when `path` does not exist but `path/index.html` does,
    the response will be a redirect to `path/`,
 4. when neither 2. nor 3. apply, +path.html+ is tried.

To avoid confusion, it's probably a good idea to have only one
of `resource`, `resource/index.html`, and `resource.html` present
as file in your site.

## Reporting Bugs

Report bugs on the Lanyon home page: <https://github.com/stomar/lanyon/>

## Credits

Lanyon was inspired by [rack-jekyll][rack-jekyll] and written as a replacement.

## License

Copyright &copy; 2015-2020 Marcus Stollsteimer

Lanyon is licensed under the [MIT License][MIT].
See also the included `LICENSE` file for more information.


[ruby]: http://www.ruby-lang.org/
[jekyll]: http://jekyllrb.com/
[rack]: http://rack.github.io/
[rack-jekyll]: https://github.com/adaoraul/rack-jekyll
[MIT]: http://www.opensource.org/licenses/MIT
