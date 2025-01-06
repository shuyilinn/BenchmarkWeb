---
#
# By default, content added below the "---" mark will appear in the home page
# between the top bar and the list of recent posts.
# To change the home page layout, edit the _layouts/home.html file.
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
#
layout: page
---

"NN4SysBench is a benchmark suite for neural network verification, incorporating applications from the domain of neural network for computer systems (NN4Sys). This suite includes verification benchmark for learned index, learned bloom filter, learned cardinality, learned Internet congestion control, learned adaptive bitrate, learned distributed system scheduler, which are six tasks that apply neural networks to solve traditional tasks for systems.


Results of different verifiers    *(Hover to zoom in for a closer look)*:

<style>
.zoom-image {
    transition: transform 0.3s ease;
}
.zoom-image:hover {
    transform: scale(1.45);
}
</style>

![Verification Results]({{ '/assets/graphs/verification_runtime_2.jpg' | relative_url }}){: .zoom-image}


## Applications

<div class="accordion">

{% include LearnedIndex.md %}
{% include LearnedBloomFilter.md %}
{% include LearnedCardinality.md %}
{% include LearnedInternetCongestionControl.md %}
{% include pensieve.md %}
{% include decima.md %}

</div>


<!-- ## Specifications -->


<!-- ####from cheng:
Introduction for each app
description
paper
NN(link to our folder)
brief description of NN
input, output, sepcification
performance of verifier(number)

After Summary: 1 figure of result of difference verifier -->



