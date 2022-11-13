# Automatic_Mixing_Tutorial-ISMIR_2022-
An ISMIR 2022 tutorial on Automatic Mixing

#How to install and create a Jupyter Book
https://jupyterbook.org/en/stable/start/overview.html 

Clone the repository
``` git clone https://github.com/sai-soum/Automatic_Mixing_Tutorial-ISMIR_2022-.git ```

Create a virtual env
```python -m venv env```

Activate the env
``` source env/bin/activate ```

#Install Jupyter book
``` pip install -U jupyter-book ```

- book/_toc.yml contains table of contents
- book/_config.yml has basic config details
- book/assets contains logo and other media
- book/landing-page.md contains the abstract and presenter info. This is the landing-page. 
- To build the book from scratch: jupyter-book build --all book/
- you can access the html version of the book inside book/_build/html
...................................................................................
#book was created using the command
``` jupyter-book create book/ ```
...................................................................................

Outline

1. Introduction to Audio Engineering #book/part_1
    - intro
    - audio-effects
    - signal-processing
    - technical-aesthetics

2. Music Production #book/part_2
    - music-production
    - intelligent-music-production
        - intro  
        - lit-rev
     
3. Approaches for Automatic Mixing #book/part_3
    - methods
        - intro
        - challenges
        - models
    - dataset
        - intro
        - dataloader
    - evaluation
        - intro
        - obj-metrics
        - sub-metrics

4. Future Direction and Conclusion #book/part_4
    - future-directions
        - models
        - dataset
        - evaluation
    - conclusion

5. Resources #book/part_5
    - references


To-Do:

- [ ] Change Logo
- [ ] Connect to online repo
- [ ] update references
