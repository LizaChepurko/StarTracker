# Star Tracker

## 📖 Overview

Our algorithm finds congruents between stars in two images of the same sky region even if they’re shifted or rotated by:

1. Enumerating every triple of stars in each image and computing the three internal angles of each triangle.
2. Matching triangles whose angles differ by at most a user defined threshold.
3. Voting on individual stars based on how often they appear in matched triangles.

Why triangles- Any three non-collinear points define a triangle whose internal angles remain the same under rotation or translation of the entire image.

Thresholding: For each triangle in image 1, compare against every triangle in image 2.

All three angles of the congruent triangles must differ by ≤ angle_thresh.

**Result**: A list of matched triangle pairs matched_tris.

Voting on Stars:

```bash
ctr1 = Counter()
ctr2 = Counter()
for tri1, tri2 in matched_tris:
    ctr1.update(tri1)
    ctr2.update(tri2)
```

we sort stars in each image by descending vote count and pair the top‐ranked star in image 1 with the top‐ranked star in image 2, the second with the second, and so on.
This “greedy” assignment assumes the highest‐confidence stars correspond to one another.


## Usage
Start with the creating of csv file:
```bash
detect_stars_cv2
```
Or for HEIC files run:
```bash
detect_stars_heic
```
The output is a csv file with x,y,r (radius),b (brightness) parameters

Then annotate the images via:
```bash
visualize_and_save_stars
```

The output is annotated images.


Edit the paths and parameters in match_stars.py:
```bash
star_csv1      = "/path/to/IMG_3053.csv"
star_csv2      = "/path/to/IMG_3055.csv"
image1_jpg     = "/path/to/IMG_3053_annotated.jpg"
image2_jpg     = "/path/to/IMG_3055_annotated.jpg"
angle_thresh   = 0.5    # maximum allowed angle difference (degrees)
output_match_csv = "matched_stars.csv"
```
Run:
The last code block

The script writes matched_stars.csv and displays both images with matched star pairs highlighted.

[Code](https://github.com/LizaChepurko/StarTracker/blob/main/find_match.ipynb)

## Annotation

![ST_db1_annotated](https://github.com/user-attachments/assets/ced8995d-326f-4892-8388-62b7245cd9d2)<img width="972" alt="ST_db1" src="https://github.com/user-attachments/assets/c9f72881-7ed1-4d06-8e3b-4cbf4d9581e8" />


## Results
You can see the identified stars and images in [results](https://github.com/LizaChepurko/StarTracker/tree/main/results)

![matched_stars_fr1_fr2](https://github.com/user-attachments/assets/35b70ac2-5ae3-4d37-bbf4-5c9adbb27f52)



