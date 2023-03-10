# Network Size and Green Technology Innovation

## Overview - Theory of Change & Research Question

As the world continues to see and feel the impacts of climate change, including urban smog, more frequent forest fires, rising ocean temperatures, and more frequent and stronger hurricanes, ensuring green technology innovation is as successful and as efficient as possible constitutes an increasingly high priority. Our group was interested in how the geographic dispersal of researchers affected this efficiency. Empirical evidence from previous studies has borne out that the number of patents produced in a given place is directly correlated with population at increasing returns to scale. Researchers have theorized that these increasing returns are partially the result of the informal connections and interactions that larger metropolitan areas facilitate, as well as the thicker employment markets found there. Collaboration between academia and industry is likely also more easily facilitated in these areas in which industry actors are typically located.

**Articulated simply, our research question asks:** 

Does professional network size matter in innovation? 

## Dataset
- [StarMetrics Federal Reporter](https://federalreporter.nih.gov)
  Federal Grants data for the period 2010-2018
- [USPTO Patents View](https://patentsview.org)
  Federal Patents data for the period 2010-2020
- [US Census Bureau Cartographic Boundary Files](https://www.census.gov/geographies/mapping-files/time-series/geo/carto-boundary-file.2014.html)
  Cartographic shapefile (2014) for map visualizations

## Methodology: Quantifying Innovation through Patents

Our outcome of interest is the number of patents produced within a given city as a function of the number of PIs (and associated researchers) and the dollar amount of grants received. Below are the steps followed in the study:

1. Identify Green Technology Grants
2. Link grants and patents on city level through Record Linkage
3. Visualize the results
4. Hypothesis Testing

<img width="932" alt="Screen Shot 2023-02-08 at 5 59 30 PM" src="https://user-images.githubusercontent.com/78453405/217702765-f2df3578-1544-4266-84fd-5822e661458d.png">

#### Some Definitions
- **Network:** The principle investigators & associated researchers located within a given city.
- **Grant Funding:** The amount of money awarded in grant funding to researchers for a given city,  measured in dollars.
- **Innovation:** The number of patents produced.

## Results

### 1: Green Technology Grants

We defined green technology with by applying the NLP model Latent Dirichlet Allocation (LDA), also known as topic modeling. We made all the abstracts go through the steps of stemming, lemmatization and vectorization and segregated them in 10 topics, that gave us following green-tech keywords from the entire corpus of words.

<img width="634" alt="Screen Shot 2023-02-08 at 6 39 08 PM" src="https://user-images.githubusercontent.com/78453405/217704177-67b4bc56-5842-45e3-a585-936a10b0224a.png">

Using the grant abstracts and the above keywords, we filtered our dataset for green grants.

This yielded 30,274 or 3.8% of all available grants. The grants are approximately uniformly distributed across 2010-2018.

### 2: Record Linkage of Grants and Patents

The grants are then linked via record linkage to the patents. Linkage is performed by matching any of the PI (primary or secondary) by their phonetic name and organization to the phonetic inventor name and assignee organization on the patents.

We used the New York State Identification and Intelligence System (NYSIIS) phonetic transformation, a commonly used rule-based algorithm.

Significant data munging was required to structure the secondary PIs for the join; ultimately we were able to expand the grant dataset so each row contained a unique PI and then later remove duplicates after the join. Matching on all PIs over just the primary resulted in approximately 400 additional matches.

Finally, we only considered patents that occur at least one year after the grant project start date. The final matching resulted in 1,417 grant-patent pairs. 

The three metrics are then summarized at the city level. 

The process diagram is as below: 

<img width="404" alt="Screen Shot 2023-02-08 at 6 39 33 PM" src="https://user-images.githubusercontent.com/78453405/217704333-a57f5716-f96b-4c88-b393-6e9cf7c5ff78.png">

### 3. Visualizations of the Results

From our initial results, we found that there are a high number of PIs concentrated mainly in the East Coast, Midwest and West Coast (refer Fig 2 below). However, we also found a fair amount of PIs in states such as Texas, Minnesota, Colorado etc., likely due to the presence of large state universities in these areas.

The trend for funding towards green technology research (refer Fig 3 below) follows a similar pattern i.e, highest where the most no. of PIs are concentrated. But we also found large amounts of funding in places having small no. of PIs, suggesting that the correlation between no. of PIs and amount of green funding may not be the strongest.

<img width="1293" alt="Screen Shot 2023-02-08 at 6 40 55 PM" src="https://user-images.githubusercontent.com/78453405/217704714-e1f602f8-df72-4948-b26b-e195d66b6119.png">

However, most green grants were found to have not been converted to patents, as can be seen below. This is explained by the fact that we found ~ 30,000 grants awarded to green tech research, however, only ~1400 were converted to patents.

<img width="855" alt="Screen Shot 2023-02-08 at 6 41 20 PM" src="https://user-images.githubusercontent.com/78453405/217705061-fb93b6f3-d504-4082-9b4b-1fca222b5963.png">

### 4. Verifying by Multivariate Regression Analysis

To answer our research question, we wish to understand not the geospatial relationship but the relationship between grant funding, number of PIs, and number of patents. We find this relationship by applying multivariate regression analysis. 

#### More PIs, More Patents (Fig 5 below)

- More PIs in a city is slightly but positively correlated with the number of patents
- Does not account for city population and density
- CT researchers may not think of NJ researchers as part of their network

#### More Grants $, More Patents (Fig 6 below)

- More grant money is also associated with more patents produced.
- Multivariate regression indicates that both n PIs and grant $ are positively associated with additional patents -- however effect size is small

<img width="986" alt="Screen Shot 2023-02-08 at 6 42 02 PM" src="https://user-images.githubusercontent.com/78453405/217705195-8967f11b-f4c6-4a04-a328-c732d5108d0b.png">

The multivariate regression including all three variables confirms the relationship. The number of PIs and the grant cost are both positively and significantly associated with the total patents produced in a city. 

<img width="1014" alt="Screen Shot 2023-02-08 at 6 42 25 PM" src="https://user-images.githubusercontent.com/78453405/217705527-fb67d72c-7ae6-4e1a-9562-8d6d4f3f4a42.png">

Despite the weak effect size, evidenced by the small coefficient estimates, we believe these results support our theory of change. A larger PI network is associated with a greater number of patents produced, holding grant funding constant.

## Policy Implications

Our findings suggest that in order to spur as much innovation as possible, grants should be awarded to researchers located within larger networks. Grant-making institutions should possibly reexamine their funding criteria to take network size into account when deciding which researchers and projects to give funding to. 

In addition to revisions to funding criteria, further policy implications can be inferred for research university systems. While the locations of research universities’ main campuses and the locations of other research entities are likely fairly sticky, decisions about where to open satellite campuses and locations should likely factor in these findings. 

One last policy implication of our results is a question of equity. In order to avoid concentration of research and education in areas with larger networks to the detriment of areas with smaller networks, programs need to be in place to spread the wealth. One such program is EPSCoR, Established Program to Stimulate Competitive Research, which “enhances research competitiveness of targeted jurisdictions… by strengthening STEM capacity and capability”. EPSCoR funds research and development in STEM fields in areas across the country that have historically received less financial support. More programs like EPSCoR that have a broader focus would prove beneficial in terms of equity for areas with smaller networks. 


