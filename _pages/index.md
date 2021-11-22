---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

# description: I am a developer in New York City. I have experience all across the board, from Ruby/Rails and React, to some machine learning.
layout: splash
# author_profile: true
permalink: /

header:
  overlay_color: "#000"
  overlay_image: assets/images/pexels-manuel-geissinger-325229.jpg
  caption: "Photo by Manuel Geissinger from Pexels"
#excerpt: "I am a full-stack developer based in the US. I enjoy the intersection of data science and full-stack."


projects_row1:
  - image_path: assets/images/pexels-tima-miroshnichenko-7991579-2.jpg
    caption: "Photo by Tima Miroshnichenko from Pexels"
    alt: "Box Office Revenue Predictor"
    title: "Box Office Revenue Predictor"
    excerpt: "The classifier predicts a movie box-office revenue."
    btn_label: "Visit"
    btn_class: "btn--primary"
    url: "/projects/Hollywood_bluckbuster_github_portfolio.html" 
    # github_url: ""
  - image_path: assets/images/fitness_small.png
    alt: "E-com Fitness web application"
    title: "E-com Fitness web application"
    excerpt: "A web-based application designed to forecast fitness product sales"
    btn_label: "Visit"
    btn_class: "btn--primary"
    url: "https://ecomfit.herokuapp.com/"

projects_row2:
  - image_path: assets/images/phds_cover_img.png
    alt: "Pattern formation in Reaction-Diffusion systems"
    title: "Pattern formation in Reaction-Diffusion systems"
    excerpt: "Simulations of pattern formation in Chemicla/biological complex system."
    btn_label: "Visit"
    btn_class: "btn--primary"
    url: "/projects/phds"
  - image_path: assets/images/random_cover.png
    alt: "Simulation of heat & mass transfer in porous materials"
    title: "Simulation of heat & mass transfer in porous materials"
    excerpt: "Simulation of heat-mass transfer process to assist in design new porous materials, with potential use in energy-efficient products."
    btn_label: "Visit"
    btn_class: "btn--primary"
    url: "/projects/stoch_combustion"
  - image_path: assets/images/mlayer_laser_cover.png
    alt: "Modeling solidification during metal additive manufacturing"
    title: "Modeling solidification during metal additive manufacturing"
    excerpt: "Simulation of solidification process of sintered powder Aluminum-based alloys."
    btn_label: "Visit"
    btn_class: "btn--primary"
    url: "/projects/laser"
---

<link rel="stylesheet" href="/assets/styles/projects.css">

## About Me:
I am a data professional based at Montreal. I have 7 years of professional work experience in designing high-performance algorithms and deploying advanced statistical techniques to solve problems involving extremely large data sets. 

As a data scientist I have hands on experience with: 
<ul>
<li> ML algorithms & frameworks: Keras, TensorFlow, Scikit-learn</li>
<li> Big Data tools & Cloud Computing: Spark (Ml, SQl), AWS (S3, Redshift, EMR, EC2)</li>
<li> NLP & Sentiment Analysis</li>
<li> Advanced statistical techniques & concepts: Random Forests, Support Vector machine, Gradient boosting, artificial neural networks, Bayesian networks, Regression, Time Series, statistical tests</li>
</ul>


<br>
Below are some of my selected projects.

Hiring? please reach out to me on [LinkedIn](https://www.linkedin.com/in/hossein-azizi/) or just [email me](mailto:hosseinphy@gmail.com).


## Projects
{% include project_row id="projects_row1" %}
{% include project_row id="projects_row2" %}
