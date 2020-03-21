---
title: "Visualize jsPsych RT Data"
author: "Rick Gilmore"
date: "2020-03-21 10:45:36"
output: 
  html_document:
    toc: true
    toc_float: true
    toc_depth: 2
    keep_md: true
---



# Purpose

This document shows how to import a JSON file with data from the jsPsych simple RT experiment and to visualize the data using R.

# Preliminaries

We will need the `jsonlite` and `tidyverse` packages.


```r
if (!require("jsonlite")) {
  install.packages("jsonlite")
}
```

```
## Loading required package: jsonlite
```

```r
if (!require("tidyverse")) {
  install.packages("tidyverse")
}
```

```
## Loading required package: tidyverse
```

```
## ── Attaching packages ─────────────────────────── tidyverse 1.3.0 ──
```

```
## ✓ ggplot2 3.3.0     ✓ purrr   0.3.3
## ✓ tibble  2.1.3     ✓ dplyr   0.8.5
## ✓ tidyr   1.0.2     ✓ stringr 1.4.0
## ✓ readr   1.3.1     ✓ forcats 0.5.0
```

```
## ── Conflicts ────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter()  masks stats::filter()
## x purrr::flatten() masks jsonlite::flatten()
## x dplyr::lag()     masks stats::lag()
```

# Import data

The data file is in the root (".") directory of the repository.


```r
list.files(path = ".", pattern = "\\.json$")
```

```
## [1] "sample-data.json"
```

