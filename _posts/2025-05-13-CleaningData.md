# Cleaning Data

## Premise

I was doing my elec4630 assignment and recently came across the issue of my model for question 4 being too inaccurate.

![](/Capture.JPG)

There are too many mislabelled entries in the confusion matrix. Also, the t-SNE plot looks like a starfish and is very sparse for all the classes. Since I'm scraping images off of the internet, these inaccuracies are probably a result of the image data itself. So, this is going to be a post talking about **data cleaning**, based on the content from the lecture 10a slides from the bear detector.

I started off with trying to pop up all the high loss entries from the dataloader using this code I took from the lectures:
```python
interp.plot_top_losses(10)
```

![](/Capture.JPG)

So, there're a bunch of mislabelleed entries here. The one that stands out the most is the image of the **sun** labelled as a *dog*. I'm pretty sure this is a result of this line of code `download_images(dest, urls=search_images(f'{o} sun photo'))` which attempted to grab sunny variants of the image class but winded up getting an actual image of the sun itself. There's also a whole bunch of wierd images, like the black snail image in the corner.

According to lecture 10a, its possible to open up a data cleaner by writing:

```python
cleaner = ImageClassifierCleaner(learn)
cleaner
```
![](/Capture3.JPG)

In using this GUI, I can set which images I want to relabel and which other one's I want to remove from the system entirely. When I'm finished specifying which images to delete, I can run:

```python
for idx in cleaner.delete():
    cleaner.fns[idx].unlink()
for idx, cat in cleaner.change():
    shutil.move(str(cleaner.fns[idx]), path/cat)
```

To apply my changes in the GUI to the dataset. Seems simple enough, but the problem is that there's so many bad images. One the most common bad images I've seen are these car screens with cats and dogs in them which keep messing up the model.

Also, I'm going to change the image scraper to `download_images(dest, urls=search_images(f'{o} sunny photo'))` to make sure I don't get pictures of the sun.

---
