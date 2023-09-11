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

ffmpeg -i 'test.jpeg' -filter:v "hflip" -c:a copy output.jpeg
