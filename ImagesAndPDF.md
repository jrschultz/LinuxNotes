# 🖌️ PDFs and Images

## 📄 Working with PDFs

Using ```pdftk``` package

### Merge or Combine

```bash
pdftk PDF1.pdf PDF2.pdf cat output PDF3.pdf
```

 
### Rotate

```bash
pdftk input.pdf cat 1-endeast output output.pdf
pdftk input.pdf cat 1-endwest output output.pdf
```

### PDF to Images

```bash
pdftoppm -png -rx 300 -ry 300 updatedvalues.pdf document
```

### Images to PDF

```bash
img2pdf *.png --output ShopInsurance.pdf
```

The Default Resolution is 150

```bash
for p in *.pdf; do pdftoppm "$p" "$p" -png; done
```

This is for 300

```bash
or p in *.pdf; do pdftoppm "$p" "$p" -png -rx 300 -ry 300;
```

---

## 🖼️ Working with Images

using imagemagick

### Scale by Pecentage

```bash
mogrify -path resized/ -resize 50% *.jpg
```

### Resize to spec, maintain aspect ratio

```bash
mogrify -path resized/ -resize 1920x1080\> *.jpg
```

### Strip Metadata to Save Even More Space

```bash
mogrify -path resized/ -resize 1920x -strip -quality 75% *.jpg
```