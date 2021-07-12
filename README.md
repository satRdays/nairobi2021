# satRday_site_template

## How to get an official satRdays website

You can very easily fork this repo and work off of it

__HOWEVER__

If you are starting a satRdays event, then the best thing to do is join the [slack R User Groups Workspace](https://join.slack.com/t/rusergroups/shared_invite/enQtMjEyNDA3MzcyMjczLTE3NWEzNjQ3MjZiMWM0OGE2ZWFiZDliNTY4NTJjYWY1NGNjMmNlNDUzNzkzOTZmMDBjYjRiZjFhNjk4MDY0ZGY) and go to the `#satrdays-website` channel and ask about setting up a website, tagging @DaveParr.

here is an __EXAMPLE REQUEST__ that you can copy, edit, and paste into the channel:

> Hi @DaveParr, I would like a website to promote my event in [your city] that will be held in [the year of the event]. My GitHub user name is [your username]. Thanks!

This will mean that:

* we create a repo for you in the satRdays GitHub Organisation
* we will set you up as a member of the satRdays GitHub Organisation
* we will set up a GitHub Team in the GitHub Organisation for you to manage your new site
* we will set up hosting for the repo in the satRdays organisation on [netlify](https://www.netlify.com/) to a domain like this: `myevent.satrdays.org`

## Support in slack

The #satrdays-website channel is now filled with people who have used this template. This is your best resource for asking questions about how to use and edit the template.

## What I can do

I can give you most of a website for satRdays events, ready (almost) out of the box. I have a number of sections to help you out:
* Event description
* Event location
  + With map
* Embedded tickets
  + Tito
  + Ticket Tailor
  + Eventbrite
* Call for papers
  + Sessionize
* Speaker Bios
* Talk descriptions
* Schedule
* Important Dates
* Links to satRdays Code of Conduct and Diversity materials

If you want to have a website set up, please request this in the #satrdays-website slack channel of the R User Group organizers Slack (rusergroups.slack.com), tagging @DaveParr.

## Organiser tasks

### Build locally

You can locally build your site using the shell command `hugo serve` in the working directory of the project, as long as you have it [installed on your machine](https://gohugo.io/getting-started/installing/). You can then open you browser to the link that is listed in the message (probably localhost:1313), and see your changes. Hugo features fast builds and hot-reload so you should be able to see _most_ changes simply after saving the relevant file.

#### Initialise the sub-modules

When you locally clone your events repo to your machine, the first time you build the project you _might_ need to initialise the sub-modules which contain the theme. You can avoid this by cloning with the `--recurse-submodules` option, similar to this:

```
git clone --recurse-submodules https://github.com/satrdays/[my_conference_repo]
```

If you fogot that, you can always run this command _after_ you cloned the repo normally:

```
git submodule update --init
```

### Edit the base url in `config.toml`
Change 
```
baseurl = "https://satrdays-event-template.netlify.com/"
```
to
```
baseurl = "https://yourcity20XX.satrdays.org/"
```
otherwise, images you upload to your site won't work.

### Customise the config
The file [config.toml](https://github.com/satRdays/satRday_site_template/blob/master/config.toml) gives you access to a number of points on the site, mostly using [site params](https://gohugo.io/variables/site/#the-site-params-variable).

A high level overview of these features:
* `enable` 
  + boolean to render or hide that section
* `title`/`subtitle`/`description`/`button text`/...
  + strings to display text in that position
* `bg`
  + boolean to toggle lightly shaded backgrounds on or off for that section
* `eid`/`accountevent`/`eventviewid`/`CfSpage`
  + strings that are part of a url (that are usually part of an iframe) to link to a service for tickets/Call for papers

### Include a new talk desciption
* Talks are generated from `Talk0X.yaml` files in `data/projects/`
* Each talk should have similar structures (some values may be missed or blank) based on the included examples, and be in its own file

### Include a new bio
* Speaker/organiser bios are generated from `Speaker0X.toml` files in `data/speakers/`
* Each speaker should have similar structures (some values may be missed or blank) based on the included examples, and be in its own file

## What if I need even more customistation?
In the hopefully rare event that even more specific material is needed you can explore the following. Make use of the [hugo inheritance method](https://gohugo.io/templates/lookup-order/#hugo-layouts-lookup-rules-with-theme) to override defaults where applicable, rather than modify the defaults in place.

### CSS/style
* Copy the base `hugo-satrdays-theme/static/css/style.css` into `/static/css/style.css`
  + This will now be the style sheet for your website, overriding the themes
  
### New Section/Custom Section
* Either 
  + find a [partial](https://gohugo.io/templates/partials/) from `/layouts/partials` in the existing themes you want to base your work on, copy it to the project `/layouts/partials`, and modify the copy
  + write a new `myfile.html` from scratch and include it in the project `/layouts/partials`
* then make sure that it is referenced in `index.html`

## What I am
I am a [Hugo](//gohugo.io) website, with two themes. [Agency](https://github.com/digitalcraftsman/hugo-agency-theme) provides the base layer of theming, with a custom [satRday](https://github.com/satRdays/hugo-satrdays-theme) theme which overides some areas.

More information on installing [hugo](https://gohugo.io/getting-started/installing/), including setting it up for [local previews](https://gohugo.io/getting-started/usage/) can be found in the official docs.

## Some notes and gotchas
As the design is strongly based on the `hugo-agency-theme`, naming conventions are not obvious in certain situations
* The `talks` section of `hugo-satrdays-theme` is built from the `portfolio` section of the `hugo-agency-theme`
* The `important dates` section of `hugo-satrdays-theme` is built from the `about` section of the `hugo-agency-theme`
* The `speakers` section of `hugo-satrdays-theme` is built from the `team` section of the `hugo-agency-theme`
* The `sponsors` section of `hugo-satrdays-theme` is built from the `clients` section of the `hugo-agency-theme`

## Video documentation
- [How to configure the site](https://youtu.be/3b7y_wan_d8)

## Administrator tasks

### Traditional method - Set the repo as a mirror the main repository

1. Open Git Bash (or your command-line interpreter).

2. Create a bare clone of the repository.

  ```
  git clone --bare https://github.com/satRdays/satRday_site_template
  ```

3. Make a GitHub Repo named `[cityYEAR]` in all lower case, no spaces. Don't initialize it with a README.

4. Mirror-push to the new repository.

```
cd satRday_site_template.git
git push --mirror https://github.com/satRdays/[cityYEAR].git
```

5. Remove the temporary local repository you created in step 1.

```
cd ..
rm -rf satRday_site_template.git
```

5. Make a GitHub Team and add the conference organisers as members

6. Add the GitHub Team to the repo you made as 'Admin'

### New cool method - Set the repo up from template

1. Press the 'Use this template' button

2. Set the owner of the repo to be 'satrdays' organisation

3. Set the repository name to be `[cityYEAR]`

4. Set the repo to be 'Public'

5. Create repository from template

6. Make a GitHub Team and add the conference organisers as members

7. Add the GitHub Team to the repo you made as 'Admin'

There is now WIP on automating deployment using the scripts in [this repo](https://github.com/satRdays/automation)

### Netlify

1. Make a new deploy from GitHub in the Satrdays Netlify Team

2. The build command is `hugo` the build directory is `public`

3. Rename the default domain to [cityYEAR].netlify.com

4. Add the additional domain [cityYEAR].satrdays.com
