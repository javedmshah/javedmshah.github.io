---
layout: frontpage
title: Game theory and Learning
---

<div class="navbar">
  <div class="navbar-inner">
      <ul class="nav">
          <li><a href="bots.html">prev</a></li>          
          <li><a href="{{ BASE_PATH }}/jshah-public.pdf">cv</a></li>
          <li><a href="https://github.com/javedmshah">github</a></li>
          <li><a href="https://linkedin.com/in/javedmaqboolshah">LinkedIn</a></li>
          <li><a href="emotion_agency.html">next</a></li>          
      </ul>
  </div>
</div>

#### Game theory for feature analysis in learning models
***working paper*** <br>
The research is in early stages, but focuses on using a zero-sum game for calculating payoff matrices for pairwise feature analysis. We try to derive how each 'player' (in this case, each feature of a dataset) competes or cooperates with others to achieve a goal, such as explaining variance in the data.<br> A payoff matrix is built using a decision tree classifier with 10-fold cross validation on pairs of features selected from the dataset that have potential to occur in pairs. Mean classification accuracy scores are used to build the payoff matrices. <br>

***Approach*** <br>
Compute the payoff matrix using classification accuracy between pairs of features from the dataset. Create a game using the nashpy library and find Nash Equilibria. Plot the payoff matrices, showing how each feature pair's classification accuracy (payoff) relates to each other. Visualize feature pair classification accuracy as a heatmap for a more intuitive understanding of how well each pair performs.
Plot the first Nash Equilibrium (if one exists), illustrating the balance point where neither player ("feature") can benefit by unilaterally changing their strategy. We believe this carries some potential for determining a pairwise strategy for inclusion of said features for a learning model. <br>

<img src="payoffs.png" alt="glm" width="800"/>
**Payoff matrix using decision classifiers**. &mdash; <br>
The payoff matrix here represents how well each pair of features works together to classify the data. A higher score indicates a better combination for classification. The 'payoff' is quantified based on the contribution of each feature to this goal. To emphasize the game-theoretic nature of the problem, we visualize the payoff matrix and Nash Equilibrium, if we can find one. <br>

<img src="gt_feature_classes.png" alt="glm" width="800"/>
**Pairwise significance using classification accuracy heatmap**. &mdash; <br>
Feature pair classification accuracy is used as a heatmap gauging pairwise performance. Additionally, we plot the accuracies of each feature pair to understand their contributions better. The payoff for each feature in the sample dataset is based on how well it can classify or separate the data when combined with other features. The predictive power of this approach is yet to be quantified but we believe it holds potential using simple classification accuracy as a proxy to start with.<br>

<img src="nasheqbox.png" alt="glm" width="800"/>
**Nash equilibrium for feature pairing**. &mdash; <br>
We expect the application of game theory in factor analysis to be complex and context-dependent. These plots provide a visual and simplified understanding of how game theory might apply to feature selection or analysis in a dataset. Real-world testing is on the roadmap.<br>
