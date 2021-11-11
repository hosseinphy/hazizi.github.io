---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

description: I am a developer in New York City. I have experience all across the board, from Ruby/Rails and React, to some machine learning.
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
    url: "/projects/Classification_project.html" 
    github_url: "https://github.com/elliott-king/resume-compare"
  - image_path: assets/images/fitness_small.png
    alt: "E-com Fitness web application"
    title: "E-com Fitness web application"
    excerpt: "A web-based application designed to forecast fitness product sales"
    btn_label: "Visit"
    btn_class: "btn--primary"
    url: "https://ecomfit.herokuapp.com/"
    github_url: "https://github.com/astoria-tech/bill-tracker"

projects_row2:
  - image_path: assets/images/phds_cover_img.png
    alt: "Pattern formation in Reaction-Diffusion systems"
    title: "Pattern formation in Reaction-Diffusion systems"
    excerpt: "Simulations of pattern formation in Chemicla/biological complex system."
    btn_label: "Visit"
    btn_class: "btn--primary"
    url: "/projects/phds"
    github_url: "https://github.com/elliott-king/freedom-js-app"
  - image_path: assets/images/random_cover.png
    alt: "Simulation of heat & mass transfer in porous materials"
    title: "Simulation of heat & mass transfer in porous materials"
    excerpt: "Simulation of heat-mass transfer process to assist in design new porous materials, with potential use in energy-efficient products."
    btn_label: "Visit"
    btn_class: "btn--primary"
    url: "/projects/stoch_combustion"
    github_url: "https://github.com/elliott-king/creepy-tracker"
  - image_path: assets/images/mlayer_laser_cover.png
    alt: "Modeling solidification during metal additive manufacturing"
    title: "Modeling solidification during metal additive manufacturing"
    excerpt: "Simulation of solidification process of sintered powder Aluminum-based alloys."
    btn_label: "Visit"
    btn_class: "btn--primary"
    url: "/projects/laser"
    github_url: "https://github.com/elliott-king/drawful-1.5"

---

<link rel="stylesheet" href="/assets/styles/projects.css">
About me:
<h2 style="font-size:25px">About Me:</h2>
I have a PhD in Computational Physics from McGill University. I have 7 years of professional work experience in designing high-performance algorithms and deploying advanced statistical techniques to solve problems involving extremely large data sets. Moreover, as a Fellow at The Data Incubator I have learned additional skills that have further strengthened my abilities as a data scientist, including:  ML frameworks (Keras, TensorFlow, Scikit-learn), Spark (ML, SQL), Cloud Computing (AWS: S3, Redshift, EMR, EC2), SQL, Automated algorithm design as well as Business mindset.


## Projects
{% include project_row id="projects_row1" %}
{% include project_row id="projects_row2" %}
