# send2ereader
A service for sending ebooks to a Kobo or Kindle ereader through the built-in browser.

This repo is what I'm using on my self-hosted version (link to follow).

## Instructions to set up a copy for yourself:
### assumptions for these instructions
  - you're using linux.
  - you have a basic idea of how to work a CLI
  - you're running all of these commands as root (i'll mark the ones that don't have to be root).
  - you're going to ignore my inevitable typos; I'm writing this directly into github's "create a README" page.

### prereqs
1. Install node.js and npm (node package manager). Actual method will vary based on your distro, but as it's pretty widely used, it shouldn't be hard to find instructions.
2.  Install node package prereqs with `npm install [package name]`. There's a list of these a the start of the `index.js` file; I'll reproduce it below for you. 
    - koa
    - mkdirp
    - fs
    - child_process
    - path
    - file-type
3. You're also going to need to install `kepubify` if you want to be able to convert EPUBs to KEPUBS. You can leave this out if you want, but if you do, I would recommend editing `upload.html` to remove all references to kepubify: if you don't have it installed and working and someone tries to send an EPUB to be converted, send2ereader is going to crash. I wouldn't remove the section on it in `index.js` in case you decide to add it later.
      - **installing kepubify**:
     - the easiest way is to clone the gh-pages branch of the kepubify repo, and use that for your npm package. I'm sure there's a more elegant way, but it's not what I used.
      - the actual commands you'll use to do this are `git clone --single-branch --branch gh-pages https://github.com/pgaskin/kepubify.git` (doesn't need root) and then `npm install ./kepubify`
4. ideally, we would then install KindleGen to do EPUB -> MOBI conversions. Unfortunately, Amazon has discontinued KindleGen, so we'll leave it out for now. Thus, I've removed all mention of it on my `upload.html`. (If I *do* figure out how to get EPUB -> MOBI conversions working/how to install KindleGen, I'll update here).
5. cd to the directory where you've got your `index.js` and everything else.
6. run `node index.js` to start send2ereader. If all went well, you'll get `server is listening on port 3001`.
7. open your browser, navigate to your IP:3001 to make sure everything's working. If all *didn't* go well, you'll want to read the errors you got, google them, and then fix them.
9. If you want your send2ereader instance to be available outside your local network, you'll want to set up port forwarding and (probably) a domain name. Explaining how to do those things varies based on router and how you decide to go about getting a domain name, so a more detailed explanation is out of scope. you'll also probably want to make sure that you've got a decent security setup, but if you're selfhosting things I assume you've got a good idea of what that should entail.
10. enjoy! :)
