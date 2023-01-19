# Remaining Lifespan Prediction 

[Download the dataset from Dropbox](https://www.dropbox.com/s/qn4y16p52a2gn2w/remaining-lifespan-data.zip?dl=0) (size: 1.03 gb)


The data has been collected from Wikidata/Wikipedia of:
- persons
- with a unique birth year specified
- with a unique death year specified
- who died between 1990 and 2022 (inclusive)
- whose manner of death is "natural causes" or not specified
- whose cause of death is a natural cause (disease, old age, etc.) or not specified
- who have an image associated
- whose associated image has a point-in-time property or a caption that includes a single number with the 19** or 20** format

The label for each image is the length of time (in years) between when the image was taken and when the person died (Remaining Lifespan or RL).

The dataset includes 24167 faces cropped from the images.

The file "info.pkl" includes a pandas dataset of the images, labels, and other relevant info so you can filter them based on your needs. 

To open the info file:
```python
import pandas as pd #version 1.5.2
df_rl = pd.read_pickle("path/to/info.pkl")
```

Here's a description of the variable names in the info file:
- person: wikidata entry url
- article: wikipedia article url
- birth_year: year of birth
- death_year: year of death
- img_year: the year the image was taken
- **img_name**: name of the image file (cropped and aligned face)
- img_src: the url from which the original image was downloaded
- death_manner: the general reason of death. Has two possible values, empty or Natural Causes (https://www.wikidata.org/wiki/Q3739104)
- n_death_causes: number of causes of death listed for the person on their Wikidata entry. 
- death_causes: the specific reason(s) of death. If multiple reasons, they are separated by _#_
- **remaining_lifespan**: (the label) how many years the person lived after the image was taken (death_year - img_year)
- age_at_death: how old the person was when he/she died (death_year - birth_year)
- age_at_img: how old the person was when the image was taken (img_year - birth_year)
- confidence: how confidence the MTCNN algorithm is about whether it detected a human face in the original image
- is_grayscale: is the original image grayscale (has only one channel or the three channels are similar)
- face_box: [x, y, w, h] of the face detected in the original image
- face_keypoints: dict containing MTCNN face keypoints in the original image. Can be used if you want to filter the images for a specific pose.
