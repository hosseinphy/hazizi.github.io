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
  - image_path: assets/images/fitness.png
    alt: "E-com Fitness web application"
    title: "E-com Fitness web application"
    excerpt: "A web-based application designed to forecast fitness product sales"
    btn_label: "Visit"
    btn_class: "btn--primary"
    url: "https://ecomfit.herokuapp.com/"
    github_url: "https://github.com/astoria-tech/bill-tracker"

projects_row2:
  - image_path: assets/images/project-screenshots/creepy-tracker.png
    alt: "Pattern formation in Reaction-Diffusion systems"
    title: "Pattern formation in Reaction-Diffusion systems"
    excerpt: "Simulations of pattern formation in Chemicla/biological complex system."
    btn_label: "Visit"
    btn_class: "btn--primary"
    url: "/projects/phds"
    github_url: "https://github.com/elliott-king/freedom-js-app"
  - image_path: assets/images/project-screenshots/freedom.png
    alt: "Simulation of heat & mass transfer in porous materials"
    title: "Simulation of heat & mass transfer in porous materials"
    excerpt: "Simulation of heat-mass transfer process to assist in design new porous materials, with potential use in energy-efficient products."
    btn_label: "Visit"
    btn_class: "btn--primary"
    url: "/projects/stoch_combustion"
    github_url: "https://github.com/elliott-king/creepy-tracker"
  - image_path: assets/images/project-screenshots/drawful.png
    alt: "Modeling solidification during metal additive manufacturing"
    title: "Modeling solidification during metal additive manufacturing"
    excerpt: "Simulation of solidification process of sintered powder Aluminum-based alloys."
    btn_label: "Visit"
    btn_class: "btn--primary"
    url: "/projects/laser"
    github_url: "https://github.com/elliott-king/drawful-1.5"

---

<link rel="stylesheet" href="/assets/styles/projects.css">


## Projects
{% include project_row id="projects_row1" %}
{% include project_row id="projects_row2" %}
