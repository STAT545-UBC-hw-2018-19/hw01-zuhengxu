![Zuheng Xu](http://www.yishuzi.com/i/11/1033.png?0912110552678)


## Overview

Welcome to this repository, which provides a brief introduction to **Zuheng(David) Xu** [@zuhengxu](https://github.com/zuhengxu) and is also a test for the realizaitons of various markdown functions.

### what you can find here:
* *An introduction about myself*
* *[Some materials about STAT545](https://github.com/zuhengxu/STAT545_participation)*
* *Some boring codes* :dizzy_face:

## About Me 
My name is **Zuheng Xu**, as shown on the top, and you can also call me **David**. I am a new master student in statistics and it's also my first year in Canada. Nice to meet all you guys in STAT545.

### Hobby
#### *Bascketball*:basketball:
I enjoy the competitiveness in a bascketball game. **Dwyane Wade** is my favorate player, who is also known as *flashman*.
![Dwyane Wade](http://hauteliving.com/wp-content/uploads/2018/02/IMG_0417.jpg)

  
#### *Biking*:bicyclist:
It's always enjoyable to biking on weekends. I am into fixed gear biking.
![Fixed gear](http://78.media.tumblr.com/7615d8f73ef8109a79f4f1f379a0675f/tumblr_n5ugj5Vh3Y1qd8i4ko1_400.gif)

#### *Movies*:movie_camera:
![movies](https://qph.fs.quoracdn.net/main-qimg-51ed1bcde002dca611ea48918e008401) 

> There’s a chance you watch a tragedy movie that’s even worse than whatever’s going on in your life to remind you there’s still hope or simply giving you a good cry to release your sadness; or you might want to watch a movie with happy ending to cheer you up. 

### Reseach Interests
| **Area** | **Reason**                        |
|------------------------|--------------------------|
| ML|Incredibally effective    |
|Beyesian | More interesting  |
| MCMC   | Can explore traditional problem by using stat simulation|


### To-do lists this week
- [x] Finish Readme.md
- [x] Food prep for this week 
- [ ] TA lab

## Materials about STAT545

### Markdown exploration 
##### about how to edit `.md` file 
Here is some markdown notes I've taken in class01 and before.
* [how to insert a math equation](https://github.com/zuhengxu/STAT545_participation/blob/master/Markdown%20Math%20equations.md)
* [how to build lists](https://github.com/zuhengxu/STAT545_participation/blob/master/lists.md)
* [a macdown template provided by Macdown](https://github.com/zuhengxu/STAT545_participation/blob/master/markdown%20template.md)
* [note teken in class02](https://github.com/zuhengxu/STAT545_participation/blob/master/md%20explorer/md%20explorer.md)


### R markdown
##### about using Rmardown and editing `.rmd` files 
* [r markdown practce in class03](https://github.com/zuhengxu/STAT545_participation/blob/master/cm_003/in%20class%20excercise_sep11.Rmd) 
but it looks wierd since we cannot see the output of `.rmd` on github
* [a `.r` script about basic r syntex and command](https://github.com/zuhengxu/STAT545_participation/blob/master/cm_003/cm003-in%20class%20exercise-R.r)
* [official R Markdown guide](https://bookdown.org/yihui/rmarkdown/)

### Navigation to STAT Participation

* cm_001 *(I didn't create a folder for cm_001 since I didn't upload any file in that class)*
  * [say hi](https://github.com/STAT545-UBC/Discussion-Internal/issues/2) *You can find @zuhengxu in the disscssion board*.
  * [my recommendation to markdown editor](https://github.com/STAT545-UBC/Discussion-Internal/issues/6) *two live-preview editors*.
* [cm_002](https://github.com/zuhengxu/STAT545_participation/tree/master/cm_002)
* [cm_003](https://github.com/zuhengxu/STAT545_participation/tree/master/cm_003)


## Some Boring Code

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

Here is a piece of code about *Accept-Reject Methods* for \\(\beta\\) distribution: 

```
#matlab
function Z = exbeta(a,b) 
D=(((a-1)/(a+b-2))^(a-1))*(((b-1)/(a+b-2))^(b-1))/B(a,b);
while 1
X=unifrnd(0,1);
R=unifrnd(0,1);
  if R<=(X^(a-1))*((1-X)^(b-1))/(B(a,b)*D)
    Z=X;
    break
  else return
  end
end
```
