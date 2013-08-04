imgDiffUploadr
==============

Each successive different image will be uploaded to a Flickr account.

Setup
=====

On Lubuntu 12.04 ...

Install libpuzzle
-----------------

Libpuzzle hadn't been updated in some time ... perhaps because of this, the configure/ make files didn't work out of the box.  Here's a (brief) summary of what finally worked (after some poking around/ experimentation):

Install libgd2

    sudo apt-get install libgd2-xpm-dev

Clone libpuzzle library on github: 

    git clone http://github.com/jedisct1/libpuzzle.git

Then came the hackery ... 
 * run autoconf
 * run autoheader
 * run ./configure
 * Rename (or copy) lots Makefile.am to Makefile.in in most of the subdirectories.
 * Finally, ./configure finished without error.
 * Try make, or make puzzle-diff.  Didn't work for me.
 * Added #include \<math.h\>; and #include \<gd.h\> lines in dvec.c.
 * Copied config.h to src/.
 
Rather than try to debug the Makefiles, I ended up compiling puzzle-diff directly using: 
    
    cc puzzle-diff.c puzzle.c cvec.c dvec.c tunables.c vector_ops.c -lm -lgd -o puzzle-diff

Install streamer
----------------

Simply: 

    sudo apt-get install streamer

Install libflickr
-----------------

Simply:

    sudo apt-get install libflickr-upload-perl
    

Now set up auth token for Flickr authentication.  Run:

    flickr_upload --auth

Then: 
 * Paste the URL into a web browser and follow the instructions that appear.  
 * Paste the authentication token into ~/.flickrrc/token.
 * Then run: bash checkFlickrToken.bsh
 * If you see XML indicating that you have write permission, it's done!





