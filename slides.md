# The Director’s Signature: Computational and Historical Perspectives on Theatrical Stylometry

<!-- .slide: data-background-video="assets/vis_fondly_phalp_coco.mp4" -->
<!-- .slide: data-background-size="contain" -->
<!-- .slide: data-background-video-loop -->
<!-- .slide: class="main-title" -->


---


## The Team

<div class="headshots">

![Michael Rau](assets/people/michael_rau.jpeg) Michael Rau

![Peter Broadwell](assets/people/peter_broadwell.jpeg) Peter Broadwell

![Simon Wiles](assets/people/simon_wiles.jpeg) Simon Wiles

![Vijoy Abraham](assets/people/vijoy_abraham.jpeg) Vijoy Abraham

</div>

<div class="logos">

![TAPS](assets/logos/taps.png)
![SUL](assets/logos/Stanford-University-Libraries-stacked-wht.png)

</div>

:::

Thank you for joining us today.

We'll be discussing our exploratory work bringing Machine Learning techniques to the study of theater performance and directorial style.

The project, Machine Intelligence for Motion Exegesis, or MIME, is a collaboration between myself, Assistant Professor Michael Rau in Stanford's Theater and Performance Studies department, and the Developer Team at Research Data Services at Stanford University Library: Vijoy Abraham, Peter Broadwell and Simon Wiles.


---


## ➡️ &nbsp; The Problem: Understanding Pose in Theater <!-- .element: class="fragment custom order-of-sections" -->


## ➡️ &nbsp; Methodology: Models and Tools <!-- .element: class="fragment custom order-of-sections" -->


## ➡️ &nbsp; The MIME Platform <!-- .element: class="fragment custom order-of-sections" -->


## ➡️ &nbsp; Results and Analysis <!-- .element: class="fragment custom order-of-sections" -->


## ➡️ &nbsp; Implications and Complications <!-- .element: class="fragment custom order-of-sections" -->

<!-- .slide: class="order-of-sections" -->

:::
Our talk has six sections: first I'll discuss the problem we're solving, then Peter will give a technical overview, Simon will discuss the platform, and the bulk of our talk will focus on different analyses our platform has enabled on theatrical performance, and I'll end with some thoughts about the future of this work.

---


# The Problem

:::
Pose is fundamental to theater. Pose and staging lie at the intersection of authorial intent and directorial vision, pose is shaped by design choices of the costumes, set and lights and mediated by the performer's body. In traditional theater studies, pose is often taken for granted. Directors, performers and audiences intuitively understand the power of well-crafted tableaux or precisely choreographed movement sequences. Certain iconic poses define productions: Brecht's silent scream choreography in Mother Courage, Bob Fosse's shoulder rolls and arm pops in The Pajama Game, or the ensemble poses in "A Chorus Line." These indelible poses make work memorable and serve as shorthand for identifying directorial style. Examining pose in theater is challenging since it sits at the heart of artistic expression and is so fundamental it's often ignored. Our research addresses one major question: How can we quantify and analyze actors' physical arrangements and movements to reveal meaningful insights about the director's creative contribution?

---


## The Problem (and Opportunity)

<div class="screenshots">

![Michael Hampe](assets/results/Hampe-Karajan_nopose.png)

![Romeo Castellucci](assets/results/Castellucci-DG_nopose.png)

![Erik Söderblom](assets/results/Soderblom-Helsinki_nopose.png)

![Sven-Eric Bechtolf](assets/results/Bechtolf-Zurich_nopose.png)

![Damiano Michieletto](assets/results/Michieletto-La-Fenice_nopose.png)

![Jean-François Sivadier](assets/results/Sivadier-Aix_nopose.png)

</div>

<!-- .slide: data-transition="slide-in fade-out" -->

