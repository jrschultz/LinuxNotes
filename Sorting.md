# 📋 Sorting in Linux

## 🧺 Sort

### Sort Data into Groups

```bash
sort sample.txt
```

## 🐇 Uniq

### Show only unique entries

```bash
uniq sample.txt - shows only unique entries
```

### Show only duplicate entries
```bash
uniq -d sample.txt - shows only duplicate entries
```

## Pipeflow

```bash
sort -d textile.txt | uniq > updatedlist.txt
```