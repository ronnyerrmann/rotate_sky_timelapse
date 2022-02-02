# rotate_sky_timelapse
How to rotate individual images taken as a timelapse so that the sky is stationary and earth is rotating below the sky

## Using the linux tools: `mogrify`
I used a spreadsheet for the task, created many years ago, when it seemed easier to do that than to write code. It was only tested for data from the northern hemisphere.

The user needs to modify the entries with the yellow background:

1. **B3**: give the syntax to find all frames that you want to include in the video
2. **C4-Cx**: give all individual frame names, e.g. after running `ls -l <B3>`
3. **D3-I3**: give the time for which the rotation angle will be 0, e.g. the middle of the time series
4. **B5-B6**: give the original image size
5. **B11**: factor by which the frames need to be scaled down
6. **B8-B9**: point around which the images should be rotated in the original pictures. It's measured from the *top left corner* of the image and will be the same in all frames. Due to lens distortion, the centre doesn't need to be know with pixel precision. The rotation centre can be outside of the original image, this might require some try and error to find it. Good luck :)
7. **B35**: Use 1 for rotation around the north pole and -1 for rotation around the south pole
8. **D4-Ix**: Make sure that each column contains the right information for Year, Month, Day, Hour, Minute, Second

Afterwards the commands from blue cells need to be executed:

0. **L1**: This can be used to create a script and run it. Any other editor can be used, if `vi` is used then **i** changes to insert mode to paste the fields listed below, **ESC** ends the insert mode, and **:x** saves the file and closes `vi`.
1. **K3**
2. **K4-Kx**
3. **L3**
4. **L4-Lx**

## Creating the time lapse video:
```
mencoder mf://*.jpg -mf fps=24:type=jpg -noskip -vf scale=1156:868 -of lavf -lavfopts format=mp4 -ovc x264 -sws 9 -x264encopts nocabac:level_idc=30:bframes=0:bitrate=16384:threads=auto:turbo=1:global_header:threads=auto:subq=5:frameref=6:partitions=all:trellis=1:chroma_me:me=umh -o video.mp4
```
* **fps=24** can be changed to a different frame rate
* **scale=1156:868** needs to be modified to the size of the final images
* **bitrate=16384** can be increased if the video quality is not good enough
* **video.mp4** give your own filename 

## Extra remarks:
Maybe at some point, I will convert it into a script.
