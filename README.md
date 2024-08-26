# Podcast Feed Generator
A GitHub Action to generate a podcast feed from a YAML file. YAML is much easier to read and write that XML, and this action will convert your YAML file into a valid podcast feed.

You can use this project to update a podcast feed located within this repository in the **./output/podcast.xml** file or update other podcast feeds in other repositories. When you use another repo to run the project, it will find the _action.yml_ file, understand that it needs to use the Docker image, run the _Dockerfile_ to generate the server then run the _entrypoint_, which will set up git, run _feed.py_ and push the code to the server and in so doing generate your feed.

You can find a sample podcast at the homepage or **index.html** and a sample _XML formatted_ podcast feed by navigating to [https://Kmtengo.github.io/podcast-feed-generator/output/podcast.xml](https://Kmtengo.github.io/podcast-feed-generator/output/podcast.xml)

# Usage
## Turn on GitHub Pages
In your repository got to **Settings** > **Pages** and select the **main** branch as the source.This will create a link to your page and give all of the content in the main branch a URL. Note the URL for the next step.

## Create a YAML file
Create a YAML file in your repository with the following format:

```title: <Podcast Title>
subtitle: <Podcast Subtitle>
author: <Author Name>
description: <Podcast Description>
image: <Artwork location>
language: <Podcast Language i.e. en-us>
category: <Podcast Category i.e.Technology>
format: <Format of files i.e. audio/mpeg>
link: <GitHub Pages URL>
item:
  - title: <Podcast Episode Title>
    description: <Podcast Episode Description>
    published: <Date Published i.e. Thu, 12 Jan 2023 18:00:00 GMT>
    file: <Filename i.e. /audio/TFIT01.mp3>
    duration: <Podcast Duration i.e. 00:00:36>
    length: <Podcast Length i.e. 576,324>
... Repeat for each episode
```
## Sample Workflow
You are also going to need your own workflow file, here's a sample:
```name: Generate Feed
on: [Push]
jobs:
  generate-feed:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repo
        uses: actions/checkout@v3
      - name: Run Feed Generator
        uses: username/name-of-repository@branch
```

> [!NOTE]
> Alternatively, you can clone this repo and **edit** the _YAML file_ with your podcast information as well as the _uses poperty of the main.yml file_ with your repo details.
