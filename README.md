# OSIRIS Zoo
This repository contains three python notebooks designed to help find pairs of images of the same region of comet 67P taken by the OSIRIS scientific camera. It is not completely documented, so feel free to look at the notebooks for dependency information and instructions. The purpose of each notebook is briefly described here:

## rosetta_zoo_getlabels
This notebook is basically a single call to the `psa_utils` package which combines API calls to the EPN-TAP and PDAP services offered by the ESA Planetary Science Archive to download the PDS3 labels of matching images. These labels are text files in a specific format (PVL) which contain key meta-data about each image.

The output is thus a set of labels, which are not contained in this repository.

## rosetta_zoo_metadata
This notebook uses the downloaded PDS3 labels and indexes them in order to build a pandas DataFrame containing selected meta-data determined by a yaml configuration file and the (as yet unpublished) pds3_utils module. This is quite time consuming and as an intermediate step a python pickle is created containing this DataFrame before any additional manipulations. A variable (`read_labels`) determins whether the labels are scraped or whether this Pickle is read from disk in further operations.

The DataFrame is then tidied up, removing entries without relevant meta-data, adding links to the browse and data products in the PSA, and saved to a compressed CSV file.

## rosetta_zoo_pairs
This notebook reads the CSV file produced and gives an example of how it can be used to find pairs of images which meet certain criteria. It is provided as an example only, and the `best_match` function should be adapted to the individual use case. It also provides an example of how to use the browse image URL in the CSV to rapidly display pairs for visual inspection.