# My meme:

![meme](https://user-images.githubusercontent.com/65698262/159200662-6f8f4f2c-a15b-4b47-900e-4a560c586734.png)

## The motivation:

I wanted to make something as self-explanatory as possible. So my idea was to *ONLY* use memes to make memes. Memes into **new** memes. 

- The text at the top is kind of only so that I can practice using the image_annotate() function in Part A of the assignment, could go without it. 

- Likewise for the hot pink border! Just wanted to try use these functions. 

Team squidward!!! :^)

## R code used:

```{r, echo=TRUE}
library("magick")

# load squidward images
squidward_chair_url <- "https://pbs.twimg.com/media/EvJJzJUUUAUAZA6.jpg"
squidward_chair <- image_read(squidward_chair_url)%>% image_scale(450)

squidward_leaving_url <- "https://static.wikia.nocookie.net/cbe73667-82f1-41ef-bc55-1e059ea06c08/scale-to-width/755"
squidward_leaving <- image_read(squidward_leaving_url) %>%
  image_scale(600) %>% 
  image_crop("450x450+0")
squidward_leaving

# load drake image
drake_url <- "https://www.meme-arsenal.com/memes/b61471ab564a22bf014ad06f07098e5f.jpg"
drake <- image_read(drake_url) %>% image_scale(250)

# blank canvas and then add text
title <- image_blank(width = 700, height = 100, color = "#ffffff") %>% 
  image_annotate(text="When they ask me how I like my memes:",
                 color = "#000000",
                 size = 40,
                 font = "Serif",
                 gravity = "center")

# Stack the squidwards
squid_vector <- c(squidward_leaving, squidward_chair)
stacked_squidward <- image_append(squid_vector, stack = TRUE)

# TOP
top_panel_vector <- c(squidward_leaving, drake)
top_panel <- image_append(top_panel_vector) 

# BOTTOM
small_stacked_squidward <- stacked_squidward %>% image_scale(250)
bottom_panel_vector <- c(squidward_chair, small_stacked_squidward)
bottom_panel <- image_append(bottom_panel_vector) 

# APPEND TOP & BOTTOM
combined_vector <- c(title, top_panel, bottom_panel)
combined <- image_append(combined_vector, stack = TRUE)

# add border
meme_image <- image_border(image_background(combined, "pink"), "#ffffff", "20x20") %>%
  image_border("#e60ee2", "10x10")

meme_image
```
