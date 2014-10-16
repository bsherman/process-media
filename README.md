process-media
=============

## Overview ##

This collection of scripts was created to facilitate the migration 
of photos and videos out of iPhoto into a generic folder hierarchy
accessible by any number of photo/video tools, or no tool at all.

## process-sync-media ##
This is my python front end to the execellent *exiftool* 
( http://www.sno.phy.queensu.ca/~phil/exiftool/ ). It helps sort a 
pile of photo and video files into appropriate locations.

usage: ./process-sync-media /source [--inplace-rename]|[/target/photo /target/video]

It requires you to specify a single media source.

Optionanlly, you can do a rename in place... OR
specify both a target photo and video directory, and it will sort videos and photos 
in to those distinct locations.

I use this from cron to auto-sort vids/pics from my iPhone, which have been
sync'd over via CameraSync ( http://homegrownsw.com/camerasync/ )

    MAILTO=none
    PATH=/usr/local/bin:/bin:/usr/bin
    30 3 * * * date >> /tmp/psm-CameraSync.log && process-sync-media /home/me/Dropbox/CameraSync /files/Photos /files/Videos >> /tmp/psm-CameraSync.log 2>&1


My default video structure looks like:

    # a year directory
    /Videos/2014
    # month directories
    /Videos/2014/2014-04
    /Videos/2014/2014-05
    # and then the file in the month directories
    # the filename is full date, plus time, plus the original filename
    /Videos/2014/2014-05/20140503_1441 - IMG_5432.mov 
    
    
My default photo structure looks like:

    # a year directory
    /Photos/2014
    # month directories
    /Photos/2014/2014-04
    /Photos/2014/2014-05
    # day directories
    /Photos/2014/2014-05-01
    /Photos/2014/2014-05-03
    # and finally the file in the day directories
    # the filename is full date, plus time, plus the original filename
    /Photos/2014/2014-05-03/20140503_144101 - IMG_1234.jpg 

Differences between photos and videos are the photos have an extra 
"day" directory level and the time in the filename includes seconds. 
In both cases, this is because, in general, there are a lot more photos
being taken all the time. This helps keep them organized and avoid overlaps 
and weird sorting issues.
