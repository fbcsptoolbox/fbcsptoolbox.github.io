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
The intention of this toolbox is to provide FBCSP in its original implementation as proposed originally by the authors. Therefore an example code has been provided which contains all the original settings on the BCI Competition dataset IV 2a. The function LoadBCIC imports and epochs the data as originally proposed. Moreover, the toolbox has been written in a modular structure to allow easy reuse of the essential components of the  algorithm on other datasets. An overview of the toolbox can be found <a href="https://fbcsptoolbox.github.io/architecture" target="_blank">here</a>. A manual containing the detailed descriptions of the whole toolbox can be downloaded here. 

## How to install this toolbox
Link to the codebase can be found here.
A yml file containing the environment requirements for running this toolbox is also included along with the code.

## How to use this toolbox
EEG data to be used for running this code has not been included along with this toolbox. The example code provided along with this toolbox can be used on the BCI Competition dataset IV 2a and the Korea University dataset. Data can be downloaded in the original GDF format and mat formats, respectively. Data loading functions provided along with this toolbox are configured with defaults to process the data as proposed by the authors and to reproduce the results provided in this manual.