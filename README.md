# Measuring Technological Filter Bubbles in Online News

## Data
In the data folder we provide two files, that together contain all the information needed to fit the analysis model.
These are dummy files, and can be replaced with identically structured files that contain real data.

- `item_metadata.csv` - item metadata from the [BBC dataset](https://www.kaggle.com/competitions/learn-ai-bbc/overview).
    - `item (int)`
    - `text (str)`
    - `topic (str)`

- `recommendations.csv` - 5000 randomly generated (user, item, timestamp) recommendation triplets, for 5 users, with items from the BBC dataset.
    - `timestamp (float)` - in seconds since epoch
    - `user (int)`
    - `item (int)`


## Running the notebooks

We provide 4 notebooks to be run in order to:

- `Add-Topics-to-Articles.ipynb` and `Add-Viewpoints-to-Articles.ipynb` both augment the metadata with topics based on the text available in the item. If you have your own topics, like the BBC data, you could skip these notebooks by copying the `item_metadata.csv` file to `item_metadata_with_tags.csv`, which will be used in subsequent notebooks.
- `Transform-Recommendation-Log-to-Samples.ipynb` takes the recommendations and the metadata with topics, and turns them into the aggregated observations we need to fit the model. It aggregates the recommendations of a user per week, and computes summary statistics such as diversity for that week and number of weeks the user has been on the platform. The resulting samples are written in `samples_for_model.csv`. 
- `Fit-Model.ipynb` is the final step, it will take the output of the previous notebook, and fit the GLMM model. Then it extracts the relevant coefficients and plots from the model for analysis as described in the paper.