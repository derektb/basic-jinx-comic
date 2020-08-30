# Jinx Comic Template

This is a basic template for making a Jinx comic, based on best practices I've developed (and continue to develop) from making Jinx comics.

### See Also
* [Jinx](https://github.com/derektb/jinx), a framework for building interactive comics in Twine.  Documentation can be found there.
* [Wizard Town](http://www.wizard.town), the place where I post comics I have made with Jinx.

## Building Comics

The comic's data are packaged from `/src` into a single `/dist/index.html` file by [Tweego](https://www.motoslave.net/tweego/), a command-line utility for building Twine stories from files.

The build commands are:

```
npm run build-comic     # Builds dist/index.html with local packaged tweego
npm run build-art       # Copies valid files from /art to /dist/art
npm run build           # Runs the above two commands
npm run build-watch     # Runs build, then watches /src and /art for changes
```

_(Tweego is included with this repo with the latest production version of Jinx, so you don't need to do any other setup on your machine.  If you'd like to use your own install of Tweego, just change the local call to Tweego in `build-comic` to a global one.)_

The comic will fail to build the first time; this is by design.  Twine stories are required to have a StoryData passage with a unique IFID.  When Tweego doesn't find one in `panels.tw`, it will suggest one in the command line, like this:

```
:: StoryData
{
  "ifid": "A-UNIQUE-STRING-OF-NUMBERS-AND-LETTERS"
}
```

Paste it into `panels.tw`, or wherever you're keeping your required StoryTitle and StoryDescription passages.

### Tweego Issues

Sometimes I encounter issues with this Tweego setup the first time I use the repo, largely because of permissions issues in running local Tweego not in its own directory.  If this happens, try:

```
chmod +x ./tweego/tweego
```

MacOS will likely block the script as from an unverified developer, so you'll need to go allow it in Security.  Things should be good to go after that.

## File Structure

This template uses the following file structure:

```
/art
  /1
    /AXp1
      art.png
/src
  /scripts
    _setup.js    # Contains Jinx setup calls
  /styles
    main.css
  panels.tw      # Contains a basic Jinx panel definition
/dist
  # Builds go in here.
```

### Art

Use `/art` for storing all the art you want to be exported to `/dist/art`.  This folder contains the sample page-panel file structure I commonly use.

Upon running `build-art`, only valid files in `/art` will be copied into `/dist/art`, with the exact same file structure.  This means you can store your non-production art files (such as PSDs) _in situ_ alongside your production assets.

The basic valid filetypes are JPEGs, PNGs, and GIFs; if you have other filetypes you want to be considered valid in your comic, add them to the `build-art` command.

Keep in mind that `/dist` is not cleaned of previous builds, so if you're renaming or restructuring your art assets, they'll still be in there if you don't clean house every once in a while.

### Src

Tweego will build `/dist/index.html` from everything in the `/src` directory.

One thing to keep in mind: Tweego compiles scripts and styles from files in alphabetical order.  Twine will run all user scripts compiled in this way at runtime, in order.  This is why `_setup.js` is prefixed with an underscore; to make sure it gets run first.  You may want to set up naming or numbering conventions if you have files you need compiled in a specific order.
