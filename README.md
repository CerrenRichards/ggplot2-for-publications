# Making figures ready for publication with `ggplot2`

This tutorial offers a step-by-step guide for how to create publication-ready figures using `ggplot2` and the data from `palmerpenguins`.

![image](https://user-images.githubusercontent.com/39834789/86522447-78104680-be38-11ea-8330-3d5fc96ceafc.png)

## Install the package & data

```{r, message = FALSE}
# Install the package
remotes::install_github("allisonhorst/palmerpenguins")

# Load the package
library(palmerpenguins)

# Load the data into the Global Environment
data("penguins")
```

## Meet the Penguins

![image](https://user-images.githubusercontent.com/39834789/86522450-7f375480-be38-11ea-9437-9fd2a382aa7b.png)

Artwork by @allison_horst


## What are culmen length & depth?

The culmen is the upper ridge of a bird’s bill. In the simplified penguins data, culmen length and depth are renamed as variables bill_length_mm and bill_depth_mm to be more intuitive.
For this penguin data, the culmen (bill) length and depth are measured as shown below:

![image](https://user-images.githubusercontent.com/39834789/86522451-84949f00-be38-11ea-9555-6409579f3b58.png)

Artwork by @allison_horst


## The steps for creating a beautiful scatter plot in `ggplot2`

First we will create a basic scatterplot of `body_mass_g` against `bill_length_mm`.

```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
# Load the package
library(ggplot2)

ggplot(penguins, aes(body_mass_g, bill_length_mm))+ # this is the data
     geom_point() # here we add the points
```

<img width="887" alt="Screen Shot 2020-07-04 at 9 09 20 PM" src="https://user-images.githubusercontent.com/39834789/86522580-cd4d5780-be3a-11ea-9cd7-9748d668cbbd.png">

### Change the size of points

We can manually change the size of our datapoints. The points in the standard plot are quite small, so lets increase the size of the points with `size = 3`.

```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
ggplot(penguins, aes(body_mass_g, bill_length_mm))+ 
     geom_point(size = 3) 
```

<img width="887" alt="Screen Shot 2020-07-04 at 9 11 04 PM" src="https://user-images.githubusercontent.com/39834789/86522590-e5bd7200-be3a-11ea-822e-c40d3e55dcdc.png">


### Change the shape of points

In `ggplot2`, it is possible to change the shape of the points. Here is a quick reference guide:

![shapes](https://user-images.githubusercontent.com/39834789/86522564-8e1f0680-be3a-11ea-9c7b-8cd1f39eb479.png)

The shape of all datapoints can be changed with e.g. `shape = 8`.

```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
ggplot(penguins, aes(body_mass_g, bill_length_mm))+
     geom_point(size = 3, shape = 8) 
```

<img width="887" alt="Screen Shot 2020-07-04 at 9 15 40 PM" src="https://user-images.githubusercontent.com/39834789/86522659-e4407980-be3b-11ea-823a-65dabc7f10e2.png">


Alternatively, we can change the shape of our points based on species with `aes(shape = species)`.

```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
ggplot(penguins, aes(body_mass_g, bill_length_mm))+ 
     geom_point(aes(shape = species), size = 3) 
```

<img width="887" alt="Screen Shot 2020-07-04 at 9 16 06 PM" src="https://user-images.githubusercontent.com/39834789/86522661-e7d40080-be3b-11ea-9d02-fb763a7c2c00.png">

### Change the opacity of points

You can also change the opacity of the data points using `alpha`. Alpha values are required to be between 0 - 1 where 0 is transparent and 1 is opaque.  

```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
ggplot(penguins, aes(body_mass_g, bill_length_mm))+ 
     geom_point(aes(shape = species), size = 3, alpha = 0.6) 
```

<img width="887" alt="Screen Shot 2020-07-04 at 9 16 40 PM" src="https://user-images.githubusercontent.com/39834789/86522662-e86c9700-be3b-11ea-8cd7-ff602bbfd4ad.png">

### Adding colour

Now lets explore the different species by adding colour with the code `colour = species`. 

```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
ggplot(penguins, aes(body_mass_g, bill_length_mm))+ 
     geom_point(aes(shape = species, colour = species), size = 3, alpha = 0.6) 
```

<img width="887" alt="Screen Shot 2020-07-04 at 9 17 00 PM" src="https://user-images.githubusercontent.com/39834789/86522663-e86c9700-be3b-11ea-961d-0321b70dc2e7.png">

This red-green colour combination is colourblind unfrieldly, so lets change the colour of the points with `scale_colour_manual`. To ensure the shapes match with the names we will also use `scale_shape_manual`.

```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
ggplot(penguins, aes(body_mass_g, bill_length_mm))+ 
     geom_point(aes(shape = species, colour = species), size = 3, alpha = 0.6)+ 
  
  scale_colour_manual(values = c("#C15CCB", "#00868B", "#FF6A00"), 
                      labels = c("Chinstrap", "Gentoo", "Adélie"))+
  scale_shape_manual(values = c(17, 15, 16),
                     labels = c("Chinstrap", "Gentoo", "Adélie"))
```

<img width="887" alt="Screen Shot 2020-07-04 at 9 17 21 PM" src="https://user-images.githubusercontent.com/39834789/86522664-e9052d80-be3b-11ea-8124-a6e5e97002ab.png">

We won't change the points any more, so let's save the plot as `penguin_plot`, so we can build upon it.

```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
penguin_plot <- ggplot(penguins, aes(body_mass_g, bill_length_mm))+ 
     geom_point(aes(shape = species, colour = species), size = 3, alpha = 0.6)+ 
  
     scale_colour_manual(values = c("#C15CCB", "#00868B", "#FF6A00"), 
                      labels = c("Chinstrap", "Gentoo", "Adélie"))+
     scale_shape_manual(values = c(17, 15, 16),
                     labels = c("Chinstrap", "Gentoo", "Adélie"))
```

### Changing the background

You can change the background of `ggplot2` figures in a variety of ways with: 

- `theme_gray()`
- `theme_bw()`
- `theme_linedraw()`
- `theme_light()`
- `theme_minimal()`
- `theme_classic()`
- `theme_void()`
- `theme_dark()`

<img width="553" alt="Screen Shot 2020-07-04 at 9 18 04 PM" src="https://user-images.githubusercontent.com/39834789/86522665-e99dc400-be3b-11ea-9696-4ad2a5adfb0f.png">


My personal favourite is `theme_bw` therefore we will continue to make our plot with this theme. 

We will further remove the thicker lines in the background with `panel.grid.major = element_blank()`, and the thinner lines with `panel.grid.minor = element_blank()`.

```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
penguin_plot + 
  theme_bw()+ # set the background theme                                                 
  theme(panel.grid.major = element_blank(), # remove the major lines
        panel.grid.minor = element_blank()) # remove the minor lines
```

<img width="802" alt="Screen Shot 2020-07-04 at 9 22 35 PM" src="https://user-images.githubusercontent.com/39834789/86522769-8ad94a00-be3d-11ea-8f85-e925c5b40cce.png">

### Changing the text size

There are several ways to change the size of the font, but we can quickly change all font size with `theme_bw(base_size = 20)`.

```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
penguin_plot <- penguin_plot + 
  theme_bw(base_size = 15)+                                                 
  theme(panel.grid.major = element_blank(),
        panel.grid.minor = element_blank()) 

penguin_plot
```

<img width="802" alt="Screen Shot 2020-07-04 at 9 23 00 PM" src="https://user-images.githubusercontent.com/39834789/86522979-5fa42a00-be40-11ea-9271-6a1b831736e8.png">

### Renaming the axes and legend

You can rename the axes and legend using `labs`.


```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
penguin_plot <- penguin_plot + 
  labs(x = "Body Mass (g)", y = "Bill Length (mm)", colour = "Species", shape = "Species")

penguin_plot
```


<img width="802" alt="Screen Shot 2020-07-04 at 9 23 16 PM" src="https://user-images.githubusercontent.com/39834789/86522980-629f1a80-be40-11ea-963c-c74015f4e1f3.png">

### Change axes position

In the standard plots, the axes titles are really close to the plot. We will increase their distance with `vjust`:

```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
penguin_plot <- penguin_plot + 
    theme(axis.title.y = element_text(vjust = 3))+ # increase distance from the y-axis
    theme(axis.title.x = element_text(vjust = -1)) # increase distance from the x-axis

penguin_plot
```

<img width="802" alt="Screen Shot 2020-07-04 at 9 23 33 PM" src="https://user-images.githubusercontent.com/39834789/86522981-6337b100-be40-11ea-8cad-2ec62cbba3c6.png">

### Change legend position

Legends can be positioned in a number of different ways using `legend.position`:

- `theme(legend.position="top")`
- `theme(legend.position="bottom")`
- `theme(legend.position="left")`
- `theme(legend.position="right")`
- `theme(legend.position="none")`

Legend loction can be also a numeric vector c(x,y), where x and y are the coordinates of the legend box. Their values should be between 0 - 1. c(0,0) is the “bottom left” and c(1,1) is the “top right” position.


```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
penguin_plot <- penguin_plot + 
    theme(legend.position = c(0.85, 0.2))

penguin_plot
```

<img width="823" alt="Screen Shot 2020-07-04 at 9 23 52 PM" src="https://user-images.githubusercontent.com/39834789/86522982-63d04780-be40-11ea-9840-93bd41523d72.png">

### Saving the figure

Publications require high quality images and they specify the size and format required on their website. 

#### `ggsave`
`ggsave` is one example of how to save your figures. 

It allows you to save high quality images in a variety of different file types (e.g. "png", "eps", "ps", "tex", "pdf", "jpeg", "tiff", "png", "bmp", "svg", "wmf"). You can also specify the `width` and `height` in "in", "cm", or "mm", and specify the plot resolution with `dpi`.

```{r, eval = FALSE}
# This will save the last plot for the code you ran:

ggsave("penguin_plot.pdf", 
       dpi = 600, 
       width = 100, height = 60, unit = "mm")
```

#### `pdf`

An alternative method is to use `pdf`. This allows you to specify the colour mode (e.g. cmyk).

```{r, eval = FALSE}
pdf("ggplot-cmyk.pdf", width = 12 / 2.54, height = 8 / 2.54,
    colormodel = "cmyk")

print(penguin_plot)

dev.off()
```



## More `ggplot2` plots and tricks 


### Change the size of points based on other data

Size can be changed based on data within the `penguins` dataframe. For example, here we have changed the size of the points based on `bill_depth_mm`.

```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
ggplot(penguins, aes(body_mass_g, bill_length_mm))+ 
     geom_point(aes(size = bill_depth_mm)) 
```
<img width="823" alt="Screen Shot 2020-07-04 at 9 24 22 PM" src="https://user-images.githubusercontent.com/39834789/86522983-63d04780-be40-11ea-9169-6c766151715c.png">

### Adding an ellispe

Add 95% confidence interval ellispses with `stat_ellipse`.

```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
ellipse<- penguin_plot + 
  stat_ellipse(aes(colour = species, level=0.95))
  

ellipse
```

<img width="823" alt="Screen Shot 2020-07-04 at 9 24 42 PM" src="https://user-images.githubusercontent.com/39834789/86522964-29ff4100-be40-11ea-8a8b-dfb4fa8cb66a.png">


### Linear regression line

Add a linear regression line with `geom_smooth(method=lm)`.

```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
lm <- penguin_plot + 
  geom_smooth(method=lm, aes(colour = species))

lm 
```
<img width="823" alt="Screen Shot 2020-07-04 at 9 24 56 PM" src="https://user-images.githubusercontent.com/39834789/86522966-2cfa3180-be40-11ea-8a52-2a9b094f2c62.png">

### `facet_wrap`

`facet_wrap` is a fantastic tool to slit plots based on a specified categorical column. Here we will use the `species` column.  

```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
penguin_plot + 
  facet_wrap(~species, ncol = 3, nrow = 1) + # specifying 3 columns, 1 row
  theme(legend.position = "none") # remove legend
```

<img width="823" alt="Screen Shot 2020-07-04 at 9 25 12 PM" src="https://user-images.githubusercontent.com/39834789/86522947-e4db0f00-be3f-11ea-9766-0b4539fec0b9.png">


### Changing strip design

It is also possible to change the `size`, `colour`, `face` and `fill` colour of the facet strips with the following code:

```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
penguin_plot + 
  facet_wrap(~species, ncol = 3, nrow = 1) + # specifying 3 columns, 1 row
  theme(legend.position = "none")+ # remove legend
    theme(strip.text.x = element_text(size = 16, color = "white", face = "bold"), 
          strip.background = element_rect(fill="black"))
```

<img width="823" alt="Screen Shot 2020-07-04 at 9 25 28 PM" src="https://user-images.githubusercontent.com/39834789/86522949-e73d6900-be3f-11ea-8d8c-d94e218183d3.png">


### Removing white space and free axes

We can also remove the free space using `scales = free`.

```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
penguin_plot + 
  facet_wrap(~species, scales = "free")+ 
  theme(legend.position = "none")+ # remove legend
    theme(strip.text.x = element_text(size = 16, color = "white", face = "bold"), 
          strip.background = element_rect(fill="black"))
```

<img width="823" alt="Screen Shot 2020-07-04 at 9 25 48 PM" src="https://user-images.githubusercontent.com/39834789/86522950-e7d5ff80-be3f-11ea-907d-6db8db3bbdc7.png">


### `facet_grid`: Free facet width

To allow the facets to be different widths, we must use `facet_grid` and `space = "free"`. This can be used with `scales = "free"`.

```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
penguin_plot + 
  facet_grid(.~species, scales = "free", space = "free")  +
  theme(legend.position = "none")+ # remove legend
    theme(strip.text.x = element_text(size = 16, color = "white", face = "bold"), 
          strip.background = element_rect(fill="black"))
```
<img width="823" alt="Screen Shot 2020-07-04 at 9 26 06 PM" src="https://user-images.githubusercontent.com/39834789/86522951-e86e9600-be3f-11ea-9bbc-e4421015a054.png">

### Bar plot


```{r, warning=FALSE, fig.align = "center", message = FALSE, out.width = '50%'}
library(dplyr)
penguin_summary <-  penguins %>% 
                    group_by(species) %>% 
                    summarise(mean = mean(body_mass_g, na.rm = T), 
                              sd = sd(body_mass_g, na.rm = T))


ggplot(penguin_summary, aes(y = mean, x=species, fill = species)) + 
  geom_bar(stat="identity")+
   geom_errorbar(aes(ymin = mean-sd, ymax = mean+sd), 
                width=.1)  
```
<img width="823" alt="Screen Shot 2020-07-04 at 9 26 26 PM" src="https://user-images.githubusercontent.com/39834789/86522919-988fcf00-be3f-11ea-9150-58c63f1029e7.png">

Create the plot like the code above for the scatter plot.

```{r, warning=FALSE, fig.align = "center", out.width = '50%'}
bar <- ggplot(penguin_summary, aes(y = mean, x = species, fill = species)) + 
  geom_bar(stat = "identity")+
  geom_errorbar(aes(ymin = mean-sd, ymax = mean+sd), 
                width=.1)+
  theme_bw(base_size = 20)+
  theme(panel.grid.major = element_blank(), panel.grid.minor = element_blank())+
  labs(x = "Species", y = "Body Mass (g)")+
 scale_fill_manual(values = c( "#FF6A00","#C15CCB",  "#00868B"))+
  theme(legend.position = "none") +
  scale_y_continuous(limits = c(0, 5700))+
  theme(axis.title.y = element_text(vjust = 3)) +
  theme(axis.title.x = element_text(vjust = -1)) 

bar
```
<img width="823" alt="Screen Shot 2020-07-04 at 9 26 41 PM" src="https://user-images.githubusercontent.com/39834789/86522921-99c0fc00-be3f-11ea-84a6-11f299072466.png">

### Histogram

```{r, warning=FALSE, fig.align = "center", message = FALSE, out.width = '50%'}
ggplot(penguins, aes(x = flipper_length_mm, fill = species)) + 
  geom_histogram(alpha = 0.4)+
  scale_fill_manual(values = c( "#FF6A00","#C15CCB",  "#00868B"))
```

<img width="823" alt="Screen Shot 2020-07-04 at 9 26 57 PM" src="https://user-images.githubusercontent.com/39834789/86522901-5cf50500-be3f-11ea-8118-717799bcfcbd.png">

### Density Plot

```{r, warning=FALSE, fig.align = "center", message = FALSE, out.width = '50%'}
ggplot(penguins, aes(x = flipper_length_mm, fill = species)) + 
  geom_density(alpha = 0.4)+
  scale_fill_manual(values = c( "#FF6A00","#C15CCB",  "#00868B"))
```

<img width="823" alt="Screen Shot 2020-07-04 at 9 27 14 PM" src="https://user-images.githubusercontent.com/39834789/86522902-5ebec880-be3f-11ea-9a0e-695413543356.png">

```{r, warning=FALSE, fig.align = "center", message = FALSE, out.width = '50%'}
 flipper <- ggplot(penguins, aes(x = flipper_length_mm, fill = species, colour = species)) + 
  geom_density(alpha = 0.4)+
  scale_fill_manual(values = c( "#FF6A00","#C15CCB",  "#00868B"))+
  scale_colour_manual(values = c( "#FF6A00","#C15CCB",  "#00868B"))+
  theme_bw(base_size = 20)+
  theme(panel.grid.major = element_blank(), panel.grid.minor = element_blank())+
  labs(x = "Flipper Length (mm)", y = "Density", fill = "Species", colour = "Species")+
  #theme(legend.position = "none") +
  scale_x_continuous(expand = c(0,0), limits = c(165, 238))+
  scale_y_continuous(expand = c(0,0), limits = c(0, 0.065), breaks=seq(0, 0.065, 0.02))+
  theme(axis.title.y = element_text(vjust = 3)) +
  theme(axis.title.x = element_text(vjust = -1)) 

flipper 
```

<img width="823" alt="Screen Shot 2020-07-04 at 9 27 30 PM" src="https://user-images.githubusercontent.com/39834789/86522903-5feff580-be3f-11ea-8d42-52f75619abaf.png">

### Add a mean line

```{r, warning=FALSE, fig.align = "center", message = FALSE, out.width = '50%'}
flipper_mean <- penguins %>%
        group_by(species) %>%
        summarise(mean = mean(flipper_length_mm, na.rm = TRUE))
  
density <- flipper +
  geom_vline(data = flipper_mean, aes(xintercept = mean, colour = species), linetype = "dashed", size = 1.3)

density
```

<img width="823" alt="Screen Shot 2020-07-04 at 9 27 47 PM" src="https://user-images.githubusercontent.com/39834789/86522904-60888c00-be3f-11ea-91a6-8d1e3ae38e46.png">


### Box plot

```{r, warning=FALSE, fig.align = "center", message = FALSE, out.width = '50%'}
ggplot(na.omit(penguins), aes(x=species, y=flipper_length_mm, fill=sex)) +
  geom_boxplot()
```
<img width="823" alt="Screen Shot 2020-07-04 at 9 28 03 PM" src="https://user-images.githubusercontent.com/39834789/86522880-156e7900-be3f-11ea-9f1c-9959595a8e5f.png">


```{r, warning=FALSE, fig.align = "center", message = FALSE, out.width = '50%'}
box_plot<- ggplot(na.omit(penguins), aes(x=species, y=flipper_length_mm, fill=sex)) +
  geom_boxplot()+
  theme_bw(base_size = 20)+
  theme(panel.grid.major = element_blank(), panel.grid.minor = element_blank())+
  labs(x = "Species", y = "Flipper Length (mm)", fill = "Sex")+
   theme(axis.title.y = element_text(vjust = 3)) +
  theme(axis.title.x = element_text(vjust = -1)) +
  theme(legend.position = c(0.15, 0.8))

box_plot
```
<img width="823" alt="Screen Shot 2020-07-04 at 9 28 17 PM" src="https://user-images.githubusercontent.com/39834789/86522876-0ab3e400-be3f-11ea-92c7-8a7bf2fb638d.png">


### Arrange plots

There are several different methods that allow you to arrange your plots into different panels. 

#### `ggarrange`

Here we will arrange four of the plots that we made above into one figure using `ggarrange`. You can specify the number of rows `nrow` and `ncol` and add `labels. 

Note we previously saved our figures (`ellipse`, `density`, `bar`, `box_plot`) in the Global Environment and we are calling on them here.


```{r, warning=FALSE, fig.align = "center", message = FALSE, fig.width=12, fig.height=8}
library(ggpubr)

ggarrange(ellipse, density, bar, box_plot,
          nrow = 2, ncol = 2,
          labels = c("a", "b", "c", "d"))
```


<img width="887" alt="Screen Shot 2020-07-04 at 9 28 41 PM" src="https://user-images.githubusercontent.com/39834789/86522873-f4a62380-be3e-11ea-8d5f-1f914c14a793.png">


#### Same axes

If two plots have the same axes, you can remove one and use `align = "v"` to ensure the plots remain the same size.

```{r, warning=FALSE, fig.align = "center", message = FALSE, fig.width=12, fig.height=8}
# Remove y axes text and title
lm <- lm +
   theme(axis.title.y=element_blank(),
        axis.text.y=element_blank(),
        axis.ticks.y=element_blank())


ggarrange(ellipse, lm,
          nrow = 1, ncol = 2,
          labels = c("a", "b"),
          align = "v")
```

<img width="887" alt="Screen Shot 2020-07-04 at 9 29 02 PM" src="https://user-images.githubusercontent.com/39834789/86522871-e48e4400-be3e-11ea-99cd-f43f1c9edd5d.png">


#### `patchwork`

`patchwork` is a very straighforward and intuative package for arranging plots. 
e.g:

- `plot1 + plot2` aligns two plots next to each other
- `plot1 / plot2` aligns plot2 under plot1

Lets make a fancy one. 

We add the figure labels with e.g. `labs(tag = 'a')`. We will also make two of our plots half the size of the main plot with `plot_layout(widths=c(2,1))`.


```{r, warning=FALSE, fig.align = "center", message = FALSE, fig.width=18, fig.height=10}
library(patchwork)

(ellipse + labs(tag = 'a')| ((bar+ labs(tag = 'b')) / (box_plot +labs(tag = 'c')))) + plot_layout(widths=c(2,1))
```
<img width="887" alt="Screen Shot 2020-07-04 at 9 29 25 PM" src="https://user-images.githubusercontent.com/39834789/86522867-d93b1880-be3e-11ea-863c-d4ca3b0498f6.png">


![image](https://user-images.githubusercontent.com/39834789/86522452-88282600-be38-11ea-8095-4d2cfcd60373.png)

Artwork by @CerrenRichards

