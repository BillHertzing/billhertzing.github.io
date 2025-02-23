---
Title: How I setup this GitHub Pages Blog, Part 2
date: 2021-04-17 12:00:50 -0600
tags: Jekyll GitHubPages
description: Second steps in setting up a Jekyll generated blogging site hosted on GitHub Pages which uses any plugin, theme, Jekyll version or Ruby version.
category: technical
---

Welcome to the second part of this series detailing how I setup this blog site hosted on GitHub Pages. If you have not yet seen the first post in the series [How I setup this GitHub Pages Blog Part 01]({{ '/technical/2021/2021-04-06-how-i-setup-this-github-pages-blog-site-part-01.html' | relative_url }}), you should probably give it a quick review, to become familiar with how it all started.

The next steps will be to implement the features specified in [Milestone 0.02.0](https://github.com/BillHertzing/BillHertzing.github.io/milestone/2).  I like to plan my development efforts using GitHub Milestones. They are quick and easy to create and maintain, especially for tiny sites like mine that have no collaborators. Of course I don't ***have*** to create Milestones, but I've found that there is always "feature creep" in releases if I don't take the time to write down what is going into the next release, and what's on tap for some future release. This helps me keep to the release cadence I want, and ensures these posts corresponding to each release don't get too big!

This release is mostly adding files that are common to a good repository, and then adding the ability to add comments to a post.

Lets move on!

## Create `_drafts` folder

Being able to work on a draft of a post, and not have that draft appear on the production site, is important during development. Jekyll has built in support for drafts, using a `_drafts` folder. Simply create the folder `_drafts` under the root of your repository.

## Create a draft post

1. Create the file `how-i-setup-this-github-pages-blog-site-part-02.md` under the new `_drafts` subdirectory. Do not add the *YYYY-MM-DD* prefix to this file.
1. Add the following Front Matter text to the file. Modify it as appropriate for your site. *Note* There is no `date:` key in a draft post. Jekyll will insert that key when you promote the post out of `_drafts` and publish it for the first time.

    ```markdown
    ---
    Title: How I setup this GitHub Pages Blog, Part 2
    tags: Jekyll "GitHubPages"
    layout: post
    description: Second steps in setting up a Jekyll generated blogging site hosted on GitHub Pages which uses any plugin, theme, Jekyll version or Ruby version.
    ---

    Add text you want to see in your second post
    ```

1. Save and commit.
1. Run `bundle exec jekyll serve --drafts`. Jekyll will build the drafts with the current date so they will be easy to find at the top of your (chronologically sorted) post listings.
1. Validate your new post exists locally.

## Community Health files

GitHub encourages authors to ensure their repositories are setup for building communities for healthy and effective collaboration. Details are at [Building communities](https://docs.github.com/en/communities). The first guideline is [Setting up your project for healthy contributions](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions). Among other things, it recommends [Adding a code of conduct to your project](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/adding-a-code-of-conduct-to-your-project) and [Setting guidelines for repository contributors](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/setting-guidelines-for-repository-contributors). But what if you have more than one repository? Do you have to duplicate these files in every one? No, you can setup defaults for these files, and have every repository inherit from your default. Details are in [Creating a default community health file](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file).

### Create `.github` repo

I'm not going to repeat here the instructions you can find on the GitHub doc above. But at this point in the development of this site, I created the new `.github` public repository under my username, and added the `CODE_OF_CONDUCT.md` and `CONTRIBUTING.md` files to the `.github` repo. ToDo: insert jpg

*Note* I changed my GitHub theme to Dark, so the screen shots of GitHub are going to look different from Part 1 of this series!

Now go look at your site's repository in GitHub, drill down into `Insights`, and then the `Community` tab, and you can see that both of these files are now present in this repository's Community Profile! ToDo: insert jpg

### How to link to these default files

Lets add links to both of these files, both here, and in the `_includes/footer.html` template. From the `Insights->Community` page, click the `Code of conduct` link, the in the browser's address bar, copy the URL showing. Mine looks like this: `https://github.com/BillHertzing/.github/blob/main/CODE_OF_CONDUCT.md`. Create a markdown link to this as follows:

<notextile>[Code of Conduct](https://github.com/BillHertzing/.github/blob/main/CODE_OF_CONDUCT.md)</notextile> produces [Code of Conduct](https://github.com/BillHertzing/.github/blob/main/CODE_OF_CONDUCT.md)

Repeat for `CONTRIBUTING.md`.

<notextile>[CONTRIBUTING](https://github.com/BillHertzing/.github/blob/main/CONTRIBUTING.md)</notextile> produces
[CONTRIBUTING](https://github.com/BillHertzing/.github/blob/main/CONTRIBUTING.md)

Edit `_includes/footer.html`, add the following code just below the copyright:
  
```html
<div class="footer-col">
  <p> <a href=https://github.com/BillHertzing/.github/blob/main/CODE_OF_CONDUCT.md>Code of Conduct</a></p>
</div>
<div class="footer-col">
  <p> <a href=https://github.com/BillHertzing/.github/blob/main/CONTRIBUTING.md>CONTRIBUTING</a></p>
</div>
  ```

## Add `ReadMe.md`

The `ReadMe.md` file at the root of a repo will get displayed to visitors on the repo's landing page. Here are some posts with great ideas

- [A Beginners Guide to writing a Kickass README](https://meakaakka.medium.com/a-beginners-guide-to-writing-a-kickass-readme-7ac01da88ab3#:~:text=A%20great%20README%20file%20helps,basic%20introduction%20to%20the%20software.)
- [A template to make good README.md · GitHub](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2)
- [A curated list of awesome READMEs](https://github.com/matiassingers/awesome-readme)
- [awesome-github-badges](chetanraj/awesome-github-badges) - add some badges to the readme
- [badges](https://github.com/aleen42/badges) - To make badges more standard and acceptable.
- [Markdown License badges](lukas-h/license-badges.md)

*Note* If you want to use a badge that refers to any of the repo's Community Health files (like `CONTRIBUTING` or `CODE OF CONDUCT` AND if you want to use ***default*** Community Health files, then specify the repo *GitHubUserName*/.github in the badge's repo field.

1. Create the file `ReadMe.md` in the root of the repo.
1. Edit the file, and add whatever content you think appropriate
1. Commit and push to the GitHub repo.
1. Validate your ReadMe file now displays on the GitHub repo's landing page.

## Add `ChangeLog.md`

Having a ChangeLog for your blog site will help user's understand changes you  have applied

[keep a changelog](https://keepachangelog.com/en/1.0.0/)

If you want to automate the ChangeLog to a degree, it is important that the commits in the repo have meaningful commit messages that are machine readable. Here are some examples of commit messages and tools that can read them.
[Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) also has a large bibliography of tooling around Conventional Commits
[Universal Changelog Generator action](https://github.com/marketplace/actions/universal-changelog-generator).

***If you want to automate the generation of the ChangeLog, you need to write your commits in a standard format***

I have a feature identified in the Far Future Milestone for automation in this area, so I'll start using commits in the style specified by [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/). According to that document, commits I've already made will just be ignored by the automated tooling, and the ChangeLog can be manually edited as I have done for the initial ChangeLog I create below.

1. Create the file `ChangeLog.md` in the root of the repo.
1. Edit the file, and add content appropriate for the site's "Birthday", and Release V1.01.1
1. Commit and push to the GitHub repo.
1. Validate the `ChangeLog.md` file is listed on the GitHub repo's `<>Code` landing page.

## Add Commit Message Template

To make it easier to create commit messages that follow a standard template, add a git commit message template to the repository and configure git to use that file. The standardized commit message template I chose for my initial version of the template can be found at [Keeping Git Commit Messages Consistent with a Custom Template](https://dev.to/timmybytes/keeping-git-commit-messages-consistent-with-a-custom-template-1jkm).

1. Create the file `git.commit.template.txt` in the subdirectory `.github`.
1. Add text similar to the following to the template `.txt` file, and save it.

    ```Text
    # ----------------------------------------------------------60
    WIP 
    # Header - type(scope): Brief description [ FEAT BUGFIX BREAKINGCHANGE DOC STYLE REFAC PERF TEST DATA BUILD CI CHORE SPEC WIP ]
    # ----------------------------------------------------------60
    #   Commit Key is Case insensitive, 2-letter minimum
    #    * FEAT             A new feature - SemVar PATCH
    #    * BUGFIX           A bug fix - SemVar MINOR
    #    * BREAKINGCHANGE   Breaking API change - SemVar MAJOR
    #    * DOC              Change to documentation only
    #    * STYLE            Change to style (whitespace, etc.)
    #    * REFAC            Change not related to a bug or feat
    #    * PERF             Change that affects performance
    #    * TEST             Change that adds/modifies tests
    #    * BUILD            Change to build system
    #    * CI               Change to CI pipeline/workflow
    #    * SPEC             Changes to a project Specification
    #    * CHORE            General tooling/config/min refactor
    #    * WIP              General ongoing design work on a FEAT or BUGFIX
    # ----------------------------------------------------------
    
    # ------------------------------------------------------------------------------80
    # Body - More description, if necessary
    # ------------------------------------------------------------------------------80
    
    # ------------------------------------------------------------------------------80
    # Footer - Associated issues, PRs, etc.
    See Milestone Release 0.02.00
    #    * Ex: Resolves Issue #207, see PR #15, etc.
    # ------------------------------------------------------------------------------80
    ```

1. Run `git config --global commit.template .github/git.commit.template.txt` to add the template to your global git config.
1. Run `git config --global core.editor "code --wait"` to add VSC as git's editor of choice. See also [MarredCheese's answer to StackOverflow question](https://stackoverflow.com/questions/30149132/multiline-git-commit-message-in-vscode/54139152#54139152).
1. Run `git commit -a`
1. Validate that VSC is the editor for the commit message which comes up pre-populated with the template's text.
1. Click on the SCM icon in the sidebar. Validate that what was the single line commit message text box at the top has expanded to contain the non-comment template lines, and blank lines wherever there was a comment. Hmmm... Wonder how we can have only non-comment lines from the template in the SCM editor's commit text box, yet have the full template text at just a keystroke away if needed for reference  ToDo: Figure that out.

When doing design work on a feature, it saves some time if you edit the template to add a reference to the feature specification or the release milestone that calls out the feature under development. Likewise if you are working on a post, and doing the edit/build/view dance, editing the template may save you some time and keystrokes.

## Add Bug Report and Feature Request Issue Templates

Bug Report and Feature Request Issue Templates will make it easier for contributors to create issues for bug reports and feature requests. Standardizing on formats for these items early in the site's development will make it easier for automation in the future. These files can also be part of the `Community Health Files`, and default versions of these can be placed in the user's or organization's `.github` repository and shared amongst all of a GitHub user's or organization's repositories.

Details on how to use the issue templates from the Community Health repo are at:

- [Configuring issue templates for your repository](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository).
- [Configuring the template chooser]- [https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository#configuring-the-template-chooser]
- [https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)
- [About issue and pull request templates](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/about-issue-and-pull-request-templates).

1. Use the tool of your choice to navigate to the root of your `.github` repository that was created above in [#Create`.github`repo].
1. Create a new subdirectory `.github` in the root of `.github` (yes, it ***is*** confusing).
1. Create a new subdirectory `ISSUE_TEMPLATE` in the subdirectory `.github` in root of the `.github1 repository.
1. Create a new file `Bug_Report_Template.md` in the new subdirectory `ISSUE_TEMPLATE`.
1. Add text similar to the following to the template `.md` file, and save it.

    ```text
    ---
    name: Bug Reporting issue
    about: Use this template for reporting a bug.
    title: "[DATE]: [Bug Name]"
    labels: Bug issue, needs triage
    assignees: *DefaultAssigneeGithubUserName*
    ---
    
    **Do you want to request a *feature* or report a *bug*?**
    <!-- Please ask questions on StackOverflow or the *YourProjectName* Gitter (https://gitter.im/*TBD**). Questions will be closed. -->
    
    **What is the current behavior?**
    
    **If the current behavior is a bug, please provide the steps to reproduce.**
    <!-- A great way to do this is to provide your configuration via a GitHub gist. -->
    
    **What is the expected behavior?**
    
    **If this is a feature request, what is motivation or use case for changing the behavior?**
    
    **Please mention other relevant information such as your hardware, OS and version, Browser and version, and if the problem is repeatable on other hardware/OS/Browser **
    ```

1. Create a new file `Feature_Request_Template.md` in the new subdirectory `ISSUE_TEMPLATE`.
1. Add text similar to the following to the template `.md` file, and save it.

    ```text
    ---
    name: Feature Request issue
    about: Use this template for requesting a new feature.
    title: "[DATE]: [Feature Name]"
    labels: Feature Request, needs triage
    assignees: *DefaultAssigneeGithubUserName*
    ---
    
    **New Behavior**
    <!-- Please ask questions on StackOverflow or the *YourProjectName** Gitter (https://gitter.im/*TBD*). Questions will be closed. -->
    
    **Suggested New feature Name**
    
    **what is motivation or use case for changing the behavior?**
    ```

1. Commit the change made to .github repository and sync the changes with the remote.
1. Validate the new templates are available in the static site repository. ToDo: insert jpg

## Add the `jekyll-timeago` plugin

One of the main reasons that I am not using GitHub Pages built-in Jekyll site generator is so that I can use the entire ecosystem of Jekyll plugins. Github limits you to a white-list of approved plugins. `jekyll-timeago` is a nice simple non-approved plugin that adds simple functionality to calculate how long ago a date is. To ensure we can use non-approved plugins, lets start with this one.

### Install the `jekyll-timeago` plugin locally

Run `gem install jekyll-timeago` in the Powershell window (at the base of the repo).  **Make a note of the version installed**, it will be used in the next step, to the right of the `~>` in the `gem ...` line.

### Add the `jekyll-timeago` plugin to the `Gemfile`

1. Edit the `Gemfile` in the base of the repo.
1. Add `gem "jekyll-timeago", "~> 0.14.0"` to the `Gemfile` in the block `group :jekyll_plugins do`. The block should look like this at this point in the development of the site.

    ```yml
    group :jekyll_plugins do
    gem "jekyll-feed", "~> 0.12"
    gem "jekyll-timeago", "~> 0.14.0"
    end
    ```

1. Save the file.

### Add the `jekyll-timeago` plugin to the `_config.yml` file

1. Edit the `_config.yml` in the base of the repo.
1. add `-jekyll-timeago` to the plugins key. The block should look like this at this point in the development of the site.

    ```yml
    plugins:
    - jekyll-feed
    - jekyll-timeago
    ```

- The next line looks like this in the post's `.md` file.

page publication date was {{ "{{" }} page.date }}, which was {{ "{{" }} page.date \| timeago }}
  
- Which renders as:

page publication date was {{ page.date }}, which was {{ page.date | timeago }}

## Put the most recent releases tag Semantic Version in the `footer` template

The plugin [jekyll-version-plugin](https://github.com/rob-murray/jekyll-version-plugin) will get the latest releases tag from the local git repository.

### Install the `jekyll-version-plugin` plugin locally

- Run `gem install jekyll-version-plugin` in the Powershell window (at the base of the repo). **Make a note of the version installed**, it will be used in the next step, to the right of the `~>` in the `gem ...` line.

### Add the `jekyll-version-plugin` plugin to the `Gemfile`

1. Edit the `Gemfile` in the base of the repo.
1. Add `gem "jekyll-version-plugin", "~> 2.0.0"` to the `Gemfile` in the block `group :jekyll_plugins do`. The block should look like this at this point in the development of the site.

    ```yml
    group :jekyll_plugins do
      gem "jekyll-feed", "~> 0.12"
      gem "jekyll-timeago", "~> 0.14.0"
      gem "jekyll_version_plugin", "~> 2.0.0"
    end
    ```

1. Save the file.

### Add the `jekyll-version-plugin` plugin to the `_config.yml` file

1. Edit the `_config.yml` in the base of the repo.
1. add `-jekyll-version-plugin` to the plugins key. The block should look like this at this point in the development of the site.

    ```yml
    plugins:
    - jekyll-feed
    - jekyll-timeago
    - jekyll_version_plugin
    ```

- The next line looks like this in this post's `.md` file.

project_version returns: {{ "{%" }} project_version %}
  
- Which renders as:

project_version returns:  releases/0.01.000-28-g1b44469  *** The semantic version and the commit hash will be different each time this is run***

### Parse the full tag into a string suitable for display

- The next line looks like this in this post's `.md` file.

{% raw %}

latest release tag: {% capture long_tag_name %}{% project_version %}{% endcapture %}{{ long_tag_name \| remove: 'releases/' \| split: '-' \| first \| prepend: 'V' }}
{% endraw %}

- Which renders as:

latest release tag: {% capture long_tag_name %}{% project_version  %}{% endcapture %}{{ long_tag_name | remove: 'releases/' | split: '-' | first | prepend: "V" }}

### Place the results in the `footer.html` file

1. Edit `_includes/footer.html`.
1. Add the following just after the `CONTRIBUTING`

```MarkDown
   {% raw %}<div class="footer-col">
     <p>Site Release {% capture long_tag_name %}{% project_version %}{% endcapture %}{{ long_tag_name | remove: 'releases/' | split: '-' | first | prepend: "V" }}</p>
   </div>{% endraw %}
```

1. Save the `footer.html` file
1. Run `bundle exec jekyll serve --drafts`
1. Validate the site's release version information appears at the bottom of each page and each post, including the landing page.
1. Commit the changes with an appropriate commit message.

## Add `jekyll-include-cache` plugin

Build times for the static site locally can be significantly improved over the out-of-the-box experience. Details of one such approach can be found at [How I reduced my Jekyll build time by 61%](https://forestry.io/blog/how-i-reduced-my-jekyll-build-time-by-61/). This early in the creation of this site, I don't expect to see a whopping improvement, but getting the speedup steps done now should keep me from writing incompatible code in future releases.

### Benchmark the current build time

1. Run `bundle exec jekyll build --profile` to use Jekyll's built in profiler. Here are the results:

  ````Text
  | PHASE      |   TIME |
  +------------+--------+
  | RESET      | 0.0001 |
  | READ       | 0.0900 |
  | GENERATE   | 0.0043 |
  | RENDER     | 1.1278 |
  | CLEANUP    | 0.0105 |
  | WRITE      | 0.0184 |
  +------------+--------+
  | TOTAL TIME | 1.2511 |
  ```

1. Run `measure-command { bundle exec jekyll build  | out-host }` to use Powershell's Measure-Command applet. THis only works when building on Windows. Here are the results:

  ```text
    TotalSeconds      : 4.1939049
  ```
Powershell's measurement includes all the overhead time to invoke Ruby and to clean up after the generation. This number is much closer to the "clock-time" I experience when generating the site.

### Install the `jekyll-include-cache` plugin locally

- Run `gem install jekyll-include-cache` in the Powershell window (at the base of the repo). **Make a note of the version installed**, it will be used in the next step, to the right of the `~>` in the `gem ...` line.

### Add the `jekyll-include-cache` plugin to the `Gemfile`

1. Edit the `Gemfile` in the base of the repo.
1. Add `gem "jekyll-include-cache", "~> 2.0.0"` to the `Gemfile` in the block `group :jekyll_plugins do`. The block should look like this at this point in the development of the site.

    ```yml
    group :jekyll_plugins do
      gem "jekyll-feed", "~> 0.12"
      gem "jekyll-timeago", "~> 0.14.0"
      gem "jekyll_version_plugin", "~> 2.0.0"
      gem "jekyll-include-cache", "~> 0.2.1"
    end
    ```

1. Save the file.

### Add the `jekyll-include-cache` plugin to the `_config.yml` file

1. Edit the `_config.yml` in the base of the repo.
1. add `-jekyll-include-cache` to the plugins key. The block should look like this at this point in the development of the site.

    ```yml
    plugins:
    - jekyll-feed
    - jekyll-timeago
    - jekyll_version_plugin
    - jekyll-include-cache
    ```

### Benchmark the improved build time

1. Run `bundle exec jekyll build --profile` to use Jekyll's built in profiler. Here are the results:

  ````Text
  | PHASE      |   TIME |
  +------------+--------+
  | RESET      | 0.0001 |
  | READ       | 0.0943 |
  | GENERATE   | 0.0044 |
  | RENDER     | 1.1449 |
  | CLEANUP    | 0.0109 |
  | WRITE      | 0.0181 |
  +------------+--------+
  | TOTAL TIME | 1.2727 |
  ```

1. Run `measure-command { bundle exec jekyll build  | out-host }` to use Powershell's Measure-Command applet. This only works when building on Windows. Here are the results:

  ```text
    TotalSeconds      : 4.2954848
  ```

HaHaHaHa - adding the cache increased the build time infinitesimally! But as any performance tester will tell you, it is important to run timing tests like these hundreds of times, throw out outliers, and take the average of the results. I'm not going to do that yet in the development of this site, but I'll add a task to do this into the later Milestones of the project.

- Commit the changes with an appropriate commit message.

## Add draft post `Why I Wanted A Blog` to `political` category

If you are not planning to implement post categories, you can ignore the following two sections. If you want catagories, follow along with these instructions, and modify them to fit your specific needs.

1. Create a subdirectory below the repo root named `political`.
1. Add a new file in the `_drafts` subdirectory (under the repo root) called `Why I Wanted A Blog.md`
1. Add the following to the draft post:

    ```markdown
    ---
    Title: Why I wanted a Blog
    tags: 
    layout: post
    description: The motives that led me to start this site
    category: political
    ---
    
    ## TL DR
    
    - Replace this line with all the text you want to put into this document.  
    ```

1. Save the file.
1. Run `bundle exec jekyll serve --drafts` 
1. Validate that the post appears on the home (landing) page, and the contents of the post appear as expected.
1. Commit the changes with an appropriate commit message.

## Add draft post `Welcome to the Personal section of my site` to `personal` category

This part creates the second category, if you want them.

1. Create a subdirectory below the repo root named `personal`.
1. Add a new file in the `_drafts` subdirectory (under the repo root) called `Welcome to the Personal section of my site.md`
1. Add the following to the draft post:

    ```markdown
    ---
    Title: Welcome to the Personal section of my site
    tags: Introduction Personal
    layout: post
    description: Explanation of how to register for and use the personal section of this site.
    category: personal
    ---
    
    ## TL DR
    
    Replace this line with all the text you want to put into this document.
    ```

1. Save and commit the file
1. Run `bundle exec jekyll serve --drafts` 
1. Validate that the post appears on the home (landing) page, and the contents of the post appear as expected.

## Making the third release of the site

I'm happy now with the enhancements I've made to the blogging site. It's time to wrap up this release. I'm going to update the checklist for "release" chores, and eventually will automate as much as I feel is worth putting in the time to do.

### Site Minor Release checklist

1. Ensure the `main` branch builds cleanly, without the `--drafts` option.
1. Review any `warnings` that appear in VSC's `problems`. pane. Clean up the underlying issue, or decide they are OK to live with for this release. Commit any changes made during this step to `main` and push to the remote.
1. Update the ChangeLog.md. I simply cleanup the Milestone text and add it to ChangeLog. I'll get around to automating this from the Git commit messages in a future release. Commit the ChangeLog.md and push it.
1. Publish the draft ` How I setup this GitHub Pages Blog, Part 3` post into _technical
1. Build the `main` branch again.
1. Commit and sync with remote

Once you have committed all the changes you want for Release 0.02.0,

1. Run `git tag -a releases/0.02.000 -m "Bill's Blog, second wave of features"` (modify the command as appropriate for your site)
1. Run `git tag` which will list all existing tags and verify the tag is there.
1. Run `git push --tags` to push the release tag to GitHub
1. Validate that the Deploy github Action ran.
1. Validate that the new features appear on the public site

## Wrapping up

This concludes the second post in this series. I've already had to make changes to this post after publishing the first edition when Release 0.02.000 went live. I've still not built a post revision tracking system into the blog site, but eventually I'll be able to come back and revise any post, and the post will show an `edition` and `publication date` for the original edition and all revisions, along with change bars or a "what's changed" document for each post.

Comments for posts should be enabled soon, until then, please use the Issues on this repository to communicate with me, if you find errors or have questions.

Thanks for staying to the end. 😊

Bill Hertzing, April 17, 2021
