# MovieReccomendationSystem


This project implements a movie recommendation system using collaborative filtering techniques. It utilizes user-based collaborative filtering with cosine similarity and matrix factorization using Singular Value Decomposition (SVD) to make movie recommendations.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [Algorithms](#algorithms)
  - [Collaborative Filtering with Cosine Similarity](#1-collaborative-filtering-with-cosine-similarity)
  - [Singular Value Decomposition (SVD)](#2-singular-value-decomposition-svd)
- [Evaluation](#evaluation)
- [Dataset](#dataset)
- [License](#license)

## Installation

1. Clone the repository:
    ```bash
    git clone <your-repository-url>
    ```

2. Navigate to the project directory:
    ```bash
    cd movie-recommendation-system
    ```

3. Ensure that the dataset is available in the project directory as a `.zip` file (e.g., `ml-latest-small.zip`). This will be automatically extracted.

## Usage

To run the recommendation system, follow these steps:

1. Extract and load the data using the `zipfile` module.
2. Run the collaborative filtering algorithm to generate movie recommendations for users.
3. Apply the SVD-based matrix factorization method to further refine recommendations.
4. Evaluate the performance using RMSE (Root Mean Squared Error).

## Algorithms

This recommendation system utilizes two key algorithms: **Collaborative Filtering with Cosine Similarity** and **Singular Value Decomposition (SVD)**.

### 1. Collaborative Filtering with Cosine Similarity

#### Overview:
Collaborative Filtering is a popular method used in recommendation systems to make automatic predictions (filtering) about a user's preferences by collecting preferences from many users (collaborating). The assumption is that if a user has agreed with another user on a particular item, they are more likely to agree on other items as well.

#### How It Works:
- **User-Based Collaborative Filtering:** We calculate the similarity between users based on their movie ratings. The assumption is that similar users will give similar ratings to the same movies.
  
- **Cosine Similarity:** We use the cosine similarity metric to measure how similar two users are based on the angle between their ratings vectors. Cosine similarity computes the cosine of the angle between two non-zero vectors in a multi-dimensional space, which essentially tells us how close two users are in terms of their preferences.

  The cosine similarity formula is:
  \[
  \text{similarity}(A, B) = \frac{A \cdot B}{||A|| ||B||}
  \]
  where \(A\) and \(B\) are the rating vectors for two users.

#### Prediction:
Once the user similarity matrix is computed, we can predict a user's rating for a movie by taking a weighted sum of the ratings of similar users for that movie. The weights are the cosine similarities between users.

The formula for predicting the rating of user \(u\) for movie \(i\) is:
\[
\hat{r}_{ui} = \bar{r}_u + \frac{\sum_{v} (\text{similarity}(u, v) \cdot (r_{vi} - \bar{r}_v))}{\sum_{v} |\text{similarity}(u, v)|}
\]
where \( \hat{r}_{ui} \) is the predicted rating, \( \bar{r}_u \) is the mean rating of user \(u\), and \( r_{vi} \) is the actual rating given by user \(v\) to movie \(i\).

### 2. Singular Value Decomposition (SVD)

#### Overview:
SVD is a matrix factorization technique that decomposes a user-item interaction matrix (in this case, the user-movie rating matrix) into three matrices. This technique helps to reduce the dimensionality of the data, capturing latent features that explain patterns in the user-movie interactions.

#### How It Works:
The matrix factorization via SVD splits the original user-movie rating matrix \(R\) into three matrices: 
\[
R = U \Sigma V^T
\]
- **U:** User-feature matrix (users in rows, latent features in columns)
- **Σ (Sigma):** Diagonal matrix containing singular values (strength of each latent feature)
- **V^T:** Movie-feature matrix (movies in columns, latent features in rows)

SVD identifies latent factors that influence the ratings. For example, the latent factors could represent underlying themes such as a preference for action movies or romantic comedies.

#### Prediction:
After decomposing the original matrix, we can reconstruct an approximate version of the user-movie rating matrix by multiplying the matrices back together:
\[
\hat{R} = U \Sigma V^T
\]
Here, \( \hat{R} \) is the predicted rating matrix, which contains the predicted ratings for all users and movies.

### Key Differences:
- **Collaborative Filtering with Cosine Similarity:** Relies on the direct similarity between users, assuming users with similar past behavior will have similar future preferences.
- **SVD:** Identifies latent factors from the data, which can sometimes better capture hidden relationships between users and movies (such as genre preferences) that aren't directly observable through similarity alone.

### Strengths and Weaknesses:

| Algorithm                            | Strengths                                                                                   | Weaknesses                                                                        |
|--------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
| Collaborative Filtering (Cosine)     | Simple to implement; interpretable; leverages direct user similarities.                     | Struggles with sparse data; may not generalize well to unseen users/movies.       |
| SVD                                  | Captures latent factors; reduces dimensionality; can handle sparse data better.             | More complex to implement; computationally intensive for large datasets.         |

These two methods complement each other well. Cosine similarity is good for capturing direct similarities between users, while SVD provides a deeper understanding by uncovering hidden patterns in the data.

Both methods are evaluated using **Root Mean Squared Error (RMSE)** to determine how well they predict user ratings for movies.


## Evaluation
The model is evaluated using Root Mean Squared Error (RMSE). This metric helps measure how well the predicted ratings match the actual ratings. Lower RMSE values indicate better performance.In this system,SVD algorithm can give more accurate recommendations than cosine similarity model due to less RMSE.

## Dataset
The dataset used for this project is the MovieLens dataset (latest small version), which contains 100,000 ratings from 600 users on 9,000 movies.

The dataset is publicly available and can be downloaded from the [MovieLens website](https://grouplens.org/datasets/movielens/).
## License
This project is licensed under the MIT License.


