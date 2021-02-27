# php-ffmpeg-wrapper
php-ffmpeg-wrapper class for audio/video

Requirements

    ffmpeg 2.8.x or later for all scripts except those listed in 2.

php-ffmpeg-wrapper is a class implementation of the popular ffmpeg audio/video command-line editing tool.

update ffmpeg-config.php file for path to ffmpeg executable  and enable/disable debug messages. 

Examples:  
  
Create a 10 second 1280x720 video.  

```php
<?php  
include("ffmpeg-wrapper.php");
$ffmpeg = ffmpeg_presets::empty_movie("1280x720",10);  
$ffmpeg->set_output("empty.mp4");                         # this should create a file empty.mp4 on the server
$ffmpeg->run();  

echo $ffmpeg->response() . PHP_EOL;                       # this shows debugging information
?>
```
  
Trim, scale and encode to a new format.

```php
<?php
include("ffmpeg-presets.php");
$ffmpeg = new ffmpeg_wrapper("/usr/local/bin/ffmpeg");    # update the path to binary if required

$ffmpeg->add_input("video_file.mp4");                     # input
$ffmpeg->set_output("output.mp4");                        # output

$ffmpeg->trim_range(1.2,3.3);                             # trim
$ffmpeg->video_filter->scale(640,480);                    # scale

$ffmpeg->audio->encoding("libfaac");                      # audio/video codec to be used 'aac' is by default always available
$ffmpeg->audio->bitrate("192k");
$ffmpeg->video->encoding("libx264");
$ffmpeg->video->group_of_picture(30);
$ffmpeg->video->qscale(0);

echo $ffmpeg->run() . PHP_EOL;                            # execute and show debuging data
?>
```
