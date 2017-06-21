Misc notes on using this:

You need to have EXIFtools installed for this to work (the windows and mac install files are in the exiftools folder or visit http://www.sno.phy.queensu.ca/~phil/exiftool/ to download the latest version). 

Here's the link to the Github repository for scripts that we use for the Video Portal (https://github.com/USGS-VideoPortal/USGS-VideoPortal).  You'll want to grab the UpdatePhotoEXIFv2.py script.  As I'm looking at the Github site now, I think we'll need to move these around into individual folders but for now all the scripts are lumped into this repository.  This version is slightly cleaned up.  But VeeAnn and I will be working over the next couple months to further clean it up and fix some of the bug/limitations with running it (for example, if you have photos with GPS EXIF info already in the headers, and you don't want to overwrite those, there's a little work around that I do, but we'd like to set an option in the GUI to skip updating certain headers if its not necessary).

The UpdatePhotoEXIFv2.py script is essentially calling on ExifTools to do the EXIF updating incrementally on several variables that are defined either in the GUI, in the params file, and the csv file containing the GPS data.

 I have encountered photos that we have Lat/Long and date but no time (camera time in the header was obviously off so we didn't want to use that).  In this case I made the time fields 99:99:99 so it is clear that the time is unknown. 

Here is a link to a metadata file that is for both the locations shapefile and the images. We're trying to bundle more...
From this link you can also get the XML or the TEXT if you want to grab sections:
http://woodshole.er.usgs.gov/field-activity-data/2015-001-FA/data/photos/2015_001_FA_photos.html

Here's one for metadata that is only for the photos as a standalone dataset:
http://pubs.usgs.gov/of/2014/1221/GIS/hyperlink_images/BBVS_SEABOSS_Photos_Metadata.html

And here's some code to extract the exisiting EXIF info from a folder full of photos (see EXIFtool website for other tag names to extract). [run from the folder that has all the photos in it.  Output is piped to a file called out.csv]:

$> exiftool -csv -f -filename -GPSTimeStamp -GPSDateStamp -GPSLongitude -GPSLatitude -n -Artist -Credit -comment -keywords -Caption -Copyright -CopyrightNotice -Caption-Abstract -ImageDescription *.jpg > out.csv
