# send2ereader
A service for sending ebooks to a Kobo or Kindle ereader through the built-in browser.

This repo is what I'm using on my self-hosted version (link to follow).

## Instructions to set up a copy for yourself:
### assumptions for these instructions
  - you're using linux.
  - you have a basic idea of how to work a CLI.
  - you're running all of these commands as root (i'll mark the ones that don't have to be root).
  - you're going to ignore my inevitable typos; I'm writing this directly into github's "create a README" page.
  - You're running this in a VM or on a regular machine - if you want to do it in a container, take a look at some of the other forks.

### prereqs
1. Install node.js and npm (node package manager). Actual method will vary based on your distro, but as it's pretty widely used, it shouldn't be hard to find instructions.
2.  Install node package prereqs with `npm install [package name]`. There's a list of these a the start of the `index.js` file; I'll reproduce it below for you. 
    - koa
    - mkdirp
    - fs
    - child_process
    - path
    - file-type
3. You're also going to need to install `kepubify` if you want to be able to convert EPUBs to KEPUBS. Do this by running `curl -LJO https://github.com/pgaskin/kepubify/releases/download/v4.0.4/kepubify-linux-64bit \
  && mv kepubify-linux-64bit /usr/bin/kepubify \
  && chmod +x /usr/bin/kepubify` 
    - You can leave this out if you want, but if you do, I would recommend editing `upload.html` to remove all references to kepubify: if you don't have it installed and working and someone tries to send an EPUB to be converted, send2ereader is going to crash. I wouldn't remove the section on it in `index.js` in case you decide to add it later. 
4. ideally, we would then install KindleGen to do EPUB -> MOBI conversions. Unfortunately, Amazon has discontinued KindleGen, so we'll leave it out for now. Thus, I've removed all mention of it on my `upload.html`. (If I *do* figure out how to get EPUB -> MOBI conversions working/how to install KindleGen, I'll update here).

### running it!
1. cd to the directory where you've got your `index.js` and everything else.
2. run `node index.js` to start send2ereader. If all went well, you'll get `server is listening on port 3001`. (you can change the actual port in `index.js`. In fact, I'd recommend poking around in it to make sure that everything's as you want it - including the all-important `style.css`.)
3. open your browser, navigate to your IP:3001 to make sure everything's working. If all *didn't* go well, you'll want to read the errors you got, google them, and then fix them.
4. If you want your send2ereader instance to be available outside your local network, you'll want to set up port forwarding and (probably) a domain name. Explaining how to do those things varies based on router and how you decide to go about getting a domain name, so a more detailed explanation is out of scope. you'll also probably want to make sure that you've got a decent security setup, but if you're selfhosting things I assume you've got a good idea of what that should entail.
5. enjoy! :)
