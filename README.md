<div align="center">
<img width="80px" src="book/assets/logo.png"> 

# Deep learning for automatic mixing
[![Jupyter Book Badge](https://jupyterbook.org/badge.svg)](https://dl4am.github.io/tutorial)
[![arXiv](https://img.shields.io/badge/arXiv-2207.08759-b31b1b.svg)](https://arxiv.org/)



[Christian J. Steinmetz](http://Christiansteinmetz.com)<sup>1</sup>, [Soumya Sai Vanka](https://www.saisoumya.com/)<sup>1</sup> 

 [Marco A. Martínez-Ramírez](https://m-marco.com/)<sup>2</sup>, and [Gary Bromham](https://c4dm.eecs.qmul.ac.uk/)<sup>1</sup>

<sup>1</sup> Centre for Digital Music, Queen Mary University of London<br>
<sup>2</sup> Sony Group Corporation, Tokyo, Japan <br>

</div>

This is a web book written for a tutorial session of the 23rd International Society for Music Information Retrieval Conference, Dec 4-8, 2022 held at Bengaluru, India in hybrid format. 
The ISMIR conference is the world’s leading research forum on processing, searching, organising and accessing music-related data.


# Overview 

Mixing is a central task within audio post-production where expert knowledge is required to deliver professional quality content, encompassing both technical and creative considerations. Recently, deep learning approaches have been introduced that aim to address this challenge by generating a cohesive mixture of a set of recordings as would an audio engineer. These approaches leverage large-scale datasets and therefore have the potential to outperform traditional approaches based on expert systems, but bring their own unique set of challenges. In this tutorial, we will begin by providing an introduction to the mixing process from the perspective of an audio engineer, along with a discussion of the tools used in the process from a signal processing perspective.

We will then discuss a series of recent deep learning approaches and relevant datasets, providing code to build, train, and evaluate these systems. Future directions and challenges will be discussed, including new deep learning systems, evaluation methods, and approaches to address dataset availability. Our goal is to provide a starting point for researchers working in MIR who have little to no experience in audio engineering so they can easily begin addressing problems in this domain. In addition, our tutorial may be of interest to researchers outside of MIR, but with a background in audio engineering or signal processing, who are interested in gaining exposure to current approaches in deep learning.

# Cite 

```
@book{deeplearning_auto_mix:book,
    Author = {Steinmetz,Christian and Vanka, Soumya Sai and Martínez, Marco and Bromham, Gary},
    Month = Dec.,
    Publisher = {https://dl4am.github.io/tutorial},
    Title = {Deep Learning for Automatic Mixing},
    Year = 2022,
    Url = {https://dl4am.github.io/tutorial},
    doi = {}
}
```

# Build

Create a Python environment and build the book.
```
python -m venv env
source env/bin/activate
pip install requirements.txt
./scripts/build-book.sh
```

Then you can upload the book to GitHub for hosting. 

```
./scripts/upload-book.sh
```

You can also export the book as a PDF. Note that this requires having TeX installed. 

```
jupyter-book build book/ --builder pdflatex
```