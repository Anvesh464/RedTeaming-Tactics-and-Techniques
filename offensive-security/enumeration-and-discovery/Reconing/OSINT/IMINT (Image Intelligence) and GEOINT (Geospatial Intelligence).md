**IMINT (Image Intelligence) and GEOINT (Geospatial Intelligence)**

Last modified: 2024-02-13

IMINT and GEOINT are types of OSINT to reveal desired information from analyzing images.

[**Basic Investigation**](https://exploit-notes.hdks.org/exploit/reconnaissance/osint/imint-and-geoint/#basic-investigation)

open example.jpg

exiftool example.jpg

**Copied!**

[**Gather Information From Search Engine**](https://exploit-notes.hdks.org/exploit/reconnaissance/osint/imint-and-geoint/#gather-information-from-search-engine)

Search the keyword which is found in the image.

-   Name
-   Location (country, city, etc.)
-   When does it open

[**Reverse Image Search**](https://exploit-notes.hdks.org/exploit/reconnaissance/osint/imint-and-geoint/#reverse-image-search)

Upload the image in each search engine.

-   [**Bing Images**](https://www.bing.com/?scope=images)
-   [**Google Images**](https://www.google.com/imghp)

Click the “Search by image” icon and upload the image.

-   [**Yandex Images**](http://yandex.com/images)

[**Video (mp4) Geolocation**](https://exploit-notes.hdks.org/exploit/reconnaissance/osint/imint-and-geoint/#video-(mp4)-geolocation)

FFmpeg extracts every single frame from a video.

*\# -i: input file*

*\# %06d: followed by six digits e.g. img_000001.png, img_000002.png, etc.*

*\# -hide_banner: hide unnecessary text.*

*\# -r: frame rate (e.g. 1 frame per second)*

ffmpeg -i example.mp4 -r 1 img_%06d.png -hide_banner
