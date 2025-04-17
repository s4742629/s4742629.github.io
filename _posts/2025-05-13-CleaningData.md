# Cleaning Data

Here's the table of contents:

1. TOC
{:toc}

## Basic setup

I was doing my elec4630 assignment and recently came across the issue of my model for question 4 being too inaccurate.

![](/Capture.JPG)

There are too many mislabelled entries in the confusion matrix. Also, the t-SNE plot looks like a starfish and is very sparse for all the classes. Since I'm scraping images off of the internet, these inaccuracies are probably from the data itself. So, this is going to a post talking about **data cleaning**, based on the lecture content from the lecture 10a slides.

I started off with trying to pop up all the high loss entries from the dataloader using this code I took from the lectures:
```python
interp.plot_top_losses(10)
```
Were pretty wierd.

![](/Capture.JPG)

So there's a bunch of wierd stuff here. The one that stands out the most is the image of the **sun** labelled as a *dog*. I'm pretty sure this is a result of this line of code `download_images(dest, urls=search_images(f'{o} sunny photo'))` which attempted to grab sunny variants of the image class but winded up getting an actual image of the sun itself. There's also a whole bunch of wierd images, like the black snail image in the corner.

According to lecture 10a, its possible to open up a data cleaner by writing:

```python
cleaner = ImageClassifierCleaner(learn)
cleaner
```
![](/Capture3.JPG)

`YEAR-MONTH-DAY-filename.md`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `filename` is whatever file name you choose, to remind yourself what this post is about. `.md` is the file extension for markdown files.

The first line of the file should start with a single hash character, then a space, then your title. This is how you create a "*level 1 heading*" in markdown. Then you can create level 2, 3, etc headings as you wish but repeating the hash character, such as you see in the line `## File names` above.

## Basic formatting

You can use *italics*, **bold**, `code font text`, and create . Here's a footnote [^1]. Here's a horizontal rule:

---

## Lists

Here's a list:

- item 1
- item 2

And a numbered list:

1. item 1
1. item 2

## Boxes and stuff

> This is a quotation

{% include alert.html text="You can include alert boxes" %}

...and...

{% include info.html text="You can include info boxes" %}

## Images

![](/images/logo.png "fast.ai's logo")

## Code

General preformatted text:

    # Do a thing
    do_thing()

Python code and output:

```python
# Prints '2'
print(1+1)
```

    2

## Tables

| Column 1 | Column 2 |
|-|-|
| A thing | Another thing |

## Footnotes

[^1]: This is the footnote.

