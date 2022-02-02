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
6. **B8-B9**: point around which the images should be rotated. It's measured from ???
7. **B35**: Use 1 for rotation around the north pole and -1 for rotation around the south pole
8. **D4-Ix**: Make sure that each column contains the right information for Year, Month, Day, Hour, Minute, Second

Afterwards the commands from blue cells need to be executed:
0. **L1**: use the commands to create a script and run it
1. **K3**
2. **L3**
3. **K4-Kx**
4. **L4-Lx**

