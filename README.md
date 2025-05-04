# StarTracker

## 📖 Overview

Finds correspondences between stars in two images of the same sky region even if they’re shifted or rotated—by:

1. Enumerating every triple of stars in each image and computing the three internal angles of each triangle.
2. Matching triangles whose angles differ by at most a user-defined threshold.
3. Voting on individual stars based on how often they appear in matched triangles.

Why triangles? Any three non-collinear points define a triangle whose internal angles remain the same under rotation or translation of the entire image.

Thresholding: For each triangle in image 1, compare against every triangle in image 2.

Criterion: All three corresponding angles must differ by ≤ angle_thresh.

Result: A list of matched triangle pairs matched_tris.

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
Then annotate the images via:
```bash
visualize_and_save_stars
```

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
```bash
python match_stars.py
```

The script writes matched_stars.csv and displays both images with matched star pairs highlighted.

