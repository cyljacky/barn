# Blogging - Jekyll

## Requirement

| [Ruby](https://www.ruby-lang.org/en/downloads/) | [Ruby Gems](https://rubygems.org/pages/download) | [GCC](https://gcc.gnu.org/install/) | [Make](https://www.gnu.org/software/make/) |
| :--- | :--- | :--- | :--- |
| `ruby -v` | `gem -v` | `gcc -v` or `g++ -v` | `make -v` |
| ver. 2.2.5+ | - | - | - |

## Install Jekyll \(MacOS\)

Mac OS version is used as localhost of the website.

```text
gem install bundler jekyll
```

[Bundler](https://rubygems.org/gems/bundler) acts as Ruby project plugin manager. Just like Composer in PHP.

To generate directory of the project:

```text
jekyll new myblog
```

```text
<your project directory> jackycheung$ sudo bundle exec jekyll serve
Configuration file: /<your project directory>/_config.yml
            Source: ./
       Destination: ./_site
 Incremental build: disabled. Enable with --incremental
      Generating...
       Jekyll Feed: Generating feed for posts
                    done in 0.84 seconds.
 Auto-regeneration: enabled for './'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```

Build the site and serve the site. When updating the file will hot rebuild the website, though the webpage need to be refreshed to see update.

## File Structure

### \_config.yml

Site-global configuration stores here.

### \_drafts/

Folder stores unpublished posts, post files name formats in `title.md`.

To preview with draft, use with command: `jekyll serve --drafts` or `jekyll build --drafts`

### \_includes

Files here are partials that can be included with `\{\% include file.ext \%\}` tag.  
Can be used as modules of layout

### \_layouts

Files here are templates used to generate general layout of the webpage.  
File layout are declared in Front matter.

### \_posts

Files here are the content of single webpage.  
Files should named in `YEAR-MONTH-DAY-title.md`.

### \_data

Data files stores here. Extensions like `.yml`, `.yaml`, `.json`, `.csv` are supported.  
Data are auto loaded, and accessible via `site.data`.  
E.g. File `test.yml` are accessible via `site.data.test`.

### \_sass

These are sass partials that can be imported into your `main.scss` which will then be processed into a single stylesheet `main.css` that defines the styles to be used by your site.

### \_site

Built website files stores here. Should be excluded from `.gitignore`.

### .jekyll\_metadata

Jekyll generated file for keep track of unmodified files. Should be excluded from `.gitignore`.

### &lt; page-name &gt;.html

If the file has Front matter, it will generated as a page by Jekyll. This applies to `.html`, `.markdown`, `.md`, `.textile` in the site root directory.

### Other files/folders

E.g. `css` and `images` folders, `favicon.ico` files Will be copied verbatim to the generated site.

