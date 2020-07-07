---
theme: jekyll-theme-cayman
title: Welcome to the FBCSP Toolbox!
---

# Filter Bank Common Spatial Patterns

Currently under construction
  
FBCSP is a popular method for classifying motor imagery (MI) (multiple classes) from electroencephalogram (EEG) signals and is typically used in brain-computer interface (BCI) applications. More information about the algorithm can be found in <a href="https://ieeexplore.ieee.org/document/4634130">Ang et al., 2008</a>.

Over the years, FBCSP has been widely deployed or benchmarked for classifying two or more MI classes. This toolbox provides the tools and methods to use FBCSP on EEG data. <a href="https://fbcsptoolbox.github.io/tutorials" target="_blank">Examples</a> are also provided to demonstrate how to use this toolbox. 

## About this toolbox
The aim of this toolbox is to provide FBCSP in its original implementation as proposed originally by the <a href="https://fbcsptoolbox.github.io/publications#Ang2012frontiers" target="_blank">authors</a>. Therefore an <a href="https://fbcsptoolbox.github.io/tutorials" target="_blank">example code</a> has been provided which contains all the original settings on the <a href="http://www.bbci.de/competition/iv">BCI Competition dataset IV 2a</a>. The class `LoadBCIC` imports and epochs the data as originally proposed. Moreover, the toolbox has been written in a modular structure to allow easy reuse of the essential components of the  algorithm on other datasets. An overview of the toolbox can be found <a href="https://fbcsptoolbox.github.io/architecture" target="_blank">here</a>. A manual containing the detailed descriptions of the whole toolbox can be downloaded <a href="">here</a>. 

## How to install this toolbox
Link to the codebase can be found <a href="">here</a>.
A yml file containing the environment requirements for running this toolbox is also included along with the code.

## How to use this toolbox
EEG data to be used for running this code has not been included along with this toolbox. The example code provided along with this toolbox can be used on the <a href="http://www.bbci.de/competition/iv">BCI Competition dataset IV 2a</a> and the <a href="https://academic.oup.com/gigascience/article/8/5/giz002/5304369">Korea University dataset</a>. Data can be downloaded in the original GDF format and mat formats, respectively. Data loading functions provided along with this toolbox are configured with defaults to process the data as proposed by the authors and to reproduce the results provided in this manual.

## Contact
Tushar Chouhan, <i>PhD</i>
email: ntubci.scse[at]gmail.com