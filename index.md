---
theme: jekyll-theme-cayman
title: Welcome to the FBCSP Toolbox!
description: Feel free to bookmark this to keep an eye on my project updates
---

# Filter Bank Common Spatial Patterns

Currently in construction
  
FBCSP is a popular method for classifying different motor imagery (MI) classes from electroencephalogram (EEG) signals and is typically used in brain-computer interface (BCI) applications. More information about the algorithm can be found here.

Over the years, FBCSP has become the <a href="https://onlinelibrary.wiley.com/doi/full/10.1002/hbm.23730"><i>"de facto standard"</i></a> method for classifying two or more MI classes. This toolbox provides the tools and methods to use FBCSP on EEG data. Examples are also provided to demonstate how to use this toolbox. 

## About this toolbox
The intention of this toolbox is to provide FBCSP in its original implementation as proposed originally by the authors. Therefore an example code has been provided which contains all the original settings on the BCI Competition dataset IV 2a. The function LoadBCIC imports and epochs the data as originally proposed. Moreover, the toolbox has been written in a modular structure to allow easy reuse of the essential components of the  algorithm on other datasets. An overview of the toolbox can be found <a href="https://fbcsptoolbox.github.io/architecture.md" target="_blank">here</a>. A manual containing the detailed descriptions of the whole toolbox can be downloaded here. 

## How to install this toolbox
Link to the codebase can be found here.
A yml file containing the environment requirements for running this toolbox is also included along with the code.

## How to use this toolbox
EEG data to be used for running this code has not been included along with this toolbox. The example code provided along with this toolbox can be used on the BCI Competition dataset IV 2a and the Korea University dataset. Data can be downloaded in the original GDF format and mat formats, respectively. Data loading functions provided along with this toolbox are configured with defaults to process the data as proposed by the authors and to reproduce the results provided in this manual.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/fbcsptoolbox/fbcsptoolbox.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