:::
To answer this question, we turned to computer vision algorithms to precisely detect actor poses for every frame of an archival theatrical production. Our methodology runs pose detection on numerous videos, generating hundreds of thousands of poses, then sifts through that data to draw meaningful conclusions. Our work doesn't just focus on one meaningful pose or tableaux but instead seeks to understand the aggregate effect of all poses throughout a production, and across multiple productions by the same director or different interpretations by different directors. This brings us closer to identifying the director's contribution to pose in theater.


---


## The Problem (and Opportunity)

<div class="screenshots">

![Michael Hampe](assets/results/Hampe-Karajan.png)

![Romeo Castellucci](assets/results/Castellucci-DG.png)

![Erik Söderblom](assets/results/Soderblom-Helsinki.png)

![Sven-Eric Bechtolf](assets/results/Bechtolf-Zurich.png)

![Damiano Michieletto](assets/results/Michieletto-La-Fenice.png)

![Jean-François Sivadier](assets/results/Sivadier-Aix.png)

</div>

<!-- .slide: data-transition="fade-in slide-out" -->

:::
By leveraging pose estimation and action recognition, we can quantify theatrical performance aspects previously left to subjective interpretation. We analyze not just individual poses, but movement patterns, spatial relationships between performers, and production rhythm and flow. We can use pose analysis to distinguish between different directors' work, regardless of actors, text, or designers, getting closer to understanding specific directorial contributions.


I'll hand it over to Peter to discuss our methodology.

---


# Methodology


---


## Temporal-Convolutional vs. Transformer Models

<div class="img-row">

![OpenPifPaf not doing well](assets/methods/OpenPifPaf_bad.jpg "OpenPifPaf not doing well") <strong>Open PifPaf</strong><br> Temporal-convolutional<br>2D only, limited tracking

![PHALP doing well](assets/methods/PHALP_WiLoR_good.png "PHALP and WiLoR doing well") <strong>PHALP</strong> (pose) + <strong>WiLoR</strong> (hands)<br>Transformers-based<br>3D, more robust to occlusion

</div>

:::
As Michael mentioned, this project works with moving images recorded on standard 2D "monocular" cameras. This opens up basically the entire history of theater on film for analysis, but it can be quite challenging to get sufficient accurate pose data from such "in the wild" live stage or studio recordings, due to multiple camera angles, panning, cuts, occlusion, shadows and so forth.

The first convolutional neural network-based pose estimation tools, such as OpenPose circa 2018, were revolutionary, but even after some further refinements, they still really struggled with in-the-wild videos such as the example shown on the left and are even more limited at estimating 3D coordinates and tracking multiple people in a shot.

As sometimes happens during this current era of AI research, a better model came along just in time, with a new generation of transformer-based models for computer vision, and more specifically via some great software tools for pose estimation and tracking from a research group at UC Berkeley.


---


## The Models Continue to Improve