Note that we specify a pattern string to limit the search to files that _end_ with `.json` by using the dollar sign (`$`) character.
The pattern string is a [regular expression](https://en.wikipedia.org/wiki/Regular_expression).
Regular expressions are amazingly powerful strings that control how the computer searches for and filters text.
Rick thinks they are like the spells students at Hogwarts used to learn.
He is in no way a Hermione, but you might want to aspire to that level of excellence.
In regular expressions, characters like the period `.` take on different meanings depending on the context.
Here, we want to *search* for a period in the file name, so we have to put two backslashes `\\` before the period `.` to make that work.

Now, let's import the data file.


```r
file_name <- list.files(path = ".", pattern = "\\.json$")
if (!is.null(file_name)) (rt_data <- jsonlite::read_json(file_name))
```

```
## [[1]]
## [[1]]$rt
## [1] 1022.88
## 
## [[1]]$stimulus
## [1] "Welcome to the experiment. Press any key to begin."
## 
## [[1]]$key_press
## [1] 32
## 
## [[1]]$trial_type
## [1] "html-keyboard-response"
## 
## [[1]]$trial_index
## [1] 0
## 
## [[1]]$time_elapsed
## [1] 1027
## 
## [[1]]$internal_node_id
## [1] "0.0-0.0"
## 
## 
## [[2]]
## [[2]]$rt
## [1] 2787.97
## 
## [[2]]$stimulus
## [1] "<p>In this experiment, a circle will appear in the center of the screen.</p><p>If the circle is <strong>blue</strong>, press the letter F on the keyboard as fast as you can.</p><p>If the circle is <strong>orange</strong>, press the letter J as fast as you can.</p><div style='width: 700px;'><div style='float: left;'><img src='img/blue.png'></img><p class='small'><strong>Press the F key</strong></p></div><div class='float: right;'><img src='img/orange.png'></img><p class='small'><strong>Press the J key</strong></p></div></div><p>Press any key to begin.</p>"
## 
## [[2]]$key_press
## [1] 32
## 
## [[2]]$trial_type
## [1] "html-keyboard-response"
## 
## [[2]]$trial_index
## [1] 1
## 
## [[2]]$time_elapsed
## [1] 3817
## 
## [[2]]$internal_node_id
## [1] "0.0-1.0"
## 
## 
## [[3]]
## [[3]]$rt
## NULL
## 
## [[3]]$stimulus
## [1] "<div style=\"font-size:60px;\">+</div>"
## 
## [[3]]$key_press
## NULL
## 
## [[3]]$test_part
## [1] "fixation"
## 
## [[3]]$trial_type
## [1] "html-keyboard-response"
## 
## [[3]]$trial_index
## [1] 2
## 
## [[3]]$time_elapsed
## [1] 6829
## 
## [[3]]$internal_node_id
## [1] "0.0-2.0-0.0"
## 
## 
## [[4]]
## [[4]]$rt
## [1] 697.07
## 
## [[4]]$stimulus
## [1] "img/blue.png"
## 
## [[4]]$key_press
## [1] 70
## 
## [[4]]$test_part
## [1] "test"
## 
## [[4]]$correct_response
## [1] "f"
## 
## [[4]]$trial_type
## [1] "image-keyboard-response"
## 
## [[4]]$trial_index
## [1] 3
## 
## [[4]]$time_elapsed
## [1] 7528
## 
## [[4]]$internal_node_id
## [1] "0.0-2.0-1.0"
## 
## [[4]]$correct
## [1] TRUE
## 
## 
## [[5]]
## [[5]]$rt
## NULL
## 
## [[5]]$stimulus
## [1] "<div style=\"font-size:60px;\">+</div>"
## 
## [[5]]$key_press
## NULL
## 
## [[5]]$test_part
## [1] "fixation"
## 
## [[5]]$trial_type
## [1] "html-keyboard-response"
## 
## [[5]]$trial_index
## [1] 4
## 
## [[5]]$time_elapsed
## [1] 7783
## 
## [[5]]$internal_node_id
## [1] "0.0-2.0-0.1"
## 
## 
## [[6]]
## [[6]]$rt
## [1] 578.745
## 
## [[6]]$stimulus
## [1] "img/orange.png"
## 
## [[6]]$key_press
## [1] 74
## 
## [[6]]$test_part
## [1] "test"
## 
## [[6]]$correct_response
## [1] "j"
## 
## [[6]]$trial_type
## [1] "image-keyboard-response"
## 
## [[6]]$trial_index
## [1] 5
## 
## [[6]]$time_elapsed
## [1] 8363
## 
## [[6]]$internal_node_id
## [1] "0.0-2.0-1.1"
## 
## [[6]]$correct
## [1] TRUE
## 
## 
## [[7]]
## [[7]]$rt
## NULL
## 
## [[7]]$stimulus
## [1] "<div style=\"font-size:60px;\">+</div>"
## 
## [[7]]$key_press
## NULL
## 
## [[7]]$test_part
## [1] "fixation"
## 
## [[7]]$trial_type
## [1] "html-keyboard-response"
## 
## [[7]]$trial_index
## [1] 6
## 
## [[7]]$time_elapsed
## [1] 8864
## 
## [[7]]$internal_node_id
## [1] "0.0-2.0-0.2"
## 
## 
## [[8]]
## [[8]]$rt
## [1] 474.605
## 
## [[8]]$stimulus
## [1] "img/blue.png"
## 
## [[8]]$key_press
## [1] 70
## 
## [[8]]$test_part
## [1] "test"
## 
## [[8]]$correct_response
## [1] "f"
## 
## [[8]]$trial_type
## [1] "image-keyboard-response"
## 
## [[8]]$trial_index
## [1] 7
## 
## [[8]]$time_elapsed
## [1] 9339
## 
## [[8]]$internal_node_id
## [1] "0.0-2.0-1.2"
## 
## [[8]]$correct
## [1] TRUE
## 
## 
## [[9]]
## [[9]]$rt
## NULL
## 
## [[9]]$stimulus
## [1] "<div style=\"font-size:60px;\">+</div>"
## 
## [[9]]$key_press
## NULL
## 
## [[9]]$test_part
## [1] "fixation"
## 
## [[9]]$trial_type
## [1] "html-keyboard-response"
## 
## [[9]]$trial_index
## [1] 8
## 
## [[9]]$time_elapsed
## [1] 11092
## 
## [[9]]$internal_node_id
## [1] "0.0-2.0-0.3"
## 
## 
## [[10]]
## [[10]]$rt
## [1] 509.765
## 
## [[10]]$stimulus
## [1] "img/orange.png"
## 
## [[10]]$key_press
## [1] 74
## 
## [[10]]$test_part
## [1] "test"
## 
## [[10]]$correct_response
## [1] "j"
## 
## [[10]]$trial_type
## [1] "image-keyboard-response"
## 
## [[10]]$trial_index
## [1] 9
## 
## [[10]]$time_elapsed
## [1] 11602
## 
## [[10]]$internal_node_id
## [1] "0.0-2.0-1.3"
## 
## [[10]]$correct
## [1] TRUE
## 
## 
## [[11]]
## [[11]]$rt
## NULL
## 
## [[11]]$stimulus
## [1] "<div style=\"font-size:60px;\">+</div>"
## 
## [[11]]$key_press
## NULL
## 
## [[11]]$test_part
## [1] "fixation"
## 
## [[11]]$trial_type
## [1] "html-keyboard-response"
## 
## [[11]]$trial_index
## [1] 10
## 
## [[11]]$time_elapsed
## [1] 13103
## 
## [[11]]$internal_node_id
## [1] "0.0-2.0-0.4"
## 
## 
## [[12]]
## [[12]]$rt
## [1] 424.225
## 
## [[12]]$stimulus
## [1] "img/blue.png"
## 
## [[12]]$key_press
## [1] 70
## 
## [[12]]$test_part
## [1] "test"
## 
## [[12]]$correct_response
## [1] "f"
## 
## [[12]]$trial_type
## [1] "image-keyboard-response"
## 
## [[12]]$trial_index
## [1] 11
## 
## [[12]]$time_elapsed
## [1] 13528
## 
## [[12]]$internal_node_id
## [1] "0.0-2.0-1.4"
## 
## [[12]]$correct
## [1] TRUE
## 
## 
## [[13]]
## [[13]]$rt
## NULL
## 
## [[13]]$stimulus
## [1] "<div style=\"font-size:60px;\">+</div>"
## 
## [[13]]$key_press
## NULL
## 
## [[13]]$test_part
## [1] "fixation"
## 
## [[13]]$trial_type
## [1] "html-keyboard-response"
## 
## [[13]]$trial_index
## [1] 12
## 
## [[13]]$time_elapsed
## [1] 15032
## 
## [[13]]$internal_node_id
## [1] "0.0-2.0-0.5"
## 
## 
## [[14]]
## [[14]]$rt
## [1] 399.835
## 
## [[14]]$stimulus
## [1] "img/orange.png"
## 
## [[14]]$key_press
## [1] 74
## 
## [[14]]$test_part
## [1] "test"
## 
## [[14]]$correct_response
## [1] "j"
## 
## [[14]]$trial_type
## [1] "image-keyboard-response"
## 
## [[14]]$trial_index
## [1] 13
## 
## [[14]]$time_elapsed
## [1] 15433
## 
## [[14]]$internal_node_id
## [1] "0.0-2.0-1.5"
## 
## [[14]]$correct
## [1] TRUE
## 
## 
## [[15]]
## [[15]]$rt
## NULL
## 
## [[15]]$stimulus
## [1] "<div style=\"font-size:60px;\">+</div>"
## 
## [[15]]$key_press
## NULL
## 
## [[15]]$test_part
## [1] "fixation"
## 
## [[15]]$trial_type
## [1] "html-keyboard-response"
## 
## [[15]]$trial_index
## [1] 14
## 
## [[15]]$time_elapsed
## [1] 15684
## 
## [[15]]$internal_node_id
## [1] "0.0-2.0-0.6"
## 
## 
## [[16]]
## [[16]]$rt
## [1] 884.945
## 
## [[16]]$stimulus
## [1] "img/blue.png"
## 
## [[16]]$key_press
## [1] 70
## 
## [[16]]$test_part
## [1] "test"
## 
## [[16]]$correct_response
## [1] "f"
## 
## [[16]]$trial_type
## [1] "image-keyboard-response"
## 
## [[16]]$trial_index
## [1] 15
## 
## [[16]]$time_elapsed
## [1] 16570
## 
## [[16]]$internal_node_id
## [1] "0.0-2.0-1.6"
## 
## [[16]]$correct
## [1] TRUE
## 
## 
## [[17]]
## [[17]]$rt
## NULL
## 
## [[17]]$stimulus
## [1] "<div style=\"font-size:60px;\">+</div>"
## 
## [[17]]$key_press
## NULL
## 
## [[17]]$test_part
## [1] "fixation"
## 
## [[17]]$trial_type
## [1] "html-keyboard-response"
## 
## [[17]]$trial_index
## [1] 16
## 
## [[17]]$time_elapsed
## [1] 17822
## 
## [[17]]$internal_node_id
## [1] "0.0-2.0-0.7"
## 
## 
## [[18]]
## [[18]]$rt
## [1] 352.1
## 
## [[18]]$stimulus
## [1] "img/orange.png"
## 
## [[18]]$key_press
## [1] 74
## 
## [[18]]$test_part
## [1] "test"
## 
## [[18]]$correct_response
## [1] "j"
## 
## [[18]]$trial_type
## [1] "image-keyboard-response"
## 
## [[18]]$trial_index
## [1] 17
## 
## [[18]]$time_elapsed
## [1] 18175
## 
## [[18]]$internal_node_id
## [1] "0.0-2.0-1.7"
## 
## [[18]]$correct
## [1] TRUE
## 
## 
## [[19]]
## [[19]]$rt
## NULL
## 
## [[19]]$stimulus
## [1] "<div style=\"font-size:60px;\">+</div>"
## 
## [[19]]$key_press
## NULL
## 
## [[19]]$test_part
## [1] "fixation"
## 
## [[19]]$trial_type
## [1] "html-keyboard-response"
## 
## [[19]]$trial_index
## [1] 18
## 
## [[19]]$time_elapsed
## [1] 19676
## 
## [[19]]$internal_node_id
## [1] "0.0-2.0-0.8"
## 
## 
## [[20]]
## [[20]]$rt
## [1] 311.095
## 
## [[20]]$stimulus
## [1] "img/blue.png"
## 
## [[20]]$key_press
## [1] 70
## 
## [[20]]$test_part
## [1] "test"
## 
## [[20]]$correct_response
## [1] "f"
## 
## [[20]]$trial_type
## [1] "image-keyboard-response"
## 
## [[20]]$trial_index
## [1] 19
## 
## [[20]]$time_elapsed
## [1] 19987
## 
## [[20]]$internal_node_id
## [1] "0.0-2.0-1.8"
## 
## [[20]]$correct
## [1] TRUE
## 
## 
## [[21]]
## [[21]]$rt
## NULL
## 
## [[21]]$stimulus
## [1] "<div style=\"font-size:60px;\">+</div>"
## 
## [[21]]$key_press
## NULL
## 
## [[21]]$test_part
## [1] "fixation"
## 
## [[21]]$trial_type
## [1] "html-keyboard-response"
## 
## [[21]]$trial_index
## [1] 20
## 
## [[21]]$time_elapsed
## [1] 21493
## 
## [[21]]$internal_node_id
## [1] "0.0-2.0-0.9"
## 
## 
## [[22]]
## [[22]]$rt
## [1] 316.1
## 
## [[22]]$stimulus
## [1] "img/orange.png"
## 
## [[22]]$key_press
## [1] 74
## 
## [[22]]$test_part
## [1] "test"
## 
## [[22]]$correct_response
## [1] "j"
## 
## [[22]]$trial_type
## [1] "image-keyboard-response"
## 
## [[22]]$trial_index
## [1] 21
## 
## [[22]]$time_elapsed
## [1] 21810
## 
## [[22]]$internal_node_id
## [1] "0.0-2.0-1.9"
## 
## [[22]]$correct
## [1] TRUE
## 
## 
## [[23]]
## [[23]]$rt
## [1] 3457.145
## 
## [[23]]$stimulus
## [1] "<p>You responded correctly on 100% of the trials.</p><p>Your average response time was 495ms.</p><p>Press any key to complete the experiment. Thank you!</p>"
## 
## [[23]]$key_press
## [1] 32
## 
## [[23]]$trial_type
## [1] "html-keyboard-response"
## 
## [[23]]$trial_index
## [1] 22
## 
## [[23]]$time_elapsed
## [1] 25268
## 
## [[23]]$internal_node_id
## [1] "0.0-3.0"
```

Ok, that worked but it's not a tidy data structure.


```r
str(rt_data)
```

```
## List of 23
##  $ :List of 7
##   ..$ rt              : num 1023
##   ..$ stimulus        : chr "Welcome to the experiment. Press any key to begin."
##   ..$ key_press       : int 32
##   ..$ trial_type      : chr "html-keyboard-response"
##   ..$ trial_index     : int 0
##   ..$ time_elapsed    : int 1027
##   ..$ internal_node_id: chr "0.0-0.0"
##  $ :List of 7
##   ..$ rt              : num 2788
##   ..$ stimulus        : chr "<p>In this experiment, a circle will appear in the center of the screen.</p><p>If the circle is <strong>blue</s"| __truncated__
##   ..$ key_press       : int 32
##   ..$ trial_type      : chr "html-keyboard-response"
##   ..$ trial_index     : int 1
##   ..$ time_elapsed    : int 3817
##   ..$ internal_node_id: chr "0.0-1.0"
##  $ :List of 8
##   ..$ rt              : NULL
##   ..$ stimulus        : chr "<div style=\"font-size:60px;\">+</div>"
##   ..$ key_press       : NULL
##   ..$ test_part       : chr "fixation"
##   ..$ trial_type      : chr "html-keyboard-response"
##   ..$ trial_index     : int 2
##   ..$ time_elapsed    : int 6829
##   ..$ internal_node_id: chr "0.0-2.0-0.0"
##  $ :List of 10
##   ..$ rt              : num 697
##   ..$ stimulus        : chr "img/blue.png"
##   ..$ key_press       : int 70
##   ..$ test_part       : chr "test"
##   ..$ correct_response: chr "f"
##   ..$ trial_type      : chr "image-keyboard-response"
##   ..$ trial_index     : int 3
##   ..$ time_elapsed    : int 7528
##   ..$ internal_node_id: chr "0.0-2.0-1.0"
##   ..$ correct         : logi TRUE
##  $ :List of 8
##   ..$ rt              : NULL
##   ..$ stimulus        : chr "<div style=\"font-size:60px;\">+</div>"
##   ..$ key_press       : NULL
##   ..$ test_part       : chr "fixation"
##   ..$ trial_type      : chr "html-keyboard-response"
##   ..$ trial_index     : int 4
##   ..$ time_elapsed    : int 7783
##   ..$ internal_node_id: chr "0.0-2.0-0.1"
##  $ :List of 10
##   ..$ rt              : num 579
##   ..$ stimulus        : chr "img/orange.png"
##   ..$ key_press       : int 74
##   ..$ test_part       : chr "test"
##   ..$ correct_response: chr "j"
##   ..$ trial_type      : chr "image-keyboard-response"
##   ..$ trial_index     : int 5
##   ..$ time_elapsed    : int 8363
##   ..$ internal_node_id: chr "0.0-2.0-1.1"
##   ..$ correct         : logi TRUE
##  $ :List of 8
##   ..$ rt              : NULL
##   ..$ stimulus        : chr "<div style=\"font-size:60px;\">+</div>"
##   ..$ key_press       : NULL
##   ..$ test_part       : chr "fixation"
##   ..$ trial_type      : chr "html-keyboard-response"
##   ..$ trial_index     : int 6
##   ..$ time_elapsed    : int 8864
##   ..$ internal_node_id: chr "0.0-2.0-0.2"
##  $ :List of 10
##   ..$ rt              : num 475
##   ..$ stimulus        : chr "img/blue.png"
##   ..$ key_press       : int 70
##   ..$ test_part       : chr "test"
##   ..$ correct_response: chr "f"
##   ..$ trial_type      : chr "image-keyboard-response"
##   ..$ trial_index     : int 7
##   ..$ time_elapsed    : int 9339
##   ..$ internal_node_id: chr "0.0-2.0-1.2"
##   ..$ correct         : logi TRUE
##  $ :List of 8
##   ..$ rt              : NULL
##   ..$ stimulus        : chr "<div style=\"font-size:60px;\">+</div>"
##   ..$ key_press       : NULL
##   ..$ test_part       : chr "fixation"
##   ..$ trial_type      : chr "html-keyboard-response"
##   ..$ trial_index     : int 8
##   ..$ time_elapsed    : int 11092
##   ..$ internal_node_id: chr "0.0-2.0-0.3"
##  $ :List of 10
##   ..$ rt              : num 510
##   ..$ stimulus        : chr "img/orange.png"
##   ..$ key_press       : int 74
##   ..$ test_part       : chr "test"
##   ..$ correct_response: chr "j"
##   ..$ trial_type      : chr "image-keyboard-response"
##   ..$ trial_index     : int 9
##   ..$ time_elapsed    : int 11602
##   ..$ internal_node_id: chr "0.0-2.0-1.3"
##   ..$ correct         : logi TRUE
##  $ :List of 8
##   ..$ rt              : NULL
##   ..$ stimulus        : chr "<div style=\"font-size:60px;\">+</div>"
##   ..$ key_press       : NULL
##   ..$ test_part       : chr "fixation"
##   ..$ trial_type      : chr "html-keyboard-response"
##   ..$ trial_index     : int 10
##   ..$ time_elapsed    : int 13103
##   ..$ internal_node_id: chr "0.0-2.0-0.4"
##  $ :List of 10
##   ..$ rt              : num 424
##   ..$ stimulus        : chr "img/blue.png"
##   ..$ key_press       : int 70
##   ..$ test_part       : chr "test"
##   ..$ correct_response: chr "f"
##   ..$ trial_type      : chr "image-keyboard-response"
##   ..$ trial_index     : int 11
##   ..$ time_elapsed    : int 13528
##   ..$ internal_node_id: chr "0.0-2.0-1.4"
##   ..$ correct         : logi TRUE
##  $ :List of 8
##   ..$ rt              : NULL
##   ..$ stimulus        : chr "<div style=\"font-size:60px;\">+</div>"
##   ..$ key_press       : NULL
##   ..$ test_part       : chr "fixation"
##   ..$ trial_type      : chr "html-keyboard-response"
##   ..$ trial_index     : int 12
##   ..$ time_elapsed    : int 15032
##   ..$ internal_node_id: chr "0.0-2.0-0.5"
##  $ :List of 10
##   ..$ rt              : num 400
##   ..$ stimulus        : chr "img/orange.png"
##   ..$ key_press       : int 74
##   ..$ test_part       : chr "test"
##   ..$ correct_response: chr "j"
##   ..$ trial_type      : chr "image-keyboard-response"
##   ..$ trial_index     : int 13
##   ..$ time_elapsed    : int 15433
##   ..$ internal_node_id: chr "0.0-2.0-1.5"
##   ..$ correct         : logi TRUE
##  $ :List of 8
##   ..$ rt              : NULL
##   ..$ stimulus        : chr "<div style=\"font-size:60px;\">+</div>"
##   ..$ key_press       : NULL
##   ..$ test_part       : chr "fixation"
##   ..$ trial_type      : chr "html-keyboard-response"
##   ..$ trial_index     : int 14
##   ..$ time_elapsed    : int 15684
##   ..$ internal_node_id: chr "0.0-2.0-0.6"
##  $ :List of 10
##   ..$ rt              : num 885
##   ..$ stimulus        : chr "img/blue.png"
##   ..$ key_press       : int 70
##   ..$ test_part       : chr "test"
##   ..$ correct_response: chr "f"
##   ..$ trial_type      : chr "image-keyboard-response"
##   ..$ trial_index     : int 15
##   ..$ time_elapsed    : int 16570
##   ..$ internal_node_id: chr "0.0-2.0-1.6"
##   ..$ correct         : logi TRUE
##  $ :List of 8
##   ..$ rt              : NULL
##   ..$ stimulus        : chr "<div style=\"font-size:60px;\">+</div>"
##   ..$ key_press       : NULL
##   ..$ test_part       : chr "fixation"
##   ..$ trial_type      : chr "html-keyboard-response"
##   ..$ trial_index     : int 16
##   ..$ time_elapsed    : int 17822
##   ..$ internal_node_id: chr "0.0-2.0-0.7"
##  $ :List of 10
##   ..$ rt              : num 352
##   ..$ stimulus        : chr "img/orange.png"
##   ..$ key_press       : int 74
##   ..$ test_part       : chr "test"
##   ..$ correct_response: chr "j"
##   ..$ trial_type      : chr "image-keyboard-response"
##   ..$ trial_index     : int 17
##   ..$ time_elapsed    : int 18175
##   ..$ internal_node_id: chr "0.0-2.0-1.7"
##   ..$ correct         : logi TRUE
##  $ :List of 8
##   ..$ rt              : NULL
##   ..$ stimulus        : chr "<div style=\"font-size:60px;\">+</div>"
##   ..$ key_press       : NULL
##   ..$ test_part       : chr "fixation"
##   ..$ trial_type      : chr "html-keyboard-response"
##   ..$ trial_index     : int 18
##   ..$ time_elapsed    : int 19676
##   ..$ internal_node_id: chr "0.0-2.0-0.8"
##  $ :List of 10
##   ..$ rt              : num 311
##   ..$ stimulus        : chr "img/blue.png"
##   ..$ key_press       : int 70
##   ..$ test_part       : chr "test"
##   ..$ correct_response: chr "f"
##   ..$ trial_type      : chr "image-keyboard-response"
##   ..$ trial_index     : int 19
##   ..$ time_elapsed    : int 19987
##   ..$ internal_node_id: chr "0.0-2.0-1.8"
##   ..$ correct         : logi TRUE
##  $ :List of 8
##   ..$ rt              : NULL
##   ..$ stimulus        : chr "<div style=\"font-size:60px;\">+</div>"
##   ..$ key_press       : NULL
##   ..$ test_part       : chr "fixation"
##   ..$ trial_type      : chr "html-keyboard-response"
##   ..$ trial_index     : int 20
##   ..$ time_elapsed    : int 21493
##   ..$ internal_node_id: chr "0.0-2.0-0.9"
##  $ :List of 10
##   ..$ rt              : num 316
##   ..$ stimulus        : chr "img/orange.png"
##   ..$ key_press       : int 74
##   ..$ test_part       : chr "test"
##   ..$ correct_response: chr "j"
##   ..$ trial_type      : chr "image-keyboard-response"
##   ..$ trial_index     : int 21
##   ..$ time_elapsed    : int 21810
##   ..$ internal_node_id: chr "0.0-2.0-1.9"
##   ..$ correct         : logi TRUE
##  $ :List of 7
##   ..$ rt              : num 3457
##   ..$ stimulus        : chr "<p>You responded correctly on 100% of the trials.</p><p>Your average response time was 495ms.</p><p>Press any k"| __truncated__
##   ..$ key_press       : int 32
##   ..$ trial_type      : chr "html-keyboard-response"
##   ..$ trial_index     : int 22
##   ..$ time_elapsed    : int 25268
##   ..$ internal_node_id: chr "0.0-3.0"
```

The `jsonlite::fromJSON` command does a better job parsing the file.


```r
rt_data <- jsonlite::fromJSON(file_name)
str(rt_data)
```

```
## 'data.frame':	23 obs. of  10 variables:
##  $ rt              : num  1023 2788 NA 697 NA ...
##  $ stimulus        : chr  "Welcome to the experiment. Press any key to begin." "<p>In this experiment, a circle will appear in the center of the screen.</p><p>If the circle is <strong>blue</s"| __truncated__ "<div style=\"font-size:60px;\">+</div>" "img/blue.png" ...
##  $ key_press       : int  32 32 NA 70 NA 74 NA 70 NA 74 ...
##  $ trial_type      : chr  "html-keyboard-response" "html-keyboard-response" "html-keyboard-response" "image-keyboard-response" ...
##  $ trial_index     : int  0 1 2 3 4 5 6 7 8 9 ...
##  $ time_elapsed    : int  1027 3817 6829 7528 7783 8363 8864 9339 11092 11602 ...
##  $ internal_node_id: chr  "0.0-0.0" "0.0-1.0" "0.0-2.0-0.0" "0.0-2.0-1.0" ...
##  $ test_part       : chr  NA NA "fixation" "test" ...
##  $ correct_response: chr  NA NA NA "f" ...
##  $ correct         : logi  NA NA NA TRUE NA TRUE ...
```

# Clean data

We want all of the `test` trials where there was an `image-keyboard-response` as the trial type.


```r
rt_data_filtered <- rt_data %>%
  dplyr::filter(., test_part == "test",
          trial_type == "image-keyboard-response")
```

# Plot

Here's a time series.


```r
ggplot(rt_data_filtered) +
  aes(x = trial_index, y = rt, color = stimulus, shape = as.factor(key_press)) +
  geom_point() +
  geom_line()
```

![](visualize-rt-data_files/figure-html/plot-rt-by-trial-stim-side-1.png)<!-- -->

What happened on trial 15? Momentary lapse of some sort.

We could make this prettier, but you get the point.
