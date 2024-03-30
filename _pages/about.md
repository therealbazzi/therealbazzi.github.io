---
permalink: /
title: "Ahmad Bazzi - Research Scientist"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

Ahmad Bazzi was born in Abu Dhabi, United Arab Emirates. He received his PhD degree in electrical engineering from [EURECOM](https://www.eurecom.fr/en), Sophia Antipolis, France, in 2017, and the MSc degree (summa cum laude) in wireless communication systems (SAR) from Centrale Supélec, in 2014. He is currently a Research Scientist at the [Wireless Research Lab](https://wp.nyu.edu/wirelesslab/) of New York University (NYU) Abu Dhabi, and NYU WIRELESS, NYU Tandon School of Engineering, contributing to integrated sensing and communications (ISAC). Prior to that, he was the Algorithm and Signal Processing Team Leader at CEVA-DSP, Sophia Antipolis, leading the work on Wi-Fi (802.11ax) and Bluetooth (5.xx BR/BLE/BTDM/LR) high-performant (HP) PHY modems, OFDMA MAC schedulers, and RF-related issues. He is an inventor with multiple patents involving intellectual property of [Wi-Fi](https://en.wikipedia.org/wiki/Wi-Fi) and [Bluetooth](https://en.wikipedia.org/wiki/Bluetooth) products, all of which have been implemented and sold to key clients.

Since 2018, he has been publishing lectures on the YouTube platform under his name "[Ahmad Bazzi](https://www.youtube.com/channel/UCgC1d4JZ1Fz4t8MWLJD464w)", where his channel contains mathematical, algorithmic, and programming topics, with over 285,000 subscribers and more than 17 million views, as of January 2024. He was awarded a [CIFRE](https://www.enseignementsup-recherche.gouv.fr/fr/les-cifre-46510) Scholarship from Association Nationale Recherche Technologies ([ANRT](https://www.anrt.asso.fr/)) France, in 2014, in collaboration with RivieraWaves (now CEVA-DSP). He was nominated for Best Student Paper Award at IEEE International Conference on Acoustics, Speech, and Signal Processing (ICASSP) 2016. He received the Silver Plate Creator Award from YouTube, in 2022, for his 100,000 subscriber milestone. He was awarded an exemplary reviewer for the IEEE Transactions on Communications in 2022 and an exemplary reviewer for the IEEE Wireless Communications Letters in 2022. He served as technical program committee (TPC) member and a reviewer for many leading international conferences. He was selected amongst top 200 Top Arab creators for 2023. His research interests include signal processing, wireless communications, statistics, and optimization.

A data-driven personal website
======
Like many other Jekyll-based GitHub Pages templates, academicpages makes you separate the website's content from its form. The content & metadata of your website are in structured markdown files, while various other files constitute the theme, specifying how to transform that content & metadata into HTML pages. You keep these various markdown (.md), YAML (.yml), HTML, and CSS files in a public GitHub repository. Each time you commit and push an update to the repository, the [GitHub pages](https://pages.github.com/) service creates static HTML pages based on these files, which are hosted on GitHub's servers free of charge.

Many of the features of dynamic content management systems (like Wordpress) can be achieved in this fashion, using a fraction of the computational resources and with far less vulnerability to hacking and DDoSing. You can also modify the theme to your heart's content without touching the content of your site. If you get to a point where you've broken something in Jekyll/HTML/CSS beyond repair, your markdown files describing your talks, publications, etc. are safe. You can rollback the changes or even delete the repository and start over -- just be sure to save the markdown files! Finally, you can also write scripts that process the structured data on the site, such as [this one](https://github.com/academicpages/academicpages.github.io/blob/master/talkmap.ipynb) that analyzes metadata in pages about talks to display [a map of every location you've given a talk](https://academicpages.github.io/talkmap.html).

Getting started
======
1. Register a GitHub account if you don't have one and confirm your e-mail (required!)
1. Fork [this repository](https://github.com/academicpages/academicpages.github.io) by clicking the "fork" button in the top right. 
1. Go to the repository's settings (rightmost item in the tabs that start with "Code", should be below "Unwatch"). Rename the repository "[your GitHub username].github.io", which will also be your website's URL.
1. Set site-wide configuration and create content & metadata (see below -- also see [this set of diffs](http://archive.is/3TPas) showing what files were changed to set up [an example site](https://getorg-testacct.github.io) for a user with the username "getorg-testacct")
1. Upload any files (like PDFs, .zip files, etc.) to the files/ directory. They will appear at https://[your GitHub username].github.io/files/example.pdf.  
1. Check status by going to the repository settings, in the "GitHub pages" section

Site-wide configuration
------
The main configuration file for the site is in the base directory in [_config.yml](https://github.com/academicpages/academicpages.github.io/blob/master/_config.yml), which defines the content in the sidebars and other site-wide features. You will need to replace the default variables with ones about yourself and your site's github repository. The configuration file for the top menu is in [_data/navigation.yml](https://github.com/academicpages/academicpages.github.io/blob/master/_data/navigation.yml). For example, if you don't have a portfolio or blog posts, you can remove those items from that navigation.yml file to remove them from the header. 

Create content & metadata
------
For site content, there is one markdown file for each type of content, which are stored in directories like _publications, _talks, _posts, _teaching, or _pages. For example, each talk is a markdown file in the [_talks directory](https://github.com/academicpages/academicpages.github.io/tree/master/_talks). At the top of each markdown file is structured data in YAML about the talk, which the theme will parse to do lots of cool stuff. The same structured data about a talk is used to generate the list of talks on the [Talks page](https://academicpages.github.io/talks), each [individual page](https://academicpages.github.io/talks/2012-03-01-talk-1) for specific talks, the talks section for the [CV page](https://academicpages.github.io/cv), and the [map of places you've given a talk](https://academicpages.github.io/talkmap.html) (if you run this [python file](https://github.com/academicpages/academicpages.github.io/blob/master/talkmap.py) or [Jupyter notebook](https://github.com/academicpages/academicpages.github.io/blob/master/talkmap.ipynb), which creates the HTML for the map based on the contents of the _talks directory).

**Markdown generator**

I have also created [a set of Jupyter notebooks](https://github.com/academicpages/academicpages.github.io/tree/master/markdown_generator
) that converts a CSV containing structured data about talks or presentations into individual markdown files that will be properly formatted for the academicpages template. The sample CSVs in that directory are the ones I used to create my own personal website at stuartgeiger.com. My usual workflow is that I keep a spreadsheet of my publications and talks, then run the code in these notebooks to generate the markdown files, then commit and push them to the GitHub repository.

How to edit your site's GitHub repository
------
Many people use a git client to create files on their local computer and then push them to GitHub's servers. If you are not familiar with git, you can directly edit these configuration and markdown files directly in the github.com interface. Navigate to a file (like [this one](https://github.com/academicpages/academicpages.github.io/blob/master/_talks/2012-03-01-talk-1.md) and click the pencil icon in the top right of the content preview (to the right of the "Raw | Blame | History" buttons). You can delete a file by clicking the trashcan icon to the right of the pencil icon. You can also create new files or upload files by navigating to a directory and clicking the "Create new file" or "Upload files" buttons. 

<!-- Example: editing a markdown file for a talk
![Editing a markdown file for a talk](/images/editing-talk.png)
I am taking students to be co-advised with faculty members.

# News
* <b>CVL</b> is accepted to CoRL 2023 as a poster <a href="https://openreview.net/forum?id=oqOfLP6bJy">[Paper]</a>.
* <b>Accelerating exploration and representation learning with offline pre-training</b> is accepted to ICML 2023 as a workshop poster <a href="https://arxiv.org/abs/2304.00046">[Paper]</a>.
* <b>Learning About Progress From Experts</b> is accepted to ICLR 2023 as a spotlight (top 25%) <a href="https://openreview.net/pdf?id=sKc6fgce1zs">[Paper]</a>.
* I started at the MLR team at Apple as a Research Scientist.
* <b>CVL</b> is accepted to NeurIPS 2022 Deep RL workshop <a href="https://arxiv.org/abs/2211.02100">[Paper]</a>.
* <b>GSF</b> is accepted to NeurIPS 2022 as a poster <a href="https://arxiv.org/abs/2111.14629">[Paper]</a>.
* <b>Low-Rank Representation of Reinforcement Learning Policies</b> is accepted to JAIR <a href="https://arxiv.org/abs/2002.02863">[Paper]</a>.
* <b>Sequential Density Estimation via Nonlinear Continuous Weighted Finite Automata</b> is accepted to LearnAut 2022 <a href="/files/learnaut_2022_Sequential_Density_Estimation_via_Nonlinear_Continuous_Weighted_Finite_Automata.pdf">[Paper]</a>.
* <b>Short-Horizon Policy Iteration</b> (jointly with Microsoft Research) is accepted to ECML-PKDD 2022. <a href="https://arxiv.org/abs/2106.00589">[Paper]</a>.
* Our generalization quantification toolbox (jointly with Microsoft Research) is out. <a href="https://github.com/microsoft/segar">[Link]</a>.
* <b>CTRL</b> is accepted to ICLR 2022 as poster. <a href="https://arxiv.org/abs/2106.02193">[Paper]</a>.
* I am teaching the <i>COMP 424: Artificial Intelligence</i> class at McGill University during the Winter 2022 term. <a href="https://www.mcgill.ca/study/2021-2022/courses/comp-424">[Link]</a>. 
* <b>GSF</b> is accepted to NeurIPS 2021 Offline RL workshop as poster. <a href="https://arxiv.org/abs/2111.14629">[Paper]</a>.
* I am teaching the <i>BINF 7105: Méthodes statistiques en bioinformatique</i> class at UQAM University during the Fall 2021 term. <a href="http://info.uqam.ca/plan_cours/Automne%202021/BIF7105.html">[Link]</a>. 
* Our COVID-19 phylogenetic analysis is accepted to <i>BMC Ecology and Evolution<i>. <a href="https://link.springer.com/article/10.1186/s12862-020-01732-2">[Paper]</a>.
* <b>NTK-CL</b> is accepted to AISTATS 2021 as a poster. <a href="https://proceedings.mlr.press/v130/doan21a.html">[Paper]</a><a href="https://www.youtube.com/watch?v=iUlOxliPqfE">[Talk]</a>.
* <b>DRIML</b> is accepted to NeurIPS 2020 as poster. <a href="https://arxiv.org/abs/2006.07217">[Paper]</a> <a href="https://bmazoure.github.io/posts/deep-rl-infomax-learning/">[Blog]</a> <a href="/files/driml/DRIML_poster_(NeurIPS2020).pdf">[Poster]</a>.
* <b>UQF</b> is accepted to AISTATS 2020 as a poster. <a href="https://proceedings.mlr.press/v108/li20h.html">[Paper]</a><a href="https://aistats2020.org/poster_922.html">[Poster]</a>.


# About me

I am currently a Research Scientist at the Machine Learning Research team at Apple, working with Josh Susskind, Walter Talbott and Devon Hjelm on fundamental problems of representation learning for sequential decision making tasks.

I recently defended my PhD at the Montreal Institute for Learning Algorithms (MILA) and McGill University, co-supervised by [Devon Hjelm](https://scholar.google.ca/citations?user=68c5HfwAAAAJ&hl=en) and [Doina Precup](https://scholar.google.ca/citations?user=j54VcVEAAAAJ&hl=en). My research interests include deep reinforcement learning, probabilistic modeling, variational inference and representation learning.

I also was a research intern at DeepMind, working with Ankit Anand, Jake Bruce and Rob Fergus on unsupervised pre-training of state representations for efficient RL finetuning.

In the summer of 2021, I was interning in the Robotics team at Google Brain, with [Jonathan Tompson](https://jonathantompson.github.io/) and [Ofir Nachum](https://research.google/people/105364/), working on using self-supervised learning to improve generalization capabilities of offline RL agents.
I was a research intern at Microsoft Research, New York in the reinforcement learning team during summer 2020, working on counterfactual evaluation in contextual bandits. Previously, I was a research intern at Microsoft Research Montreal in the reinforcement learning team during summer 2019. I was also a research intern at Nuance during the summer of 2018 where I collaborated with [Atta Norouzian](https://scholar.google.ca/citations?user=KRPMXqYAAAAJ&hl=en). My work there focused on modeling acoustic signals such as speech with deep neural architectures.

I have completed my Master's in Statistics at McGill University under the supervision of [Johanna Neslehova](http://www.math.mcgill.ca/neslehova/). My thesis focused on reconstructing graphical models from discrete data with variational inference and multiarmed bandits. It can be found here: [link](https://bmazoure.github.io/files/thesis_Msc_2018.pdf). Before that, I obtained a Bachelor's in Computer Science and Statistics in 2017 from McGill University.



# Research interests

* Deep reinforcement and representation learning;

* High-dimensional statistics and optimization;

* Parametric and non-parametric Bayesian methods, approximate inference;

* Probabilistic graphical models;

* Generative models and density estimation.

# Work
* **Student Researcher** (Now)
  *Google Brain*
* **Research intern** (Summer 2021)
  *Google Brain*
* **Researcher** (2020-2021)
  *Microsoft Research*
* **Research intern** (Summer 2020)
  *Microsoft Research (NYC)*
* **Research intern** (Summer 2019)
  *Microsoft Research (Montreal)*
* **Research intern** (Summer 2018)
  *Nuance* -->

# Education

🎓 **PhD in Electrical Engineering** (2014-2017)
  *EURECOM / Communication Systems*

🎓 **MSc in Electrical Engineering (Wireless Communications)** (2013-2014)
  *CentraleSupélec*

🎓 **BSc in Electrical and Computer Engineering** (2009-2014)
  *Lebanese University, Faculty of Engineering III*