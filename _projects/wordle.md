---
layout: project
title: "Wordle"
date: 2024-06-30
description: This is a package that replicates the New York Times Wordle game in the R Console. The code of this project can be found on <a href="https://github.com/andreghl/wordle">Github</a>.
lang: R
---

{% marginfigure "game" '../assets/wordle/game.png' "The game can be played once the package is loaded by running ```wordle()``` and looks as follows." %}

I created this project to learn how to create a package in R. If you wish to install this package on your device, run:

```R
# install.packages("devtools") 
devtools::install_github("andreghl/wordle")
library(wordle)

wordle()
```

For each attempt, the output is kept at a minimum, only presenting the necessary information. Also, the program does not check whether the attempted word is within the list of available words. This task is left to the player.  []()