# Week 1: Introducing Recommender Systems

## Preferences and Ratings<br>
- Explicit: Just ask the users what they think! e.g. rating, review, vote;
- Implicit: user action is for some other purpose, not expressing preference. e.g. Click, Purchase, Follow;

## Predictions and Recommendations <br>
**Predictions** estimates of how much you’ll like an item<br>
- Often scaled to match some rating scale;<br>
- Often tied to search or browsing for specific products;<br>
- Pro: helps quantify item;<br>
- Con: provides something falsifiable;<br>

**Recommendations** are suggestions for items you might like (or might fit what you’re doing)<br>
- Often presented in the form of “top-n lists”;<br>
- Also sometimes just placed in front of you;<br>
- Pro: provides good choices as a default;<br>
- Con: if perceived as top-n, can result in failure to explore (if top few seem poor);

## Taxinomy of Recommenders & Major Recommendation Algorithms <br>
### 1. Non-personalized summary stats
- External community data: best seller, most popular, trending hot;
- Summary of community ratings: best liked
- Examples: Zagat restaurant ratings; Billboard music rankings; TripAdvisor hotel ratings;

### 2. Content-Based Filtering: Information Filtering, Knowledge-Based
- User Ratings x Item Attributes => Model (applied to new items via attributes)
- Examples: Personalized news feeds and Artist or Genre music feeds
- Alternative: knowledge-based, Item attributes form model of item space - Users navigate/browse that space

### 3. Personallized Collaborative Filtering <br>
- Use opinions of others to predict/recommend
- Sparse matrix: User model w/ ratings vs Item model w/ratings
  - Fill in missing values (predict)
  - Select promising cells (recommend)
- techniques: 
  - User-user: select neighborhood of similar-taste people and use their opinions
  - Item-item: pre-compute similarity among items via ratings, use own ratings to triangulate for recommendations
  - Dimensionality reduction: compress and use taste representation:  yields a lower-d matrix
  
### Model elements and evaluation metrics 
- Basic model elements: Users, Items, Ratings, and Community (optional) <br>
User (demographics) -------> Ratings <------- Items (properties, genres, etc.)
- Choose evaluation metrics
  - Accuracy of prediction
  - Usefulness of recommendations: correct, non-obvious and diverse
  - Computational expense


### Examples Movielens, Amazon 
