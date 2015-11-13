Decktape Docker
===============

A Docker image with Decktape for creating PDFs from browser-based
presentations. 

Usage:

    $ docker run amouat/decktape

    Usage: phantomjs decktape.js [options] [command] <url> <filename>

    command      one of: automatic, csss, deck, dzslides, flowtime, generic, impress, remark, reveal, shower, slidy
    url          URL of the slides deck
    filename     Filename of the output PDF file

    Options:
       -s, --size                Size of the slides deck viewport: <width>x<height>  [1280x720]
       -p, --pause               Duration in milliseconds before each slide is exported  [1000]
       --screenshots             Capture each slide as an image  [false]
       --screenshots-directory   Screenshots output directory  [screenshots]
       --screenshots-size        Screenshots resolution, can be repeated
       --screenshots-format      Screenshots image format, one of [jpg, png]  [png]

    Defaults to the automatic command.
    Iterates over the available plugins, picks the compatible one for presentation at the
    specified <url> and uses it to export and write the PDF into the specified <filename>.

You will probably want to mount a volume to save the resultant PDF out to. For
example:

    $ docker run --rm -v $(pwd):/slides amouat/decktape reveal http://192.168.99.100:8000/ /slides/pres.pdf
    Loading page http://192.168.99.100:8000/ ...
    Loading page finished with status: success
    Reveal JS DeckTape plugin activated
    Printing slide #/9      (34/34) ...
    Printed 34 slides

This will save the RevealJS presentation running at http://192.168.99.100:8000/ to pres.pdf in
the current directory.

Alternatively, you can also use docker cp:
 
    $ docker run amouat/decktape reveal http://192.168.99.100:8000/ /pres.pdf
    ...
    $ docker cp $(docker ps -lq):/pres.pdf ./
    $ docker rm $(docker ps -lq)
    ...
    