![Meta's SAM 3D Body](assets/methods/SAM3D_Body.png "Meta's SAM 3D Body model") <strong>Meta's SAM 3D Body</strong><br> Infers "Momentum Human Rig" (HMR) - rigid skeletons and volumetric meshes

:::
The reward for procrastination -- eventually a better model comes along.


---


## PHALP: Predicting Human Appearance, Location and Pose

<img class="r-stretch" src="assets/methods/phalp_teaser.png" />

Jathushan Rajasegaran, Georgios Pavlakos, Angjoo Kanazawa, Jitendra Malik. “Tracking People by Predicting 3D Appearance, Location & Pose.” arxiv.org/abs/2112.04477 (2021).  
https://github.com/broadwell/PHALP

:::
The most crucial of these tools is named PHALP -- you can see the acronym there -- and it achieves state-of-the-art accuracy in pose estimation by interweaving the tasks of estimating human forms while also noting their appearance (that is, by extracting texture maps of their clothing and such) and tracking their trajectories over time in an estimated 3D space. This enables the transformer-based system to fill in occluded limbs and even entire poses that earlier models would "lose track of" for multiple frames before finding them again.


---


## LART: Lagrangian Action Recognition with Tracking

<img class="r-stretch" src="assets/methods/LART.png" />

Jathushan Rajasegaran, Georgios Pavlakos, Angjoo Kanazawa, Christoph Feichtenhofer, Jitendra Malik. “On the Benefits of 3D Pose and Tracking for Human Action Recognition.” arxiv.org/abs/2304.01199 (2023).  
https://github.com/broadwell/LART

:::
We augmented the 3D pose data from PHALP with a customized action recognition tool built by the same team, named Lagrangian Action Recognition with Transformers. This software also produces a 60-element vector in the AVA "Atomic Visual Actions" embedding space to describe every detected action inferred for every pose in every frame.


---


## Probabilistic View-Invariant (2D+) Pose Embeddings

<img class="r-stretch" src="assets/methods/view-invariant_embeddings.jpg" />

Sun, Jennifer J, Jiaping Zhao, Liang-Chieh Chen, Florian Schroff, Hartwig Adam and Ting Liu. “View-Invariant Probabilistic Embedding for Human Pose.” In Proceedings of the European Conference on Computer Vision, Springer, 2020, pp. 53-70.  
https://sites.google.com/view/pr-vipe

:::
Finally we adopted another embedding, this one from Google and CalTech, that projects the 2D coordinates of a pose into a 16-dimension space that situates poses closer together if they are probably similar in their actual 3D representations. Note that we also get the estimated 3D coordinates of the poses from PHALP, but as we'll see later, sometimes this probabilistic embedding is more useful for analysis.


---


# The MIME Platform

<div>&nbsp;</div>


### Pipeline → Database → API Server → Interfaces


:::

So how do we operationalize these models and techniques?  How do we take the inferences and predictions they generate and make them useful for exploring our research questions?

The MIME platform consists of a modular ingestion pipeline, a database with sophisticated vector storage and indexing capabilities, an application and API server, and a collection of related interfaces that allow us to investigate, analyze, and visualize the data we have assembled.

The loosely-coupled nature of the platform allows us to iterate on steps somewhat independently and experiment with different approaches while still providing a consistent framework for our development.

---


## Pipeline


<ul style="margin-top:2rem">
  <li><strong style="font-size:2rem">Inference Tasks</strong>
    <ul>
      <li>Pose Estimation (PHALP/4D-Humans)</li>
      <li>Action Estimation (LART)</li>
      <li>View-Invariant Embeddings (Pr-VIPE)</li>
      <li>Shot Detection (TransNetV2)</li> <!-- .element: class="fragment" -->
      <li>Face Recognition (ArcFace/DeepFace)</li> <!-- .element: class="fragment" -->
      <li>Hand Estimation (WiLoR)</li> <!-- .element: class="fragment" -->
    </ul><!-- .element: class="fragment" -->
  </li>


  <li style="margin-top:2rem"><strong style="font-size:2rem">Coordination Steps</strong>
    <ul>
      <li>coordination of hands and poses, calculating joint angles</li>
      <li>segmentation into movelets with in-place and sidereal motion</li><!-- .element: class="fragment" -->
      <li>calculation of pose and action interest, synchronous motion</li><!-- .element: class="fragment" -->
      <li>pregeneration of pose and face clusters</li><!-- .element: class="fragment" -->
    </ul> <!-- .element: class="fragment" -->
  </li><!-- .element: class="fragment" -->
</ul> <!-- .element: class="fragment" -->

:::

The pipeline is first and foremost about running the inference tasks.

In addition to the three core technologies that Peter already introduced our ingestion pipeline can also optionally perform Shot-Detection, Face Recognition, and Hand Estimation,

and once we have all this information we also need to perform a number of coordination tasks

these are tasks that are adjacent to the primary AI/ML inference tasks and which supplement and augment the raw pose estimation data.

---

<div>


## Database

* PostgreSQL / pgvector
* Multiple similarity metrics
* ANN Indexes (`IVFFlat`, `HNSW`)
</div>


<div style="margin-top: 2rem">


## Application / API Server

* Machine-Learning dependencies
* Full Data-Science stack
* Jupyter Notebook server <!-- .element: class="fragment" -->
* FastAPI server <!-- .element: class="fragment" -->


</div><!-- .element: class="fragment" -->

:::

These inference and computational tasks are lengthy and expensive, so all the data generated are stored in our database server for subsequent retrieval and analysis.  For our vector storage and querying capabilities we're using pgvector which offers a number of affordances for the performant ANN searches on which much of the functionality is built.


The Application and API server is a container that has all our machine-learning dependencies available and its where all our machine learning and back-end code runs

The container is also home to a Jupyter Notebook server and a FastAPI server that exposes the endpoints that are consumed by our web interface

---


# The MIME Platform

<section>
<div>

![Platform Diagram](assets/building/platform_diagram.svg)
<svg class="spotlight" viewBox="0 0 1080 300" preserveAspectRatio="none">
  <script type="application/json" class="spotlight-data">
  [
    {"x":"17px","y":"28px","height":"215px","width":"245px"},
    {"x":"295px","y":"8px","height":"143px","width":"459px"},
    {"x":"351px","y":"155px","height":"125px","width":"215px"},
    {"x":"629px","y":"155px","height":"125px","width":"150px"},
    {"x":"828px","y":"131px","height":"168px","width":"251px"},
    {"x":"772px","y":"18px","height":"92px","width":"295px"}
  ]
  </script>
  <defs>
    <mask id="spotlight-mask">
      <rect width="1080" height="300" fill="white" opacity=".6"/>
      <rect x="0" y="0" width="1080" height="300" fill="black"/>
    </mask>
  </defs>
  <rect width="1080" height="300" fill="#000" mask="url(#spotlight-mask)"/>
</svg>

</div>

:::

This diagram describes the platform architecture that delivers the flexibility we need

The whole thing is orchestrated with docker which makes maintaining it and working with it very convenient.

---


# Interfaces

:::
We don't have time for a live demonstration today, so instead I'll very quickly share some screenshots from some of the interface affordances we have available.

---

<img src="assets/interface/mime-mk1-timeline.png" >
<!-- .slide: data-transition="slide-in fade-out"-->

:::
This is a timeline view for a single performance that lets us see how our data are distributed along a temporal axis.

---

<img src="assets/interface/mime-mk1-pose-search.png">
<!-- .slide: data-transition="fade" -->

:::
This is our first iteration of a search interface that allows searching for similar poses or actions.

---

<img src="assets/interface/mime-mk1-frame-view.png">
<!-- .slide: data-transition="fade" -->

:::
Here is a full view of a single frame.

---

<img src="assets/interface/mime-mk1-face-clusters.png">
<!-- .slide: data-transition="fade" -->

:::
We have face clustering plotted along a time axis.

---

<div class="img-row">

![Visualization of 3D scene reconstruction](assets/interface/mime-3d-inference.png "A 3D scene reconstruction")

![MIME 3D pose visualization](assets/interface/mime-mk1-3d-scene-hands.png "A 3D scene reconstruction")

</div>

<!-- .slide: data-transition="fade" -->

:::
A 3D scene reconstruction

---

<img src="assets/interface/poseplot_r.gif">
<!-- .slide: data-transition="fade" -->

:::
This is an interactive 2D UMAP projection of poses clustered with the HDBSCAN algorithm.

We're using the visualization code here from pixplot, but the clustering and the projection are based not on the images but on the vector space that represents our pose estimation inference vectors.

---

<img src="assets/interface/corpus_search.gif">
<!-- .slide: data-transition="fade" -->

:::
Searching for a source pose from one recording across a corpus of recordings...

---

<img src="assets/interface/webcam_search.gif">
<!-- .slide: data-transition="fade-in slide-out" -->

:::
And finally here's yours truly performing a pose in front of a webcam and using that to search for poses.

Michael's now going to show us some of the ways he's been able to make use of these affordances in his work.

---


# Results & Analysis

---


## Recurring Poses and Thematic Pose Analysis

<video data-autoplay controls muted src="assets/Bausch4.mp4"></video>
:::
Using MIME's timeline, we can easily analyze a production in terms of repetetive gestures. A researcher can simply select a specific pose in the production, and the timeline will show where else the pose shows up in the performance. You can jump easily to those spots in the performance, or you use it chart certain thematic recurrances. The timeline view gives you a distant view of the performance, where you can see chart entrances and exits of performers, and as get a sense of some aspects rhythmic or thematic elements by noting what repeats within the performance and when.

---


## Corpus Studies: Assembling Multiple Works per Director

<img class="r-stretch" src="assets/results/31_performances.png" />

:::
To address the question of what the data we extract from recordings via the MIME platform can tell us about how theater directors produce specific effects in their own personal style, we focused on three high-profile, contemporary "auteur" directors: Bill T. Jones, Romeo Castellucci, and Krzysztof Warlikowski, selecting 10 or 11 performances each has directed. We ran video recordings of these performances through the MIME pipeline without alteration, other than upscaling some of them to at least HD quality, because the models work better with high-resolution footage.

As you can see, this produced 10-20 hours of pose data per director.


---


## Which Features Are Best for Differentiating between Directors?

<div class="img-row">

Pose motion and distance statistics
![Pose motion and distance confusion matrix](assets/results/LOO_motion_distance.png "Pose motion and distance confusion matrix")

View-invariant pose embeddings
![View-invariant pose embeddings confusion matrix](assets/results/LOO_POEM_features.png "View-invariant pose embeddings confusion matrix")

</div>

:::
We framed our approach as a performance-to-director classification problem, investigating which pose, action, motion and distance data elements are most effective at predicting the correct stage director for a given performance. The first steps was a basic "leave one out" test comparing the aggregated, averaged feature vectors across each director's entire collection to the average feature vector of one "held out" performance, using cosine similarity, in what's basically a very simple multidimensional kernel-based similarity comparison.

This approach found that the basic pose and motion statistics were not as effective at differentiating works by Castellucci and Warlikowski. However, they were quite good at telling the difference between Bill T. Jones and the other two directors. Meanwhile, the aggregated pose embeddings were more successful at differentiating the works of all three directors.


---


## Which Features Are Best for Differentiating between Directors?

<img class="r-stretch" src="assets/results/31_performances_hl.png" />

:::
Here we've highlighted the performances with greater amounts of motion. Most are from Bill T. Jones, who primarily creates dance works, while the other two directors tend to direct mostly operas and other more static forms of stage plays. So the motion and distance-based comparison may be better at picking up on the difference in primary genres between these directors. Meanwhile, the pose embedding approach seems to be picking up something distinctive about each director's individual style. We'll look into what that might be in just a minute.


---


## Which Features Are Best for Differentiating between Directors?

<div class="img-row">

Body keypoint coords (3D)
![3D coordinates confusion matrix](assets/results/LOO_3D_coords.png "3D coordinates confusion matrix")

Action recognition embeddings
![Action recognition embeddings confusion matrix](assets/results/LOO_action_features.png "Action recognition embeddings confusion matrix")

</div>

:::
Here are some further leave-one-out classification experiments with the 3D pose coordinates and action recognition vectors used as features.
The action recognition embeddings do seem to be somewhat better than the 3D coordinates for telling the directors apart.


---


## Which Features Are Best for Differentiating between Directors?

<img class="r-stretch" src="assets/results/classification_experiments.png" />

:::
Here are some results with slightly more sophisticated classification algorithms and using 10-fold cross-validation with different random seeds to try to get a better sense of how these approaches might perform with a larger, more diverse dataset. They do suggest that some algorithms are better at detecting some aspects of even the large-scale motion and distance data that differentiate directors, so that is worth exploring further, while the effectiveness of the embedding-based inputs does drop a bit when the training set is small.


---


## Feature Importances: Motion and Distance (Random Forest)

<div class="img-row">

![Motion and distance feature importances, Random Forest](assets/results/feature_importances_rf.png "Motion and distance feature importances, Random Forest") Permutation Importance

![Motion and distance feature importances, Random Forest (sorted)](assets/results/feature_importances_rf_sorted.png "Motion and distance feature importances, Random Forest") Mean Decrease in Impurity

</div>

---


## Collinearity of Motion and Distance Features

<p class="stretch"><img
  src="assets/results/feature_collinearity.png"
/></p>

---


## Feature Importances: View-Invariant Pose Embeddings

<div class="img-row">

![Pose embedding feature importances, Random Forest](assets/results/poem_feature_importances_nb.png "Pose embedding feature importances, Random Forest") Permutation Importance (Gaussian Naive Bayes)

![Pose embedding feature importances, Random Forest (sorted)](assets/results/poem_importances_rf.png "Pose embedding feature importances, Random Forest") Mean Decrease in Impurity (Random Forest)

</div>

---


## Collinearity of View-Invariant Pose Vector Features

<p class="stretch"><img
  src="assets/results/poem_vector_collinearity.png"
/></p>

---


## Visualizing Directors' Pose "Repertoires"

<img class="r-stretch" src="assets/results/poem_umap_sampled_2.png" />

:::
To explore how the directors' pose "repertoires" might be distributed through the view-invariant pose embedding space, and hopefully get a better sense of what aspects of these embeddings were helping to differentiate the directors, we plotted a sample of all of their pose embeddings into a 2D space via UMAP projection as color-coded dots. The larger hexagons represent each director's overall average pose embedding. Although we can't directly translate these average points into poses, we can search for the most similar poses to them from the entire data set thanks to MIME's powerful vector database, and we've shown some of those here in the callouts.

This projection does seem to reveal useful observations, like the overall greater similarity between Castellucci’s and Warlikowski’s pose repertoires relative to Jones’s, and the callouts highlight how Jones tends to employ dramatically contorted poses, Castellucci to favor hunched-over standing postures, and Warlikowski to deploy figures in an active sitting position.


---


## Hands and Delsarte

<div class="img-row">

Delsarte Pose
![Pose motion and distance feature importances](assets/results/delsarte_exercises.jpg "Poses from Delsarte Instruction Manual")

MIME Detection
![Hands inclusion](assets/results/Delsarte_results.png "Delsarte Comparison")

</div>

:::
One of the more recent developments that we've been working on with MIME is to take the 19th century pose system, invented by Francois Delsarte that has a long, influential and bizarre history, and to use those diagrams of poses that he invented and see where they showed up in our contemporary work. The delsarte system has a series of codified full-figure and hand poses, that express certain ideas and emotions and using the search function of MIME, we were able to identify precisely where and when certain actors would arrive in Delsarte poses. These results allowed us to create "Delsarte Thumbprints" to not only see which gestures are reminiscient of Delsarte's choreography, and to track the frequency through which they appear in a production.

---


## Delsarte Thumbprint

<div class="img-row">

Bill T Jones's Fondly Do We Hope
![Pose frequency throughout the work](assets/results/Fondly2.png "Poses from Delsarte Instruction Manual")

Romeo Castellucci's Democracy in America
![Hands inclusion](assets/results/Castellucci-Delsarte.png "Delsarte Comparison")

</div>

:::
Here you can see two different "thumbprints"--that demonstrate the the difference quantities of pose throughout the show. Bill T. Jones' production shows far more "Prostration" than Castellucci. And Castellucci's production features far more poses of supplication. And while it may seem a little silly to use these 19th century melodramatic poses to analize a works of contemporary theater, this method points towards ways in which this technology could be used to trace the genelogy of artistic movements, and the subtle ways that historical aesthetics shape our contemprary tastes.

---


## Delsarte Through the Years

<div class="img-row">


Ted Shawn: "Nobody Knows<br> the Trouble I've Seen" from his <br>_Four Dances Based on<br> American Folk Music_ in 1938
![Ted Shawn Dancing his Nobody Knows the Trouble I've Seen in 1938](assets/results/Shawn_1938.png "Ted Shawn Dancing his Nobody Knows the Trouble I've Seen in 1938")

Davon Rainey: <br>"Nobody Knows"<br> in 2016
![Davon Rainey Dancing Nobody Knows in 2016](assets/results/Shawn_Rainey_2016.png "Davon Rainey Dancing Nobody Knows in 2016")

</div>

:::
Added provisionally

---


## Delsarte Through the Years

<div class="img-row">

Plots of the prevalences of the Shawn/Delsarte "Reflection" pose archetype<br> in recordings of the two dances from the previous slides<br> (Ted Shawn dancing "Nobody Knows" in 1938, and Davon Rainey dancing the same in 2016).
![MIME pose prevalence charts](assets/results/Shawn_Nobody_MIME.png "MIME pose prevalence charts")

</div>

:::
Added provisionally

---


## Direct Comparison: Multiple Directors' Stagings of the Same Work

<div>

![Comparisons of performances of Don Giovanni](assets/results/dg_comparison_table.png "Comparisons of performances of Don Giovanni")

</div>

<div class="screenshots">

![Michael Hampe](assets/results/Hampe-Karajan.png) Michael Hampe

![Romeo Castellucci](assets/results/Castellucci-DG.png) Romeo Castellucci

![Erik Söderblom](assets/results/Soderblom-Helsinki.png) Erik Söderblom

</div>

:::


Our final analytical experiment to date, which is still a work in progress, sort of inverts the previous approach and instead considers what MIME can reveal when comparing staging from seven different directors who were all directing the same work -- in this case Mozart and Da Ponte's  Don Giovanni from 1787.

The screenshots below show some pose estimation output from each of the directors' stagings -- note that in every case this is the same scene, from the finale of Act I.

---


## Direct Comparison: Multiple Directors' Stagings of the Same Work

<div>

![Comparisons of performances of Don Giovanni](assets/results/dg_comparison_table.png "Comparisons of performances of Don Giovanni")

</div>

<div class="screenshots">

![Sven-Eric Bechtolf](assets/results/Bechtolf-Zurich.png) Sven-Eric Bechtolf

![Damiano Michieletto](assets/results/Michieletto-La-Fenice.png) Damiano Michieletto

![Jean-François Sivadier](assets/results/Sivadier-Aix.png) Jean-François Sivadier

</div>

:::
The table above gives derived statistics of the performances, highlighting entries with greater degrees of movement, distance between actors, and overall deviation from the average pose and actions. As the table is also ordered chronologically, it does seem to indicate a general tendency for performances to get more creative and/or "non-traditional" in their stagings over time, as quantified via pose and action estimation.


---


## Aligning Performances (by Music) to Get Average Pose "Consensus"

<img class="r-stretch"
  src="assets/methods/Don_Giovanni-Soderblom-Helsinki_UzxYEVbOS5w.mp4_chroma_time_correspondences.png"
/>


:::
Comparing the performances of Don Giovanni involved aligning all of them down to the sub-second level, specifically so that we could calculate the average poses and actions deployed at each moment of the opera -- building what folklorists refer to as the "consensus performance" or "tradition dominant" of a cultural expressive form -- and then compute the degree to which each director's staging deviates from this consensus at each moment.

Practically speaking, the easiest way to align the recordings, which only works because the work is an opera, is to extract the musical pitches heard at each timecode and apply the dynamic time warping algorithm to match the pitch chroma of different performances to compute a warping path that allows us to align them despite significant differences in tempo, non-musical action (e.g., intermission), and the occasional omission of certain scenes.


---


## Comparing Each Director's Staging to the "Consensus" Average

<div class="r-stack">
  <img
    src="assets/results/all_movement3d.png"
  />
  <img
    class="fragment"
    src="assets/results/consensus_all_movement3d.png"
  />
</div>

:::
As a final analytical output of the effort just described, we can plot the pose or motion similarities of each of the 7 performances to the average  "consensus" performance across the entire work (the dashed lines are scene and act boundaries). This is still a work in progress, but we can use this analysis to detect patterns such as certain scenes in which stagings are more likely to deviate from the consensus poses, and eventually use this to highlight automatically where directors might use especially distinctive poses and actions. Stay tuned...


---


# Implications

:::
To recap, using MIME, we can

Use pose similarity functions, to identify recurring poses, symmetry, and the rhythmic ebb and flow of staging. We can identify aggegrate stylistic elements that define a director's output, separating their unique contribution from performers' work or textual constraints. We can identify poses that make reference to historical movements and style and trace the evolution of a choreography. MIME also enables objective comparisons between different directors' interpretations, revealing new dimensions of artistic expression.

We can compare different directors' versions to show how physical expression and spatial storytelling evolve over time, across cultures, or in canonical works. Scholars could examine how themes or characters are represented physically—for instance, how kings are staged to show varying representations of power between productions.

This technology could chart how actors' physical choices evolve through rehearsals. Given the precision of the timeline view, we can correlate pose data with audience response—applause or laughter—to see which physical expressions elicit the strongest responses, deepening our understanding of audience engagement.

It creates an unprecedented record of a production's physical language—valuable for future research, teaching, or restaging. Beyond theater, this methodology could be adapted to film, opera, dance, and other movement-based arts. It could also apply to diverse fields from political speeches to sports biomechanics.

However, we must acknowledge ethical considerations and limitations. Like all AI, there's danger in incorrect pose estimations. Working with archival materials requires careful navigation—we've developed clear guidelines ensuring respectful, responsible use.

We must recognize the limitations of focusing solely on pose. Theater is multifaceted—pose is critical but represents only one thread in a rich tapestry including dialogue, set design, lighting, and sound. This analysis should complement, not replace, traditional artistic analysis methods.

This computational approach cannot definitively determine directorial intent. Observed patterns may stem from conscious choices, actor improvisations, or unintentional elements. These findings should serve as starting points for deeper investigations, not definitive conclusions.

While this research presents exciting quantitative analysis possibilities, its true value lies in complementing traditional scholarly approaches. By integrating computational methods with human interpretation, we develop a more comprehensive understanding of theatrical performance and directorial style, enriching both academic discourse and artistic practice.

Thank you.


---


# Complications

:::

Notes go here

---


# Thank You&#x21;

<div class="logos">

![TAPS](assets/logos/taps.png)
![SUL](assets/logos/Stanford-University-Libraries-stacked-wht.png)
![QR](assets/logos/mime-qr-code.svg)

</div>


---


# Appendix


---


## 3D Keypoint Importances (Random Forest)

<p class="stretch"><img
  src="assets/results/keypoint_importances_rf.png"
/></p>

---


## Collinearity of 3D Keypoint Coordinates

<p class="stretch"><img
  src="assets/results/keypoint_collinearity.png"
/></p>

---


## Pose "Repertoires" Visualization (Labeled Performances)

<p class="stretch"><img
  src="assets/results/poem_embedding_umap_labeled.png"
/></p>

---


## Action "Repertoires" Visualization

<p class="stretch"><img
  src="assets/results/ava_umap.png"
/></p>

---


## "Cursed" Frames (and Poses)

<div class="img-row">

![cursed_004863](assets/complications/cursed_004863.jpg)

![cursed_083450](assets/complications/cursed_083450.jpg)

![cursed_107925](assets/complications/cursed_107925.jpg)

</div>

:::

These are cursed.


---
