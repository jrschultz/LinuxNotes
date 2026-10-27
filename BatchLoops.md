# 💫 Loops for Batch Jobs

## To convert a bunch of image files: 

```bash
for i in *.jpg; do convert "$i" "${i%.*}.webp"; done
```

## To convert a bunch of audio files: 

```bash
for i in *.ogg; do ffmpeg -i "$i" "${i%.*}.m4a"; done
```

## To convert and delete the original: 

```bash
for i in *.ogg; do ffmpeg -i "$i" "${i%.*}.m4a"; done
```
