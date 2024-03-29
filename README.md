# ffmpeg-cheatsheet

## Trim a Video
This command creates a 30-second clip starting at 01:00 minute.
> `ffmpeg -i input.mp4 -ss 00:01:00 -t 30 -c:v copy output.mp4`

## Split a Video
This command splits a video vertically (top/bottom)
> `ffmpeg -i input.mp4 -filter_complex "[0]crop=iw:ih/2:0:0[top];[0]crop=iw:ih/2:0:oh[bottom]" -map "[top]" top.mp4 -map "[bottom]" bottom.mp4`

This command splits a video horizontally (left/right)
> `ffmpeg -i input -filter_complex "[0]crop=iw/2:ih:0:0[left];[0]crop=iw/2:ih:ow:0[right]" -map "[left]" left.mp4 -map "[right]" right.mp4`

## Generate a GIF
This command creates a 10-second GIF clip starting at 01:00 minute (with a lower file size).
> `ffmpeg -i input.mp4 -ss 00:01:00 -t 10 -filter_complex "[0:v] fps=8,scale=480:-1:flags=lanczos,split [a][b];[a] palettegen=max_colors=128 [p];[b][p] paletteuse" -pix_fmt pal8 -loop 0 output.gif`

## Flip Image Horizontally/Vertically
This command 
> `ffmpeg -i 'test.jpeg' -filter:v "hflip" -c:a copy output.jpeg`

## Extract video frame by frame
This command 
> `ffmpeg -i input.mp4 -vf "select=1" -vsync vfr output_%04d.png`

## Deinterlacing a video
This command 
> `ffmpeg -i input.mp4 -c:v utvideo -vf "yadif=1" -pix_fmt yuv420p -c:a copy output-des.mp4`

## Generate a video from image frames
This command 
> `ffmpeg -framerate 25 -i output/%04d.png -c:v libx264 output.mp4`

## Aspect Ratio
This command 
> `ffmpeg -i 'input.mkv' -c copy -aspect 4:3 'output.mp4`

## To 480p
> `ffmpeg -i input.mp4 -s hd480 -c:v libx264 -crf 23 -c:a aac -strict -2 output.mp4`

## Without audio
> `ffmpeg -i $input_file -c copy -an $output_file`
