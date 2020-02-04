# Oat's Quotes 

This is my personal website, for me Oat (a.k.a Pat Mulloy)
This README is mostly for my personal use, as documentation on how to use the site generator Hexo, and deploy the site to Github Pages. 

## Hexo

#### Generating a new post 
`hexo new post <title>` for a new post, this will end up on the main page.
`hexo new page <title>` for a new page.


#### Updating iOS tidbits 
For now, updating iOS Tidbits will just be updating source/Tidbits/inex.md. Eventually I need to add support so each tidbit is its own page. 


## Github (and Github Pages)
This repo is different than the repo for the actual site. The actual site is at https://github.com/OatsQuotes/OatsQuotes.github.io.


#### Pushing code 
To deploy to the Oats Quotes repo, call *hexo generate* then *hexo deploy*. This will deploy the site code to that repo. 
Be sure to push code to this repo as well, to keep everything updated. 


#### Updating CNAME 
Add a CNAME file to the repo, with oatsquotes.com as its content.
This routes the gh pages site to the actual GoDaddy domain. 
