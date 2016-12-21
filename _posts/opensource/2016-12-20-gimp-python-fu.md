---
layout: post
title: "Gimp Python-Fu "
description: "Automating an image task (scaling) with Gimp's Python-Fu"
category: "opensource"
tags: [linux, gimp, python-fu, automation, api]
---

# Background
A folder full of jpeg images of different sizes that I needed to resize to
300x300. Not wanting to open each image in Gimp - Tools - Transform Tools - Scale
I was looking for a more automated solution. Gimp's Python-Fu, Google and Stackoverflow
with kind souls sharing their expertise to the resuce:

# Gimp Python-Fu
* In Gimp go to Filters - Python-Fu - Console
* Hit Browse to find available Python methods - searched for scale and found
 *gimp_image_scale*, which seemed to do what I wanted.
 
With some more Googling I devised the following, which solves my problem. Pop 
into console and hit enter. See main sources below for proper credit.

{% highlight python %}
import os

def get_files(path):
     for (dir, _, filenames) in os.walk(path):
         for filename in filenames:
             yield os.path.join(dir, filename)

             
list_files = get_files('/my_various_images')


for filename in list_files:
    image = pdb.file_jpeg_load(filename, filename)
    pdb.gimp_image_scale(image, 300, 300)
    new_img = pdb.gimp_image_duplicate(image)
    layer = pdb.gimp_image_merge_visible_layers(new_img, CLIP_TO_IMAGE)
    pdb.gimp_file_save(new_img, layer, filename + '.scaled.jpg', '?')
    pdb.gimp_image_delete(new_img)
    
{% endhighlight %}

# Main sources
* [http://stackoverflow.com/questions/19104693/how-do-you-call-gimp-file-load](http://stackoverflow.com/questions/19104693/how-do-you-call-gimp-file-load)
* [http://stackoverflow.com/questions/3207219/how-to-list-all-files-of-a-directory-in-python (all get_files code)](http://stackoverflow.com/questions/3207219/how-to-list-all-files-of-a-directory-in-python)
* [http://stackoverflow.com/questions/26803732/how-do-i-save-export-all-layers-with-gimps-script-fu](http://stackoverflow.com/questions/26803732/how-do-i-save-export-all-layers-with-gimps-script-fu)
