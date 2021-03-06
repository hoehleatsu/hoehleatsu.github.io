---
layout: post
title: "A Shiny app for your perfect circle"
tags: [rstats, dataviz, image analysis, shiny, imager]
#  bibliography: ~/Literature/Bibtex/jabref.bib
header-includes:
   - \usepackage{bm}
comments: true
editor_options:
  chunk_output_type: console
---



## Abstract:

*The perfect circle* is a shiny app providing a user friendly
interface to the algorithm described in the previous blog post
*Judging Freehand Circle Drawing Competitions*. The app allows one to
score freehand circles directly from the mobile by uploading photos of
them them to a shiny server. An R package "perfectcircle" contains the
scoring API as well as the shiny app.

<center>
<img src="{{ site.baseurl }}/figure/source/2019-02-15-shinycircle/screenshot2.png" width="450">
</center>


{% include license.html %}


## Introduction

The blog post
[Judging Freehand Circle Drawing Competitions](http://staff.math.su.se/hoehle/blog/2018/07/31/circle.html)
contained an image analysis based procedure to automatically score the
circularity of freehand drawn circles. What motivated the post was a
curiosity on how one would rank different freehand drawn circles in a
competition such as the one mentioned by Alexander Overwijk in his
2007
['Perfect Circle' video](https://www.youtube.com/embed/eAhfZUZiwSE). A
few weeks ago, I got an email in response to this post asking about the
state of the scoring software, because there was an interest to hold a
freehand circle drawing competition as part of a math teacher's
conference. This motivated me to wrap the algorithm into a user
friendly interface in order to increase the empty-set of potential
users.

## The Perfect Circle App

The circle segmentation functionality from the blog post was wrapped
into an R package. In particular the function
[`circularity`](https://github.com/hoehleatsu/perfectcircle/blob/fb92ef694b38eb8f409b018c80c827dfb23d0c09/R/perfectcircle.R#L129)
takes an
[`imager`](https://cran.r-project.org/web/packages/imager/index.html)
image [@imager] and a `data.frame` with seedpoints and returns a
circularity measure. This allows one to easily batch process the
images of an entire competition in order to generate a
leaderboard. Furthermore, a shiny app [@shiny] is shipped as part of
the package, which adds a user interface around this API of the
package. Specifically, the app allows the user to upload their image
and provide seed points either by uploading a .csv file or manually
selecting the points in the image. The point selection was possible by
using the ggplot-plotting functionality of the `imager` package
together with the
[`shiny::nearPoints`](https://shiny.rstudio.com/reference/shiny/1.2.0/nearPoints.html)
function.

A general overview of the app is given by the following screencast:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/g8zV5jfvvlo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>
<p>
The R source code of shiny app is available as part of the R package
[perfectcircle](https://github.com/hoehleatsu/perfectcircle) available
from github under a GPLv3 license. A running version of the app can be reached at

<center>
[http://michaelhoehle.eu/shiny/perfectcircle/](http://michaelhoehle.eu/shiny/perfectcircle/)
</center>
<p>

*Note*: Using the app from the above link can lead to "Disconnected
from the server" errors when operating with high resolution
images. Even though tracking memory consumption appears to reveal no
problems, I suspect it to be an out-of-memory error of some sort -
either by the R session run by the shiny server or an error in the
`imager` package. However, reducing the image resolution using the
*Scale Factor* so far always fixed the problem. Furthermore, I did not
experience the problem when running the shiny app locally (Mac OS)

To better illustrate, how the shiny app can facilitate the scoring of
circles on the fly with the camera of your mobile, I made an
additional video tutorial about the adventures of a perfect circle:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/QZOCKn9XNN4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>
<p>

## Discussion

As always it was amazingly easy to use shiny to wrap a user interface
around functionality written in R. I hope the app is useful to
conduct your local freehand circle drawing competition! I would very
much appreciate your feedback. If you want to share
some of your best circles:  bundles of image + seed point .csv files
as pull requests to the
[round-1](https://github.com/hoehleatsu/worldfreehandcirclechampionship/tree/master/round-1) folder
on github are very welcomed!

An insight for me as non-millennial was the ease of the screen
recording feature of Quicktime followed by uploading it to Youtube:
With a few clicks the static-blackboard-fan thus created a first video
blog entry! No less than amazing are IMHO the automatically generated
subtitles on Youtube - a lot of machine learning has happened in
speech recognition!

**Update Feb 2020**: Hanh Nguyen from [Bettermarks](https://nl.bettermarks.com/) used the web-app together with a blackboard + mobile phone setup to hold a Dutch freehand circle drawing championship at the 2020 edition of the
[National Mathematics Days](https://www.uu.nl/onderwijs/nationale-wiskunde-dagen/2020-editie). The competition had more than 100 participants (mostly mathematics high school teachers), some of them taking the app to their classroom! Feedback like this makes me happy.

## Literature
