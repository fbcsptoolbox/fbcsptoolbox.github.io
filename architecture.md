layout: page
title: FBCSP Toolbox Architecture
permalink: https://fbcsptoolbox.github.io/architecture

# FBCSP Toolbox Architecture
This section explains the architecture of the FBCSP toolbox. 
To facilitate maximum reuse of the code on other datasets, it has been written in a modular structure.

The remainder of this section will provide a higher level overview of the various classes and methods that make up this toolbox along with a UML class diagram.

A manual in a pdf format can be downloaded here for an in-depth, detailed description of the toolbox.

## Machine Learning Pipeline

### MLEngine

This module serves to integrate the various steps involved in a typical machine learning pipeline for a BCI application. MLEngine.experiment() is the main function that can be used for this purpose. The main components of such a pipeline typically are data loading, preprocessing, splitting the data into training and testing sets, feature extraction, feature selection and classification. To enable maximum reuse of the methods, it is recommended that the data loading functions extract the EEG data into numpy.ndarrays and pass them as outputs for all subsequent signal processing and machine learning. This means that in order to use the other components of this toolbox, data should be arranged as 3D numpy array (trials x channels x time samples) and trial labels should be loaded as a 1D numpy array. The sampling frequency should also be made available to the corresponding classes/methods such as MLEngine.FilterBank. All other dataset specific details should be abstracted away, possibly in other variables/attributes.

## Loading EEG data

### DataLoader

This is the base class that interacts with EEG data files when the (absolute) path to the data folder and filename have been provided. This can the be subclassed to add more functionalities and dataset-specific information for importing and epoching the data. Two exemplary classes have been provided along with this toolbox, namely LoadBCIC and LoadKU, which inherit this base class to load the data from BCI Competition Dataset IV 2a and Korea University, respectively. More methods can be added to this class for intercting with EEG data in other formats.

### LoadBCIC

This class inherits the DataLoader and provides added parameters to specifically load and epoch the BCI Competition Dataset IV 2a. All the parameters for loading and epoching data from this dataset have been adopted from here. The function DataLoader.load_raw_data_gdf() is used to import the EEG data from the gdf files provided from the competition organisers. It is to be noted that this function does not download the data. The data needs to be downloaded prior to using this module.

### LoadKU

This class inherits the DataLoader and provides added parameters to specifically load the Korea University Dataset. Epoched data from mat files are loaded using the DataLoader.load_raw_data_mat() function. It is to be noted that this function does not download the data. The data needs to be downloaded prior to using this module.

## Preprocessing EEG data

###
