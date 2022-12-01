

### parsing paths

Use **ls** to retrieve folder names only, and then remove the trailing / character with **tr**

```
ls -d */ | tr -d / > file.txt
```