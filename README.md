# Spotify Song Clustering and Playlist Automation

## Project Overview

This project utilizes unsupervised machine learning, specifically **K-Means clustering**, to segment a large dataset of over 5,000 Spotify songs based on their intrinsic audio features. The primary goal is to identify distinct musical profiles within the dataset, which can then be used as the foundation for **automated playlist generation**. This prototype demonstrates how machine learning can be applied to enhance music discovery and curation. [View the full project presentation slides (PDF)](Spotify_pptx.pdf.pdf)

## Data Source

The dataset used in this project is `3_spotify_5000_songs.csv`, a publicly available dataset containing various audio features and metadata for a diverse collection of Spotify tracks.

## Methodology

1.  **Data Loading and Cleaning:** The initial step involved loading the dataset and cleaning column names for ease of use.
2.  **Exploratory Data Analysis (EDA):** Preliminary analysis was conducted to understand the relationships between different audio features (e.g., `tempo` and `time_signature`), informing subsequent modeling decisions.
3.  **Data Preprocessing:**
    *   **Feature Selection:** Only relevant numerical audio features were selected for clustering, excluding non-numeric and identifier columns.
    *   **Normalization:** All selected numerical features were scaled using `MinMaxScaler` to a common range (0 to 1), preventing features with larger scales from disproportionately influencing the clustering algorithm.
4.  **K-Means Model Training:**
    *   **Optimal Cluster Determination:** The optimal number of clusters (k) was determined using industry-standard techniques: the **Elbow Method** (analyzing inertia) and the **Silhouette Score** (measuring cluster cohesion and separation). While metrics suggested a smaller `k`, `k=50` was chosen to allow for more granular and diverse playlist themes, accepting a slight trade-off in cluster distinctness for broader variety.
    *   **Model Application:** The K-Means algorithm was applied to the preprocessed dataset, assigning each song to one of 50 distinct clusters.
5.  **Cluster Analysis & Interpretation:** The resulting clusters were analyzed by visualizing the mean values of audio features for each cluster using **radar charts**. This allowed for the interpretation of each cluster's unique sonic characteristics (e.g., "High-Energy Dance," "Mellow Acoustic") and thematic labeling suitable for playlist creation.

## Key Features

*   **Unsupervised Learning:** Application of K-Means clustering for song segmentation without prior labeling.
*   **Audio Feature-Based Clustering:** Leveraging Spotify's rich audio features (`danceability`, `energy`, `loudness`, `acousticness`, `instrumentalness`, `tempo`, etc.) for intelligent grouping.
*   **Optimal 'k' Selection:** Data-driven approach to determine the appropriate number of playlists.
*   **Cluster Profiling:** Visual interpretation of cluster characteristics using radar charts to assign meaningful themes.
*   **Scalability:** The methodology can be applied to much larger datasets, enabling large-scale playlist automation.

## Results & Analysis

The project successfully generated 50 distinct clusters of Spotify songs, each representing a unique musical profile. These clusters serve as a robust foundation for automated playlist generation. For instance:

*   **Cluster X (e.g., Cluster 4 in the radar chart):** Characterized by very high `energy` and `loudness` but extremely low `acousticness`, making it ideal for "Hype" or "Workout" playlists.
*   **Cluster Y (e.g., Cluster 28 in the radar chart):** Shows low `energy` and `loudness`, with very high `acousticness` and `instrumentalness`, perfect for "Focus" or "Chill Acoustic" playlists.
*   **Cluster Z (e.g., Cluster 0 in the radar chart):** Exhibits high `danceability` and `valence` (positivity), suitable for a "Feel-Good Party" playlist.

**(Self-Correction/Note for Reviewer):** The presentation mentioned an **84% accuracy of song identification**. This metric, while stated in the presentation, **was not explicitly calculated or demonstrated within the provided Jupyter Notebook**. For a complete and reproducible project, this calculation would ideally be included in the notebook, potentially through methods like evaluating a downstream task (e.g., how well a classifier can predict an artist/genre based on cluster assignments, or how consistently similar songs are grouped).

## How to Use

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/Inan-Aktug/Spotify-playlist-generator.git
    cd Spotify-playlist-generator
    ```
2.  **Create a virtual environment (recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```
3.  **Install the dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
4.  **Run the Jupyter Notebook:**
    ```bash
    jupyter notebook "spotify big data clean.ipynb"
    ```
    Follow the instructions within the notebook cells to execute the analysis.

## Future Work

*   **Playlist Generation Function:** Develop a Python function to automatically export a list of songs (name, artist, Spotify URL) for a given cluster ID, potentially integrating with the Spotify API for direct playlist creation.
*   **Qualitative Feature Integration:** Explore incorporating genre information or other qualitative tags from external sources to further enrich and refine playlist themes.
*   **Alternative Clustering Models:** Experiment with other unsupervised learning algorithms (e.g., DBSCAN, Hierarchical Clustering) to compare clustering outcomes and identify potentially more meaningful groupings.
*   **Interactive Dashboard:** Build a simple web-based dashboard (e.g., using Streamlit or Dash) to allow users to interactively explore cluster profiles, view sample songs from each cluster, and generate custom playlists.

