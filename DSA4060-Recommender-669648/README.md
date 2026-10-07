# DSA 4060 Personalized Movie Recommender

## Student Details
- **Name:** Sean
- **Student ID:** 669648
- **Assigned User ID:** 9 (last two digits 48, 48 MOD 40 = 8, 8 + 1 = 9)

## Project Objective
This project builds a simple content-based movie recommender for one assigned user (User 9). It looks at the movies the user rated highly, works out which genres they prefer, and suggests five movies they have not rated yet that match those tastes.

## Datasets
- `movies.csv` – the movie catalogue (36 movies) with `movie_id`, `title` and `genres` (genres separated by `|`).
- `ratings.csv` – 440 historical ratings from 40 users with `user_id`, `movie_id` and `rating`. Neither file has missing values.

## Method / Approach
1. Loaded and inspected both files with pandas.
2. Filtered the ratings of User 9 (13 movies) and looked at their top-rated movies and the average rating per genre.
3. Treated movies rated 4.0 or higher as "liked" (Inception, John Wick, Interstellar).
4. Converted genres to numeric vectors with `CountVectorizer`.
5. Averaged the liked movies' vectors into a user profile and ranked every catalogue movie by **cosine similarity** to that profile.
6. Removed movies User 9 had already rated and kept the top five.

## How to Run the Notebook
Requirements: Python 3, `pandas`, `numpy`, `scikit-learn` and Jupyter (`pip install pandas numpy scikit-learn jupyter`).
Keep `movies.csv` and `ratings.csv` in the same folder as the notebook, open `DSA4060_Recommender_669648.ipynb`, and run all cells from top to bottom (Kernel > Restart & Run All).

## Recommendation Results
| Rank | Movie | Genres |
|------|-------|--------|
| 1 | Blade Runner 2049 | Sci-Fi, Drama |
| 2 | Mission: Impossible - Fallout | Action, Thriller |
| 3 | Get Out | Horror, Thriller |
| 4 | The Shawshank Redemption | Drama |
| 5 | Mad Max: Fury Road | Action, Adventure |

User 9 rated Sci-Fi, Thriller and Action films the highest, so the top picks share those genres with Interstellar and John Wick. The lower-ranked picks (Shawshank, Mad Max) only match on one genre, so they are weaker matches.

## Limitation and Suggested Improvement
**Limitation:** The model only uses genre labels, so it can't separate two movies with the same genres, and it ignores what the other 39 users think. User 9 also only has three liked movies, which is thin evidence.
**Improvement:** Combine this with collaborative filtering (using ratings from similar users) and add richer features such as director, cast or plot keywords, with the profile weighted by rating.
