## Quick blogging guide.
This is a cliff notes version of this page: http://octopress.org/docs/blogging/
create new post: rake new_post['title']
vim that file.
rake generate watch
Then preview it at http://johnmorales.dev/


## commit your code
git commit -m 'your message'
git push origin source

## After which to deploy simply
rake deploy

## Quick md tips
links [text](url)
images
  {% img center /images/someimage.png }
