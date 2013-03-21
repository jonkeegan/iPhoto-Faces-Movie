#iPhoto-Faces-Movie

Make a movie of all the faces in your iPhoto library

This script will grab all of the faces that iPhoto has found
in your photos for a given year and glob them all together into a movie. 
This grabs ALL faces, not just the ones you have named. So you may get 
strangers in the backgrounds, statues, news anchors on the TV in the 
background etc. It's a pretty intense way to review a year of your life in photos.

You can see a sample output here: http://youtube.com/watch?v=BAZT0EW99dI

## Requirements

This was built for iPhoto 11 running on Mountain Lion (OS X 10.8.3)
Requires ffmpeg for econding the movie. To install this painlessly: 
		1. Install homebrew -> http://mxcl.github.com/homebrew/
		2. Type "brew install ffmpeg"  

## Instructions
```sh
Pick a year that you want to create a movie for 
THE_YEAR=2013

# enter the full path to your 'iPhoto Library' file. You don't have to escape spaces...
# the default location is "~/Pictures/iPhoto Library"
# maybe you moved iPhoto to an external drive? ->"/Volumes/Seagate Backup Plus Drive/iPhoto Library"
PATH_TO_IPHOTO_LIBRARY="~/Pictures/iPhoto Library"

# the output directory "iPhotoFaces" will be created on the Desktop 
mkdir ~/Desktop/iPhotoFaces/
# create a folder for this year
mkdir ~/Desktop/iPhotoFaces/$THE_YEAR/
# copy all of the matching face thumbnails for this year to this year's directory
find "$PATH_TO_IPHOTO_LIBRARY"/Thumbnails/$THE_YEAR/ -name "IMG_*_face*.jpg" -exec cp {} ~/Desktop/iPhotoFaces/$THE_YEAR/ \;
# move to it
cd  ~/Desktop/iPhotoFaces/$THE_YEAR/
# suck all the thumbs into ffmpeg, at high quality (qscale) at 30fps (r) at 200x200 pixels (s) - find more options here: http://ffmpeg.org/ffmpeg.html
ffmpeg -f image2 -pattern_type glob -i '*.jpg' -qscale 2 -r 30 -s 200x200 $THE_YEAR.avi
# clean up the thumbs
rm *.jpg
```