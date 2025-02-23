---
Title: How I setup this GitHub Pages Blog, Part 4
tags: Jekyll GitHubPages
description: Fourth group of steps in setting up a Jekyll generated blogging site
  hosted on GitHub Pages which uses any plugin, theme, Jekyll version or Ruby version.
category: technical
---
Welcome to the fourth part of this series detailing how I setup this blog site hosted on GitHub Pages. If you have not yet seen the first posts in the series [How I setup this GitHub Pages Blog Site Part 01]({{ '/technical/2021/2021-04-06-how-i-setup-this-github-pages-blog-site-part-01.html' | relative_url }}), [How I setup this GitHub Pages Blog Site Part 02]({{ '/technical/2021/2021-04-17-how-i-setup-this-github-pages-blog-site-part-02.html' | relative_url }}), and [How I setup this GitHub Pages Blog Site Part 03]({{ '/technical/2021/2021-04-24-how-i-setup-this-github-pages-blog-site-part-03.html' | relative_url }}) you should probably give them a quick review, to become familiar with how the site has been built up to this point.

The next steps will be to implement the features specified in [Milestone 0.04.0](https://github.com/BillHertzing/BillHertzing.github.io/milestone/4). I've already created Milestones for Release V0.05, [Milestone 0.05.0](https://github.com/BillHertzing/BillHertzing.github.io/milestone/5) as well and updated the Milestone *Release Far Future* to reflect what is planned for later. Release V0.05 calls for creation of a  Github project for tracking future features, so at that point hopefully, there will be a single point for tracking and reporting on planned and requested features.

Many of these instructions refer to Visual Studio Code (VSC).

## Add a new branch `SprintForRelease0.04.000`

- Run `git branch create SprintForRelease0.04.000`

## Update the commit template

- Edit `GitTemplates/git.commit.template.txt` and change `03` to `04`

## First commit on the sprint branch

Commit the changes and use VSC to synchronize changes with the remote, then inspect the Github repository to ensure the branch and first commit exist on the repo. I like using the VSC extensions `Git Lens` along with the extensions `Git Graph`. Together, these provide a clear view of the site's development history. ToDo: insert jpg

## Add the plugin jekyll-compose

jekyll-compose adds commands that help streamline the creation and publishing of posts. Installation instructions and details can be found in [jekyll-compose](https://github.com/jekyll/jekyll-compose). What follows are the steps I took and choices I made for this site.

1. Edit the Gemfile in the root of the repo.
1. Add `gem 'jekyll-compose', group: [:jekyll_plugins]` just above the `plugins:` key.
1. Run `bundle`

Refer to detailed instructions in [jekyll-compose](https://github.com/jekyll/jekyll-compose) for using the new commands. This post was drafted and published using the commands added by this tool, and it made the process much much easier. I created the draft of this post using the command `bundle exec jekyll draft "how-i-setup-this-github-pages-blog-site-part-04"`, which placed a file containing just Front Matter in the `_drafts` directory.

## Add jekyll-minifier

 Minification is the process of rewriting the stream of data sent from the server to the browser to make the stream as small as possible.Minification of your site is something that all good digital properties should do. It's just manners. But this has consequences if a developer is trying to read the data stream and debug problems.

As with any optimization, it is important to measure the baseline, and then the improvement.

-[ToDo: A short tutorial on using Fiddler 4 to measure the size of a response.]
-[ToDo: Alternative - Find online site that can quantify the number of bytes. Or see if Fiddler 4 has that capability.0

This minifier allows fine control over minification of HTML, JavaScript, CSS, and Json, as well as many more minification options.

Detailed instructions are here at [jekyll-minifier](https://github.com/digitalsparky/jekyll-minifier)

1. Run `gem install jekyll-minifier` Make a note of the version installed, mine was 0.1.10
1. Run `bundle update`
1. Edit `Gemfile` at the root of the repo, and add `gem "jekyll-minifier", "~> 0.1.10"` into the `group :jekyll_plugins do` section.
1. Edit `_config.yml` and add `jekyll-minifier` to the `plugins`: key

  ```yml
  plugins:
    - jekyll-minifier
  ```

1. Further down the `_config.yml` add lines that control the minifier's settings. Add the entire list now, and later we will work through each setting and decide if this site will need it.

  ```yml
  jekyll-minifier:
    preserve_php: true                # Default: false
    remove_spaces_inside_tags: true   # Default: true
    remove_multi_spaces: true         # Default: true
    remove_comments: true             # Default: true
    remove_intertag_spaces: true      # Default: false
    remove_quotes: false              # Default: false
    compress_css: true                # Default: true
    compress_javascript: true         # Default: true
    compress_json: true               # Default: true
    simple_doctype: false             # Default: false
    remove_script_attributes: false   # Default: false
    remove_style_attributes: false    # Default: false
    remove_link_attributes: false     # Default: false
    remove_form_attributes: false     # Default: false
    remove_input_attributes: false    # Default: false
    remove_javascript_protocol: false # Default: false
    remove_http_protocol: false       # Default: false
    remove_https_protocol: false      # Default: false
    preserve_line_breaks: false       # Default: false
    simple_boolean_attributes: false  # Default: false
    compress_js_templates: false      # Default: false
    preserve_patterns:                # Default: (empty)
    uglifier_args:                    # Default: (empty)
    
  ```

> ***es6 support is experimental.***  If your site is using es6 scripts, see the [jekyll-minifier](https://github.com/digitalsparky/jekyll-minifier) documentation for possible issues.

Run `bundle exec jekyll serve --drafts` and ensure the site looks like it should. The re-run the tests that measure the size of the data stream.

  **This is not working in the V0.04.000 Release. Error from uglifier: "...uglifier.rb:291:in `parse_result': Unexpected token: name ($style). To use ES6 syntax, harmony mode must be enabled with Uglifier.new(:harmony => true). (Uglifier::Error)"**

Note that the Release process is flexible enough to allow a release to happen even if a known issue is present, if there is a workaround.

Workaround: disable (put # in front of it) Minifier in `_config.yml` and in `Gemfile`.

- [ToDo: Create issue after release, fix, remove workaround]

## Add plugin jekyll-relative-links

The posts and pages are going to start referring to each other. This is called cross-linking, or cross-referencing, documents. To better support this, the jekyll-relative-links plugin allows these cross-reference links to be create using liquid tags that will resolve to the draft, and then to the published past or page.

Detailed instructions are here at [jekyll-relative-links](https://github.com/digitalsparky/jekyll-minifier)

1. Run `gem install jekyll-relative-links` Make a note of the version installed, mine was 0.6.1
1. Run `bundle update`
1. Edit `Gemfile` at the root of the repo, and add `gem "jekyll-relative-links", "~> 0.6.1"` into the `group :jekyll_plugins do` section.
1. Edit `_config.yml` and add `jekyll-relative-links` to the `plugins`: key

  ```yml
  plugins:
    - jekyll-relative-links
  ```

 Further down the `_config.yml` add lines that control the relative-links plugin's settings.

  ```yml
  relative_links:
    enabled:     true
    collections: false
  ```

## Create a Development override file for _Config.yml

Relative URL creates links that include the site name. The `_config.yml` file specifies the site's URL as `Billhertzing.github.io`. But during development, the site is locally hosted and served. The links used during development should use a site URL of `localhost`. It is possible to override the URL specified in '_config.yml' by creating a second .yml file, populating it with just the keys and values that should be different during development,and invoking the Jekyll build and serve process with an additional argument.

1. Create the file `_config.Development.yml` at the root of the repo.
1. Add the following two lines:

```yml
  url: https://localhost/ 
  baseurl: ''
```

During development, the command to build and serve the site should be:

```text
   bundle exec jekyll serve --config _config.yml, _config.Development.yml
```

## Setup archive pages

The MM theme has two kinds of archive support built in, either a Liquid approach or a `jekyll-archives` approach. I chose to use the `jekyll-archives` plugin.

### Add the `jekyll-archives` gem

1. Run `gem install jekyll-archives`. Mine came back as version 2.2.1.
1. Edit the `Gemfile` in the root of  the repo. Add `gem "jekyll-archives", "~> 2.2.1"` into the `group :jekyll_plugins do` group.
1. Run `bundle update`
1. Run `bundle exec jekyll build` and ensure the site builds correctly.

### Modify `_config.yml` for `jekyll-archives`

1. Edit `_config.yml`, and find the `jekyll-archives` section. Uncomment the settings that appear in MM's default. Mine looks like this:

   ```yml
   jekyll-archives:
    enabled:
      - categories
      - tags
    layouts:
      category: archive-taxonomy
      tag: archive-taxonomy
    permalinks:
      category: /categories/:name/
      tag: /tags/:name/
   ```

### Create override for `_pages/category-archive.md`

There needs to be an `index.html` in the generated site's `/categories/` directory.

1. Add a new subdirectory and file `_pages/category-archive.md` at the root of the repo.
1. Add the following Front Matter to the file. Nothing else is needed.

   ```yml
    ---
    title: "Posts by Category"
    layout: categories
    permalink: /categories/
    author_profile: true
    ---
    ```

1. Run `bundle exec jekyll serve` and ensure the site builds correctly
1. Navigate to `http://localhost:4000/categories/` and validate there is a page listing all current posts organized by category.

### Create override for `_pages/year-archive.md`

There needs to be an `index.html` in the generated site's `/year-archive/` subdirectory.

1. Add a new file `_pages/year-archive.md` at the root of the repo.
1. Add the following Front Matter to the file. Nothing else is needed.

   ```yml
    ---
    title: "Posts by Date"
    layout: archive
    permalink: /year-archive/
    author_profile: true
    ---
    ```

1. Run `bundle exec jekyll serve` and ensure the site builds correctly
1. Navigate to `http://localhost:4000/year-archive/` and validate there is a page listing all published posts organized by Date.

### Create override for `_pages/tags-archive.md`

There needs to be an `index.html` in the generated sites `/tags/` directory.

1. Add a new file `_pages/tags-archive.md` at the root of the repo.
1. Add the following Front Matter to the file. Nothing else is needed.

   ```yml
    ---
    title: "Posts by Tags"
    layout: Tags
    permalink: /tags/
    author_profile: true
    ---
    ```

1. Run `bundle exec jekyll serve` and ensure the site builds correctly
1. Navigate to `http://localhost:4000/tags/` and validate there is a page listing all current posts organized by tag.

## Setup masthead navigation

The MM theme has built-in support for masthead navigation. These are the links that appear across the top of every page, and which collapse down into the navigation hamburger on narrow screens. There is a direct relationship between the files in the `_pages` subdirectory and the navigation links in the `_data/navigation.yml`

Details on using masthead navigation are at MM's [Navigation](https://mmistakes.github.io/minimal-mistakes/docs/navigation/) . Here are the steps I took

1. Create a subdirectory and file `_data/navigation.yml` and open it for editing. I started with the following contents:

    ```yml
    ToDo: Add automation to read text from real file on file changes in site build
    main:
      - title: "About"
        url: /About/
      - title: "Posts"
        url: /year-archive/
      - title: "Categories"
        url: /categories/
      - title: "Tags"
        url: /tags/
      - title: "Subscribe"
        url: /subscribe-to-bills-blog/
      - title: "ChangeLog"
        url: /ChangeLog/
      - title: "Contributing"
        url: /Contributing/
      - title: "Code of Conduct"
        url: /Code-of-Conduct/
    ```

Run `bundle exec jekyll serve --drafts` and ensure masthead navigation is present. Play around with making the browser wider and narrower, and note how the horizontal masthead links expand from and collapse into a navigation hamburger.

## Setup custom sidebar navigation

The MM theme has the custom sidebar navigation capability built-in. Details on using it are at [Custom sidebar navigation menu](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#custom-sidebar-content) .

I plan to use this User static blog site to link together the DocFx generated static sites in every peer repository. The left Nav component is a window into all of the technical documentation for AceCommander and the ATAP Utilities.

Here are the steps I took to put up a placeholder for the left Nav:

1. Edit `_data/navigation.yml` . I started with the following contents, with TBD meaning of course "To Be Done":

    ```yml
    docs:
      - title:  Repositories Overview
        children:
          - title: "*Overview Guide - TBD*"
            url: /docs/overview-guide/
          - title: "Structure-TBD"
            url: /docs/structure/
          - title: "Testing-TBD"
            url: /docs/Testing/
          - title: "ReleaseProcess-TBD"
            url: /docs/ReleaseProcess/
          - title: "Upgrading-TBD"
            url: /docs/upgrading/
          - title: "EndOfLife-TBD"
            url: /docs/EndOfLife/
      - title:  SCM Conventions
        children:
          - title: "SCM for Code, Doc, and DB-TBD"
            url: /docs/SCM-Conventions/overview/
          - title: "Code SCM-TBD"
            url: /docs/Code-VersionControlProcess/
          - title: "Docs SCM-TBD"
            url: /docs/Documentation-VersionControlProcess/
          - title: "DB SCM-TBD"
            url: /docs/DataBase-VersionControlProcess/
          - title: "Peer Repository SCM-TBD"
            url: /docs/Peer-repository-AutoDoc-VersionControlProcess/
    ```

## Add rule for Git Merge

If a BugFix or new Post goes out on `main` while you are working on a Feature branch, you will need to rebase the feature branch onto the new head of `main`. There are likely to be a lot of files in `_site` with merge conflicts! since `_site` is all generated files, we can safely ignore any merge conflicts in the files under `site`. We can create a merge  to accomplish this by adding a custom merge driver, as follows:

1. Create the file `.gitattributes` in the root of the repo.
1. Add the line `/_site/**/*.* merge=keep-local-changes` and save the file.
1. Create (or edit) the file `~/.gitconfig`, which is your windows HOME directory, and contains the global git configuration settings.
1. Add the following block of text [Geordie answer to this SO question](https://stackoverflow.com/questions/12218977/git-add-merge-rule-to-config-for-specific-file):

   ```text
   [merge "keep-local-changes"]
      name = A custom merge driver which always keeps the local changes
      driver = true
   ```

1. You will need to close VSC and re-open it for the changes to the global `~/.gitconfig` to take effect.

## Rebase Feature branch onto the head of `main` after a site patch/post point release

The need to rebase the `Feature` branch onto the HEAD of the `main` branch can occur at any time. Detailed instructions can be found in [Bill's Blog Release Process]({{ '/technical/2021/2021-05-22-bills-blog-release-process.html#rebase-all-active-branches-onto-the-new-head-of-main' | relative_url }})

## Modify `_includes/gallery`

The `gallery` component opens an image link reusing the same tab as the parent document. Modern practice is to open an image link in a new tab. modify the `gallery` so that the anchor href now includes `target = "_blank" rel="noopener noreferrer nofollow"` . This will tell browsers to open the image in a new tab.

## Add the page `_pages/subscribe-to-bills-blog.md`

The page provides instructions on using [IFTTT](https://ifttt.com/) to subscribe to the site's RSS feed. Add the page `subscribe-to-bills-blog.md` to the root of the repo. The Front Matter should look like this:

  ```yml
    layout: single
    permalink: /subscribe-to-bills-blog/
    description: How to subscribe to posts from Bill's Blog site
    tags: [subscribe, "RSS Feed"]
    Category: technical
    ---   
  ```

Add content to the page explaining the steps necessary to setup an IFTTT trigger and target action that produces an e-mail message whenever the site's RSS feed indicates a change has been made to the site.

### Update masthead navigation

- Edit `_data/navigation.yml`
- Add the following to the `main` section:

  ```yml
   - title: "Subscribe"
      url: /subscribe-to-bills-blog/
  ```

## Add `ads.txt` file from Disqus

ADS stands for Authorized Digital Sellers. You can read more about ads.txt and the rationale for creating it, at [Ads.txt FAQ](https://help.disqus.com/en/articles/1765332-ads-txt-faq)  Disqus and other companies have cooperated to identify sellers with validated reputations. Disqus expects this file to be present in the root of the site.

1. Create the file `ads.txt` in the root of the repo.
1. Copy the contents of [ADS.txt](https://disqusads.com/ads.txt) into the file `ads.txt`
1. Save the file

This file needs to be maintained monthly. Setup a reminder to regularly compare the latest version of the file with the one local to your site, and update your local copy accordingly.

- [ToDo: write a script to automate this, and reference the script here.]
- [ToDo: write a post how to automate this, and schedule it to run monthly and notify the site admin's list.]

## Add carousel to home page

### Add a Carousel component

There are many carousel components on the Internet only a search away. The following carousel component came from the Jekyllcodex.org site, and was very highly linked, so we will start with this one. See [Slider/Carousel](https://jekyllcodex.org/without-plugin/slider/) for details. Following their instructions....

1. Add the file `_includes/carousel.html`, and copy the contents from [carousel.html](https://raw.githubusercontent.com/jhvanderschee/jekyllcodex/gh-pages/_includes/carousel.html) into the local copy of this file.
1. Add the file `_data/carousel.yml`, and fill it with content similar to this:

  ```yml
  images: 
  - image: /uploads/slider/image1.jpg
  - image: /uploads/slider/image2.jpg
  - image: /uploads/slider/image3.jpg
  - image: /uploads/slider/image4.jpg
  ```

My initial file looked like this, because I am hosting my images on Dropbox, and have to get a sharing link from Dropbox for each image:
  
```yml
images: 
  - image: https://www.dropbox.com/s/xshldyre3ghrye1/Spring%20runoff.jpg?raw=1
  - image: https://www.dropbox.com/s/irttipxfqhpf6sk/AllTrailsInfo.png?raw=1
  - image: https://www.dropbox.com/s/4z10h1qcoj54t4b/Artsy%20water.jpg?raw=1
```

### Instantiate the carousel on the home page

The component needs to be instantiated where it is to be used. We want it on the site's home page

1. Edit `_pages/Home.md`
1. Add the following line in the location where the carousel should appear.

   ```text
    {% raw %}{% include carousel.html height="50" unit="%" duration="7" %}{% endraw %}
   ```

Build the site and validate the carousel appears as expected.

### Troubleshooting: The carousel overlaps the left sidebar

Investigation shows that the `_layout/splash.html` file from the MM theme has far less Liquid template code than the `_layout/single.html` file. The `_layout/splash.html` file will need to be overridden and modified to keep the carousel within the left and right borders of the content.

### Create override for `_layout/splash.html`

Copy the file `_layout/splash.html` from the location where the MM theme was installed ([Finding the files that make up the theme]({{ '/technical/2021/2021-04-24-how-i-setup-this-github-pages-blog-site-part-03.html#finding-the-files-that-make-up-the-theme' | relative_url }})) into the `_layouts` subdirectory below the repo root.

The content changes border on substantial. In summary, we want to add a \<div class="page__inner-wrap"> to the splash layout, and place the `content` tag within this div. The best way to see this is to look at the file in my GitHub repo, [here](https://github.com/BillHertzing/BillHertzing.github.io/blob/SprintForRelease0.04.000/_layouts/splash.html)

Once these changes are made to the splash layout, the carousel will remain constrained to the inner div of the page.

## Add post `bills-blog-pre-release-checklist.md`

See [Bill's Blog Pre-Release Checklist]({{ '/technical/2021/2021-05-22-bills-blog-pre-release-checklist.html' | relative_url }})

## Add post `bills-blog-release-process.md`

See [Bills Blog Release Process]({{ '/technical/2021/2021-05-22-bills-blog-release-process.html' | relative_url }})

## Add any `personal` posts to be published

If you have created any `personal` or `political` posts while working on this feature release, and would like to publish those posts along with this site release, follow the steps in the [Bills Blog Pre-Release Checklist]({{ '/technical/2021/2021-05-22-bills-blog-pre-release-checklist.html' | relative_url }}) post and apply the post validation tests to any posts to be released.

## Validate this post (..part04)

Follow the steps in the [Bill's Blog Pre-Release Checklist]({{ '/technical/2021/2021-05-22-bills-blog-pre-release-checklist.html' | relative_url }}) and apply the post validation tests to this post.

## Validate this Site Release

Follow the steps in the [Bill's Blog Pre-Release Checklist]({{ '/technical/2021/2021-05-22-bills-blog-pre-release-checklist.html' | relative_url }}) and apply the site validation tests to this feature branch.

## Release V0.04.000 of the site along with any new published posts

Follow the steps in the [Bills Blog Release Process]({{ '/technical/2021/2021-05-22-bills-blog-release-process.html' | relative_url }}) post.

## Wrapping up

This concludes the fourth post in this series. This release included a lot of new features, pages, and posts. I'm sure that there will be revisions to all of these for typos, grammar, and general improvements. Future site revisions will support multiple editions of a post, with revision date and ChangeLog for the post. You will (eventually) be able to subscribe to the site's feed and get notifications when a revision is made.

There was also significant work done on a Powershell script outside of this repository which creates the Dropbox sharing links, and formats the links for the galleries and the HTML \<video> tag. When I get the documentation for the `ATAP.Utilities` repository pulled together and published, then I'll include cross-reference to that script and instructions on using it.

Thanks for staying to the end! 😊

Bill Hertzing, May 22, 2021
