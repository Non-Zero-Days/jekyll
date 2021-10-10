# Title

**Watch the video [here](https://youtu.be/LxEY3YQLUI4)**

## Prerequisites

- [Ruby](https://rubyinstaller.org/downloads/)
- [Visual Studio Code](https://code.visualstudio.com/)

## Loose Agenda

- Create a website from markdown using Jekyll

## Step by Step

### Setup Playground

Create a directory for today's exercise and navigate to it in a terminal instance. 

### Create a Jekyll Site

Using `gem` let's install `Bundler` and `Jekyll`.

Run `gem install bundler jekyll` from the terminal instance.

Next, run `jekyll new .` to create a jekyll template in the current directory.

Verify it worked by running `bundle exec jekyll serve` and navigating to [http://127.0.0.1:4000/](http://127.0.0.1:4000/).

**Note - If `bundle exec jekyll serve` fails then you may have to run `bundle add webrick`**

### Markdown Pages

At it's simplest, any markdown file in the directory will be processed for inclusion in the HTML hosted output from Jekyll.

Fetch `Fruit.md` from [the Markdown exercise](https://github.com/Non-Zero-Days/markdown) and add it to this directory.

Add the following snippet to the top of the Fruit.md file:

```yml
---
layout: page
---
```

Serve the HTML output via `bundle exec jekyll serve` and navigate to [http://127.0.0.1:4000/Fruit.html](http://127.0.0.1:4000/Fruit.html)

### Front Matter

At the top of each markdown file in the directory, you can add YAML surrounded by `---` to declare page level variables. Alternatively, you can define site level variables via a `_config.yml` file in the root directory.

At the top of `Fruit.md` let's adjust the front matter to include a new variable

```yml
--- 
layout: page
favorite_fruit: Banana
---
```

Let's add a new heading just below `# Fruit`
```md
# Favorites

{{ page.favorite_fruit }}

```

Serve the HTML output via `bundle exec jekyll serve` and navigate to [http://127.0.0.1:4000/Fruit.html](http://127.0.0.1:4000/Fruit.html) to observe the output.

Next, let's adjust the `_config.yml` to include the following line:
```yml
favorite_fruit: Green Apple
```

Then adjust the `Favorites` section of `Fruit.md` to include 
```md
{{ site.favorite_fruit }}
```

Serve the HTML output via `bundle exec jekyll serve` and navigate to [http://127.0.0.1:4000/Fruit.html](http://127.0.0.1:4000/Fruit.html) to observe the output.

*Note that you'll have to stop and start the serve process in order to see changes in `_config.yml` manifest.*

### Posts

Jekyll supports a concept of blog posts. Posts are markdown files which are located in the `_posts` directory and named with the format `YEAR-MONTH-DAY-title.md`

By default, the template uses the `Minima` theme within which the `home` layout includes iterating over posts in the root URL.

Navigate to the `_posts` directory and observe the `2021-10-10-welcome-to-jekyll.markdown` file which is linked on the home page of our site. 

Move the `Fruit.md` file into the `_posts` directory. Rename it to `1999-01-01-Fruit.md` and adjust the layout in the front matter of the file to `layout: post`.

Serve the HTML output via `bundle exec jekyll serve` and navigate to [http://127.0.0.1:4000/](http://127.0.0.1:4000/). Observe that the `1999-01-01-Fruit.md` document is listed in the front page.

The `Minima` theme filters the posts to not include future dates.

Rename the `1999-01-01-Fruit.md` file to `2040-01-01-Fruit.md` and serve the site once again. Observe that the document is no longer listed on the front page. 

Rename the file to `2020-01-01-Fruit.md`.

### Data Files

Jekyll also supports using `yml`, `json`, `csv`, and `tsv` files as data files from a `_data` directory.

Create a `_data` directory within which create a file named `fruit.yml`. 
```yml
- name: Apple 
  tasty: Yes

- name: Kiwi  
  tasty: Yes

- name: Orange
  tasty: Yes

- name: Banana
  tasty: Yes

- name: Pear  
  tasty: Yes
```

In the `2020-01-01-Fruit.md` file, create a new `## Data` heading under `## Favorites` as follows

```md
## Data

{% for fruit in site.data.fruit %}
- The fruit named **{{ fruit.name }}** is generally tasty. Data suggests this is `{{ fruit.tasty }}`
{% endfor %}
```

Serve the HTML output via `bundle exec jekyll serve` and navigate to [http://127.0.0.1:4000/2020/01/01/Fruit.html](http://127.0.0.1:4000/2020/01/01/Fruit.html). 

Observe the data has been iterated over in the generated output.

### Themes

Jekyll also supports the concept of themes. Many themes are openly shared with the community. Let's swap our current `Minima` theme with the `jekyll-theme-minimal` theme.

In the root directory, adjust the `Gemfile` to include the following additional line 
```Gemfile
gem "jekyll-theme-minimal"
```

From a terminal instance in the root directory, run `bundle install`

Adjust the `_config.yml` line `theme: minima` to instead be `theme: jekyll-theme-minimal`.

Serve the HTML output via `bundle exec jekyll serve` and navigate to [http://127.0.0.1:4000/2020/01/01/Fruit.html](http://127.0.0.1:4000/2020/01/01/Fruit.html). 

**Note that not all pages will generate as they did before. The jekyll-theme-minimal theme does not include a home layout and thus the root URL is blank instead of displaying a list of posts.**

Congratulations on a non-zero day!

## Additional Resources

- [Jekyll Documentation](https://jekyllrb.com/)
- [Markdown Cheatsheet](https://www.markdownguide.org/cheat-sheet/)
- [Bundler documentation](https://bundler.io/)
- [Minima Theme Repository](https://github.com/jekyll/minima)
- [Minimal Theme Repository](https://github.com/pages-themes/minimal)
