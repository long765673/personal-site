---
title: "Create your own personal website or blog for free"
date: 2021-03-28T12:06:25+08:00
description: How to create your own personal website
menu:
  sidebar:
    name: Create your own personal website or blog for free
    identifier: website tutorial
    weight: 10
---

## Introduction

Having a personal website or a business site has never been so important. Covid19 pandemic forced a lot of people to 
close the doors of their businesses to physical visitors and had to quickly transition to e-commerce (see
[1](https://www.theedgemarkets.com/article/ecommerce-fuelling-ecommerce-boom),
[2](https://blogs.lse.ac.uk/seac/2020/10/20/the-impact-of-covid-19-on-sme-digitalisation-in-malaysia/)),
some of them choosing existing platforms like Facebook, some others paying for web development companies. 
For newly graduated professionals struggled with a new way to be relevant when applying for jobs and being interviewed 
if remote scenarios (see [3](https://www.malaymail.com/news/malaysia/2020/09/28/higher-education-minister-foresees-75000-fresh-grads-struggling-to-get-jobs/1907493)).

For this reason we decided that we could help the community by preparing a simple guide that anyone with some computer
experience could follow and allow them to create their own website for free if they put some time into it.

In this guide we will be using a couple of [Open Source](https://en.wikipedia.org/wiki/Open_source) tools, free internet
services to allow hosting, publishing and owning a domain. You will need a computer with Internet and Windows OS, 
it should be easy enough to follow also on MacOS and Linux systems.

## Static sites

In order to be able to run our site for free, it has to be a static site, a static site as the name implies, 
is a site that never changes, every user visiting the site will see the same pages, in contrast with a dynamic site, 
that for example users could login and have some customized data displayed to them, dynamic sites require a backed server
to process and render the data specifically to the user while static does not, making it very "cheap" to run, so much, 
that services like GitHub allows you to do it for free.

If you already have some HTML and CSS coding experience you could create your own static site your self without needing
any static site generator tool. The advantage of choosing one is that it reduces significantly the amount of coding 
knowledge you need to almost nothing, you only need to understand how to edit text and configuration files.

For this guide we have chosen Hugo.

### Hugo - A static site generator

[Hugo](https://gohugo.io) is modern and very popular static site generator written in the Go language ([Golang](https://golang.org/)) 
which also happens to be Open Source and free to use. It has a big community and a huge variety of themes to chose from. 
We will go in detail what we mean by "themes" in the next sections.

### Using themes

Now that you understand a bit more of how to create and run a very simple static site with Hugo, lets spice things up, 
if we wanted we could create our own site in Hugo from scratch, this will require to know some HTML, CSS, templating and 
some of the internals for Hugo to create our own 100% customized site. But there is a easier option, as mentioned before,
Hugo has a big community and they offer a huge variety of prebuilt sites, these are called themes. 
You can navigate the themes here: <https://themes.gohugo.io/>

Find one you like for your site, depending on the purpose of it, you may choose from, a personal site, a blog, or something else.

For this guide we will be using [Ananke](https://themes.gohugo.io/gohugo-theme-ananke/) theme.

### Running Hugo on Windows

Lets first install Hugo and some other tools we will be using for hits guide then we can get familiar creating a basic site 
and making local modifications by using the Windows PowerShell.

For these guide we recommend using [Chocolatey](https://chocolately.org), a package manager for Windows to install the prerequisites.\
Follow this guide to install Chocolatey if you don't have already: [https://chocolatey.org/install](https://chocolatey.org/install)
If you run into any problems installing it you can check this [detailed video of the instalation](https://www.youtube.com/watch?v=7Cp2LS9eE3c).

After having Chocolatey installed, in the same PowerShell terminal run the following commands:

`choco install hugo -confirm`

Hugo as we said is the static site generator, and we will be using it to run our site locally in our computers.

`choco install git -confirm`

Git is a version control system for tracking changes in computers files specifically source code. 
It is a great tool for collaborating with other people and it is necessary to interact with GitHub.

`choco install github-desktop`

GitHub Desktop it is a UI for Git and will simply the process of uploading (pushing) source code to GitHub.

`choco install vscode`

VSCode is a powerful text editor that we wil be using to modify any file related to our website.

Great! Now you have all the tools you need installed on your machine, close your administrative terminal and continue
to the next section.

### Create a GitHub account

For this guide we will be using a couple of free features from GitHub. On GitHub you will be storing the source code
for your site but also you will be using a feature called GitHub Pages to host the final site on the Internet.
GitHub Actions will help to automate the process of publishing changes to GitHub Pages.
Go a head and create a free account on GitHub:
[https://github.com/join](https://github.com/join)

### Create a repository

Now that you have an account its important to mention tht GitHub Pages are linked to GitHub repositories, 
in short, the code that you put in a repository can become available as a GitHub page.

Login if you haven't already and create a new repository in GitHub, this can be called `personal-site`. A repository
is where you  will store all the code for your project, if you wanted to create another site in the future, you will
need to create a new repository and follow the same steps in this guide.

You should see something like this:

![New Repository was created](/posts/personal-website-tutorial/swappy-20210329_122533.png)

We will use the command in the red square in the next steps.

Now that you have your new code repository for your website, we need to configure the access from our computer to
GitHub. This way, everytime you do a `git push` it will know who you are with needed passwords.

### Adding SSH Key

To configure this access you will need to create an SSH key, this is necessary to be able to send code to GitHub.

Open a new PowerShell terminal (non-administrative this time) and write:

`ssh-keygen -C <your-email> -t rsa`

It will ask you if you are OK to write the key under `C:\Users\<your-user>/.ssh/id_rsa`

Just type enter to agree.

Next, it will ask you if you would like to add a passphrase (password) to encrypt the key, this is very recommended but not required.
Choose one, and continue.

It takes a second or two and you will see some *randomart* in the screen similar to this:

```
+---[RSA 2048]----+
|    .      ..oo..|
|   . . .  . .o.X.|
|    . . o.  ..+ B|
|   .   o.o  .+ ..|
|    ..o.S   o..  |
|   . %o=      .  |
|    @.B...     . |
|   o.=. o. . .  .|
|    .oo  E. . .. |
+----[SHA256]-----+
```

This means your key has been successfully generated. 
An SSH key consist of 2 files a public: `id_rsa` and private key `id_rsa.pub` for our case.

The private should never be shared, and it should stay in your computer only. 
On the other hand the public key, is the one you will be giving away, in this case to GitHub, 
but also if you wanted to log in into a Linux server.

Print the contents of the public key:

`cat C:\Users\<your-user>/.ssh/id_rsa.pub`

Copy this, and the navigate to you SSH keys in your GitHub Settings (<https://github.com/settings/keys>)

![swappy-20210327_185546.png](/posts/personal-website-tutorial/swappy-20210327_185546.png)

Click on **New SSH key** > Add a title (your email its fine) and paste they contents of the public key in the text box. 
Click **Add SSH key**.

Now you are ready to push code into GitHub!

### Create new Hugo site

In the same PowerShell window, navigate to your Documents directory with the following command `cd $HOME/Documents`

![powershell_home.png](/posts/personal-website-tutorial/powershell_home.png)

Next, we will tell Hugo to create a new site, choose a name for it, something like `personal-site`

`hugo new site <sitename>`

After running this command, Hugo will create a folder with the same name and with multiple files in side, navigate to that directory with:
`cd <sitename>` if you list the files inside using `ls`, it should look something like:

![powershell_personal-site.png](/posts/personal-website-tutorial/powershell_personal-site.png)

Now we need to initialize this new project as a Git repository:

`git init`

And we also need to tell our local Git where is the remote address of the GitHub server:
Where is where you use the address in the red box from the previous step which looks something like:
```
git remote add origin git@github.com:<your-username>/<your-repository-name>
```

Next import the theme you choose in the previous section, the address of the theme will need to be updated if you choose
a different one, make sure you have the GitHub address for the code of that theme and replace like hits:

_git submodule add https://github.com/<usename-of-the-author-of-the-theme>/<repository>.git themes/<theme-name>_

In this guide we  will be using Ananke theme so:

```
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
```

You may get a message asking if you want to continue connecting, type yes and press enter.

If you SSH was setup correct it will ask you for the passphrase if you set one, type it, and it will start downloading.

Next open the `config.toml` on the root of the folder and specify some parameters for this Hugo site, a toml is a text file, 
so you can use Notepad, VSCode or any other editor you prefer.

We are going to modify the title and then a new parameter called `theme` with the name of the theme we choose. 
Your file should look like this:

```
baseURL = "http://example.org/" # We will be chaging this later
languageCode = "en-us"
title = "My New Hugo Site" # Give a cool name to your website
theme = "ananke" # Or the theme you choose
```

Save the file when you are done.

Next, run your new site locally with the selected theme:

`hugo server --watch`

The command above should output something similar to this:

```
hugo server --watch
Start building sites …

                   | EN
-------------------+-----
  Pages            |  7
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  1
  Processed images |  0
  Aliases          |  0
  Sitemaps         |  1
  Cleaned          |  0

Built in 13 ms
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

You now can visit the following url on your browser and see your new site💥:

http://localhost:1313

### Making changes and adding content

If everything went well, you should see a very basic page with the title of the site.

In this section we will go on to explaining how to customize this site further and add more pages and posts.

Every Hugo theme has a set of basic features and other have more specific customization you can do, since we want you to 
be able to chose any other theme, we will guide through the most common features so that you can apply this knowledge in 
other themes and sites you build in the future.

First of all, we need to make a distinction between 2 concepts, in Hugo you have **Pages** and **Posts**, 
a Page is a static section in you site that doesn't change too often, maybe the about us, the history of your organization, 
or the contact page, and then you have posts which are articles that you write in a more frequent basis and are ordered by publish date.

Lets add our first page, it is going to be the About me. Create a new folder inside the `content`

directory named `about-me` and then create a file named `_index.md` inside.

Add the following content to it:

```
---
title: "About Me"
date: 2021-03-27
draft: false
---

Write something about you here
```

Next we will add a post, a post can be added by create a new file under `content/posts`.

Create a file named `my-first-post.md` under `content/posts` with the following content:

```
---
title: "My First Post"
date: 2021-03-27
draft: false
---

This is first post!
```

If you go back to your site in the browser you may see the post you created but not the about-us page. 
This is because we have enable the menu on the theme, to do this, edit the `config.toml` again and add the following parameter:

```
SectionPagesMenu = "main"
```

Save, and it should automatically reload and show About Me in the top right corner of the site.

So far you site should look something similar to this:

![hugo_aboutMe.png](/posts/personal-website-tutorial/hugo_aboutMe.png)

Hugo is very flexible and has many options you can use to customize your pages, remember that for formatting text you 
can use all the feature of [Markdown](https://commonmark.org/), you can also 
add [feature images](https://github.com/theNewDynamic/gohugo-theme-ananke#change-the-hero-background) or embed extra 
images to your post and pages.

If you want to add an image to your post or pages place the image inside the `static` folder and then use the following 
syntax in the page or post:

```
![Chocolate cake](/cake.jpg "A delicious chocolate cake")
```

Continue iterating on this step, by adding more posts, pages and the content you want for your site.

Once you are happy with this continue to the next section.

## To the Moon 🚀

So far we have been making modifications and viewing it locally, but you maybe thinking, how can my site go from being in
my computer to be publicly available on the internet?

There are a couple of steps you need to follow in order to archive this and we will be detailing those in the next sections

### Hosting the site on GitHub

As we mention at the beginning of the tutorial we will be using GitHub as hosting platform for our site, 
GitHub's main feature is hosting code but they also have a service called GitHub pages that allows you to do what you are imagining,
hosting your static site, and it the best part, it is 100% free, you do not need to deal with hosting providers, virtual servers, 
back-end configurations, etc.

If you want to know more about GitHub pages, watch this video:\
<<https://www.youtube.com/watch?v=2MsN8gpT6jY>>

### Push your code to GitHub

Now that it knows where is the "git server" we need to tell which code we want to push, this action is called "git commit", 
for this time, we will make a big commit with all these new code, but normally you do small pieces describing the things that were changed.

Open GitHub Desktop, login with your GitHub account:

![GitHub Desktop Login](/posts/personal-website-tutorial/71f46a72-c7bc-41ae-9f2c-28dc0bc96c91.png)

Then add the location of your repository in your computer:

![GitHub Desktop Login](/posts/personal-website-tutorial/lets-get-started.png)

and select the all the files and create a new commit, write a commit message and click the ***commit*** *button.*

Once that we have all the code committed, we just need to push to GitHub by clicking the push button:

This instruction is telling Git to push all committed code in the current branch to the branch `main` in `origin` if you look at the first command we set GitHub as the origin for our code repository, therefore this code will be uploaded to out GitHub repository.

![GitHub Desktop Commit](/posts/personal-website-tutorial/swappy-20210329_125243.png)

Amazing! you just created your first commit ever!

Now you code is on GitHub, and at this point you could invite a friend to start collaborating in this same code and 
he will be able to download and push changes, reviews or comments on those modifications and improve the site together.

### Configure GitHub Actions

So far we relied on running Hugo to build the site locally and we pushed the source code to GitHub, 
but this is not the final site, we need to tell Hugo to build or package the final files that are going to be "served" 
to the visitors of our site. For this we will be using GitHub Actions.

GitHub Actions are basically small programs that can do things for us. Do not worry we won't need to write our own program for this. 
Again, we will be relying on the power of the Open Source and we will be reusing something that someone else have done 
and put it out for other people to use.

In this section we will be configuring a GitHub Action that will build our site automatically each time we merge some code into the `main` branch.

First, in your computer add 2 new folders in the root of your project: 
`.github` (not the dot at the beginning) and inside another called `workflows` inside this folder create a file named `gh-pages.yml` 
and add the following content:

```
name: github pages

on:
  push:
    branches:
      - main  # Set a branch to deploy

jobs:
  deploy:
    runs-on: ubuntu-18.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          # extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

Commit this new file using GitHub Desktop and push it to GitHub.

Now if everything went well you should be able to navigate to the Actions section in your GitHub project and see it if 
it succeeds (look for a green check).

![swappy-20210328_112840.png](/posts/personal-website-tutorial/swappy-20210328_112840.png)

This now means that every time you make a change to your site and push that change to the `main` brach, GitHub will create
the latest version of your site automatically and save it into a branch called `gh-pages`

### Configure GitHub Pages

Ok, now we have a GitHub Action that pushes our final site to the `gh-pages` branch, how can we visit our site on the internet?
Here is where GitHub Pages enters.

We need to tell GitHub that our repository wants to make use of GitHub pages. To do this navigate to the repository settings 
and scroll to the bottom of the page to the GitHub Page settings. Here you will select the `gh-pages` branch and `/ (root)`,
click the Save button.

![swappy-20210328_113512.png](/posts/personal-website-tutorial/swappy-20210328_113512.png)

After saving the button the message in the green box will give the url for your new site.

Perfect! now you site is ready, and you should be able to visit it from anywhere in the world using an address 
like: **http://*username*.github.io/*repository***.

And there you go!, now you site can be automatically published every time that is a change, hands free! Isn't this amazing?

## Adding a custom domain

We are basically done with the guide for publishing a site for free on GitHub, but the cherry on top would be to have 
our own custom domain name pointing to our new site. This will give you a more professional look and with the time, 
your own domain will create *[authority](https://en.wikipedia.org/wiki/Domain_authority)* on the internet, 
see this as a type of reputation on the Internet.

### Getting a free or paid domain

There a couple of sites where you can get a free domain for 1 year, some of this domains have not very common TLD's 
like `*.tk` you can use it and get something like `you-username.tk`. But if you are using this site for something serious
like a personal website or business I would recommend something you like and would like to preserve for the years to 
come (remember that time you created that gigglybear4u@hotmail.com email years ago? 🤣 )

We recommend [Freenom](https://www.freenom.com/) for getting some domains free for 1 year, you can choose from 
`.tk`, `.ml` `.ga`, `.cf` and `.gp` chose any of those of if you prefer, you can select one of the non-free one, 
which cost around $15 a year.

![swappy-20210328_113914.png](/posts/personal-website-tutorial/swappy-20210328_113914.png)

Make sure you select 1 year free and take the time to configure the DNS for GitHub pages (`185.199.108.153`) :

![swappy-20210328_114015.png](/posts/personal-website-tutorial/swappy-20210328_114015.png)

### Configuring DNS

Once that you have your new shiny domain name we need to tell it what to do when a person types it in the browser bar.

DNS records are the instructions that tell servers where to look when someone or something queries them. 
For this case we created an `A` record which will point to GitHub's ip address and a `CNAME` record to forward requests
to `www.yourdomain.com` to the 'naked' domain `yourdomain.com`. Something worth mentioning is that DNS records need to
propagate across the servers in the world, depending on where you are, you domain may be available in few minutes or up to
24 hours.

Since we already created the DNS records on the previous step, so there nothing else to do on the Freenom site, but we 
still need to tell GitHub which domain we are using.

Firstly, we need to configure our site to use that domain, we need to do 2 things.

Create a CNAME file with the domain name inside the `static` folder. You can use this single line command to do it in one go. 
Remember that this command needs to be executed at the root of your project using PowerShell.

```
echo "<your-domain-name>" > static/CNAME
```

Next, edit again the `config.toml` and update the first line where the baseUrl is set, now it should be your domain name:
`baseUrl = "http://<your-domain-name>"`

Commit this change on GitHub Desktop and push them.

Finally we only need to go to the repository settings on GitHub and set the domain name to ours:

![swappy-20210328_120412.png](/posts/personal-website-tutorial/swappy-20210328_120412.png)

If desired (and recommended) after 24 hours of enabling this option, you could enable https for your domain by checking the
"Enforce HTTPS" option and updating again the baseUrl in the config.toml to be `https` instead of `http`.

## Conclusion

I hope you have enjoyed this tutorial and you are now a happy owner of a personal site on the World Wide Web. 
At this point in time of always connected and internet of things, having a simple website doesn't seems as important as it sounds
specially nowadays people uses public services like Facebook to host their business pages. 
Do not let this fool you, when using a Facebook page you are putting a requirement for your users on having a Facebook accounts.
You are also limited to Facebook feature and designs standard, and finally by having your own domain, you are the owner
of the content you publish.