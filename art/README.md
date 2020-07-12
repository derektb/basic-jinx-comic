Use `/art` for storing all the art you want to be exported to `/dist/art`.  This folder contains the sample page-panel file structure I commonly use.

Upon running `build-art`, only valid files in `/art` will be copied into `/dist/art`, with the exact same file structure.  This means you can store your non-production art files (such as PSDs) _in situ_ alongside your production assets.

The basic valid filetypes are JPEGs, PNGs, and GIFs; if you have other filetypes you want to be considered valid in your comic, add them to the `build-art` command.

Keep in mind that `/dist` is not cleaned of previous builds, so if you're renaming or restructuring your art assets, they'll still be in there if you don't clean house every once in a while.
