---
jupytext:
  cell_metadata_filter: -all
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.14.5
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

# JupyterBook vs READMEs vs Wikis

Initially this book's contents exist in my Zettelkasten vault in Zettlr and I'd place the "_vault_" folder in the cloud so as long as I have access to internet, I can sync the contents and access it from PC, Mac, or mobile while out an about.

And then, I decided to do [#100DaysofMLCode](https://twitter.com/search?q=from%3Aellacharm3d%20(%23100DaysOfMLCode%20OR%20%23MachineLearning)&src=typed_query&f=live) and realized markdown files with fenced code snippets cannot be run like in vscode. Well, DUH!

And so the journey began to research a different way of doing things, and I came across jupyter-book. 
What's funny was, while going down the rabbithole of this research, someone on Telegram also gave me a suggestion on how I can better document my **100 Days project** as I was lamenting to that study group that as I'm not a verified Twitter account, I'm restricted to short-form tweets and some content really needs to be in the form of a blog post.

## About READMEs

[source](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes)

    You can add a README file to a repository to communicate important information about your project. A README, along with a repository license, citation file, contribution guidelines, and a code of conduct, communicates expectations for your project and helps you manage contributions.

    For more information about providing guidelines for your project, see "Adding a code of conduct to your project" and "Setting up your project for healthy contributions."

    A README is often the first item a visitor will see when visiting your repository. README files typically include information on:

    * What the project does
    * Why the project is useful
    * How users can get started with the project
    * Where users can get help with your project
    * Who maintains and contributes to the project

## About Wikis

[source](https://docs.github.com/en/communities/documenting-your-project-with-wikis/about-wikis)

    Search engines will not index the contents of wikis. To have your content indexed by search engines, you can use GitHub Pages in a public repository.


## Ways of linking in jupyterbook

jupyterbook's 
* [references content page](https://jupyterbook.org/en/stable/content/references.html)
* [references tutorial page](https://jupyterbook.org/en/stable/tutorials/references.html)
