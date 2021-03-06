---
title: 'Primer: Recommender Systems'
---

The modern era of *recommender systems* (RS) research is largely considered to have begun in the mid 1990's with projects such as GroupLens {% cite resnick1994grouplens %} and Tapestry {% cite goldberg1992using %}. Since that time the field has seen rapid growth in terms of applications and techniques. An early and important survey in the field says that the defining characteristice establishing RS as its own field was the focus on user ratings of items {% cite adomavicius2005toward %}. More recently however, authors have tended to define the field simply as the study of statistical relationships between users and items {% cite shi2014collaborative %}, {% cite aggarwal2016recommender %}, {% cite bobadilla2013recommender %}, {% cite lu2012recommender %} and {% cite ricci2015recommender %}. This later definition creates room for important sub-topics within RS such as knowledge-based systems and association rules.

# Taxonomy of Techniques

Within the RS corpus there is relative agreement over the following taxonomy {% cite aggarwal2016recommender%}, {% cite ricci2015recommender %}:

 * Collaborative recommendation methods (aka, *collaborative filtering* (CF))
 * Content recommendation methods (aka, content-based recommendations)
 * Knowledge recommendation methods (aka, knowledge-based recommendations)
 * Hybrid recommendation methods

The primary characteristic distinguishing these methods is the ratings information assumed to be available to make a recommendation. Collaborative methods assume all observed ratings for all users and items are available. Content methods assume that all ratings are available either for a single user or a single item. Knowledge methods make no assumptions about ratings information and instead simply rely on comprehensive knowledge of their items to make recommendations.

Additionally, the duality of user-item ratings gives each method two interpretations:

<svg width="90%" height="90%" style="max-width:500px;" viewBox="0 0 500 320">

    <style>
	.header { font-weight: bold; }
    </style>
	
    <rect x="100" y="20" width="398" height="298" rx="5" stroke="black" fill="transparent" stroke-width="2"/>
    
    <path d="M 300 20  V 318" stroke="black"/>
    <path d="M 100 120 H 498" stroke="black"/>
    <path d="M 100 220 H 498" stroke="black"/>
    
    <text x="90" y="70" alignment-baseline="middle" text-anchor="end" class="header"> Collaborative </text>
    <text x="90" y="170" alignment-baseline="middle" text-anchor="end" class="header"> Content </text>
    <text x="90" y="270" alignment-baseline="middle" text-anchor="end" class="header"> Knowledge </text>
    
    <text x="200" y="13" text-anchor="middle" class="header"> User-Centric </text>
    <text x="400" y="13" text-anchor="middle" class="header"> Item-Centric </text>
    
    <text x="200" y="70" text-anchor="middle" alignment-baseline="middle"> Traditional CF </text>
    <text x="400" y="70" text-anchor="middle" alignment-baseline="middle"> Item-based CF </text>

    <text x="200" y="170" text-anchor="middle" alignment-baseline="middle"> Content-Based </text>
    <text x="200" y="185" text-anchor="middle" alignment-baseline="middle"> (assumes all user ratings) </text>
    
    <text x="400" y="170" text-anchor="middle" alignment-baseline="middle"> Demographic-Based </text>
    <text x="400" y="185" text-anchor="middle" alignment-baseline="middle"> (assumes all item ratings) </text>
    
    <text x="200" y="270" text-anchor="middle" alignment-baseline="middle"> ??? </text>
    <text x="400" y="270" text-anchor="middle" alignment-baseline="middle"> Constraint or Use-Case </text>

</svg> 

It is worth noting that the usage of "Demographic-Based" in the above image doesn't fit perfectly with the usage of the term within the literature. Nevertheless, we feel it is close in spirit and by that measure still helpful to place within our hierarchy.

Finally, one may notice that two common sub-categories have been left out above: (1) memory-based collaborative recommendations and model-based collaborative recommendations. While it is useful to be aware of these terms due to their usage within the literature, the terms themselves add nothing to our understanding of recommendation methods. If this were all then we'd probably keep them, however, including the terms also carries the very real risk of misleading new students. It is because of the risk of misleading while at the same time not providing any benefit that we remove them.

The terms themselves seem to be carried on primarily because of their historical usage (cf. {% cite adomavicius2005toward %} and {% cite breese1998empirical %}). Unfortunately, by only highlighting memory and model based approaches for CF it is implied that these distinctions don't exist for other methods or are somehow extra special for CF methods. However, this simply isn't the case, nor was it the argument of the original authors {% cite breese1998empirical %}. The original authors simply didn't consider methods of recommendation beyond CF when making these distinctions {% cite breese1998empirical %}. Furthermore, it is easy to show that many statistical estimation problems can be solved via both model-free (e.g., local regression) and model-based (e.g., ordinary least squares) approaches implying that there is nothing special about these approaches with CF methods.

# Considering Context

An open research question regarding RS is how to best incorporate context. Perhaps the most popular model for representing context in an RS is the *multidimensional* (MD) model {% cite aggarwal2016recommender%}, {% cite ricci2015recommender %}, {% cite adomavicius2005incorporating %} and {% cite adomavicius2011context %}. This model was originally proposed in {% cite adomavicius2001expert-driven %} with the refined version presented below developed in {% cite adomavicius2011context %}. The model is written as follows: \\[ r: U \times I \times C \to \mathbb{R}, \\] where \\( U \\) is the set of users, \\(I\\) is the set of items, \\(C\\) is the set of contexts and \\(r\\) is a function determining the rating. With this model the RS problem can be expressed as: *given a set of observations \\(O \subseteq U \times I \times C \times \mathbb{R} \\) determine \\(r\\)*. Many methods have been proposed to solve for \\(r\\) in the MD model: optimization {% cite oku2006context %}, matrix factorization {% cite karatzoglou2010multiverse %}, pre-filtering {% cite adomavicius2011context %} and {% cite adomavicius2005incorporating %}, post-filtering {% cite adomavicius2011context %} and {% cite panniello2009experimental %}, and reducing the MD model to the traditional \\(r: U \times I \to \mathbb{R}\\) by defining either \\(I \times C \mapsto IC \\) {% cite baltrunas2009context %} or \\(U \times C \mapsto UC \\) {% cite baltrunas2009towards %}.
