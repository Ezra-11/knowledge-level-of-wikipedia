Zambian Wikipedia Contributor Classifier - README
Project Overview
This project, developed for the DataLab Research group at The University of Zambia, classifies Wikipedia contributors to Zambian content into Novice, Intermediate, and Expert knowledge levels to enhance content quality and contributor engagement. It follows the CRISP-DM methodology, covering Business Understanding, Data Understanding, Data Preparation, Modeling, Evaluation, and Deployment.

Dataset: zambia_contributors_summary.csv (129 unique contributors to 20 Zambia-related Wikipedia pages).
Methodology:
Unsupervised Learning: K-Means clustering (k=3) to generate proxy labels (Novice, Intermediate, Expert).
Supervised Learning: Random Forest Classifier to predict knowledge levels based on 15 engineered features (e.g., Total_Edits, Longevity_Factor).


Deployment: A Streamlit web application and a Python function (fxn_predict_new_instance) for classifying contributors, with scalability (<1 minute per contributor) and interpretability (feature importance charts).
Key Outcomes: Achieved ~100% accuracy (inflated due to class imbalance: 115 Novice, 12 Intermediate, 1 Expert), enabling targeted strategies for Wikipedia admins and researchers.

For details, see the notebook DataMining_Zambia_Wikipedia_Classifier.ipynb.
Prerequisites

Google Colab environment (browser-based, no local setup required).
Google Drive with access to the shared folder misc-unza25-csc4792-project_team32.
ngrok Account: Obtain a free API key from ngrok.com for Streamlit app hosting.
Python Libraries: Installed automatically in the notebook (pandas, numpy, scikit-learn, streamlit, pyngrok, matplotlib, seaborn).

File Structure
The shared Google Drive folder (/content/drive/My Drive/misc-unza25-csc4792-project_team32/) contains:

DataMining_Zambia_Wikipedia_Classifier.ipynb: Main Colab notebook with all code (data loading, preparation, modeling, deployment).
zambia_contributors_summary.csv: Raw dataset (129 contributors, features like Total_Edits, Pages_Edited).
Generated Files (created by running the notebook):
zambia_wikipedia_cleaned.csv: Cleaned dataset after initial preprocessing.
zambia_wikipedia_contributors_features_engineered.csv: Dataset with engineered features (e.g., Account_Age_Days, Longevity_Factor).
zambia_wikipedia_contributors_tranformed_data.csv: Standardized features for modeling.
zambia_contributors_final_labeled.csv: Final dataset with K-Means cluster labels.
contributor_classifier_model.pkl: Trained Random Forest model for predictions.
data_scaler.pkl: StandardScaler for feature scaling.
contributor_app.py: Streamlit app code.


README.md: This file, explaining setup and usage.

Note: The generated files are created by running all cells in the notebook. Pre-generated versions are included in the shared folder for convenience, but running the notebook ensures the latest, consistent versions.
Setup Instructions

Access the Shared Folder:

Open Google Drive and navigate to Shared with Me/misc-unza25-csc4792-project_team32/.
Confirm you have at least Viewer access (or Editor to modify files).


Open the Notebook:

Right-click DataMining_Zambia_Wikipedia_Classifier.ipynb > Open with > Google Colaboratory.


Set Up ngrok API Key:

Sign up at ngrok.com and copy your API key from the dashboard.
In Colab, click the key icon in the left sidebar to open the Secrets tab.
Add a new secret:
Name: NGROK_AUTH_TOKEN
Value: Paste your ngrok API key
Enable Notebook access toggle
Save


Why: The key securely creates a public URL for the Streamlit app without hardcoding.


Mount Google Drive:

Run the cell with:from google.colab import drive
drive.mount('/content/drive')


Authenticate with your Google account to access the shared folder.


Run the Notebook:

Execute all cells in order (Shift+Enter or Runtime > Run all).
This:
Installs libraries (pip install streamlit pyngrok).
Loads zambia_contributors_summary.csv from the shared folder.
Generates intermediate files (zambia_wikipedia_cleaned.csv, etc.) and saves them to the shared folder.
Trains the Random Forest model and saves contributor_classifier_model.pkl and data_scaler.pkl.
Creates contributor_app.py.
Launches the Streamlit app via ngrok.


Note: Running all cells regenerates all files, ensuring consistency. Pre-generated files in the folder can be used if you skip this step, but regeneration is recommended.


Access the Streamlit App:

After running the deployment cell (Section 6.6), a public URL (e.g., https://random-string.ngrok.io) is printed.
Open the URL in a browser to use the app:
Enter standardized feature values (-5 to 5) for a contributor (e.g., Total_Edits=2.0).
Click Classify to see the predicted knowledge level (Novice/Intermediate/Expert), confidence scores, and feature importance chart.




Alternative: Use Prediction Function:

If the Streamlit app fails (e.g., ngrok issues), test the model with the fxn_predict_new_instance function (Section 6.5):sample_input = {
    'Total_Edits': 2.0, 'Pages_Edited': 1.5, 'Total_Size': 1.8,
    'Active_Days': 1.2, 'Activity_Span_Years': 0.8, 'Edits_per_Month': 1.5,
    'Account_Age_Days': 1.0, 'Recency_Days': -0.5, 'Edit_Frequency': 1.2,
    'Consistency_Score': 1.0, 'Pages_per_Year': 0.9, 'Edits_per_Page': 1.1,
    'Avg_Contribution_Size': 1.3, 'Contribution_Intensity': 1.4, 'Longevity_Factor': 1.6
}
result = fxn_predict_new_instance(sample_input)
print("Sample Prediction Result:", result)





Usage

Streamlit App:
Input 15 standardized features (e.g., Total_Edits, Longevity_Factor) via the form.
Outputs: Predicted knowledge level, confidence scores (e.g., Novice=0.1, Intermediate=0.8, Expert=0.1), and a bar chart of feature importances.
Use Case: Wikipedia admins classify contributors to assign mentoring or review tasks.


Prediction Function:
Programmatic interface for scripts or API integration.
Input: Dictionary of 15 standardized features.
Output: Dictionary with predicted level and confidence scores.


Future Enhancements:
Integrate Wikipedia API for real-time data fetching.
Allow raw feature inputs with auto-scaling.
Deploy on Heroku/AWS for production.



Troubleshooting

ngrok Error (Invalid Token):
Ensure NGROK_AUTH_TOKEN is set in Colab Secrets (exact name, case-sensitive).
Verify the token is valid in your ngrok dashboard.


Model/Scaler Not Found:
Run all notebook cells to generate contributor_classifier_model.pkl and data_scaler.pkl.
Alternatively, use pre-generated files in the shared folder, but regeneration is preferred for consistency.


Drive Mount Issues:
Re-authenticate when prompted.
Check folder path (/content/drive/My Drive/misc-unza25-csc4792-project_team32/).


Class Imbalance Warning:
The notebook notes only 1 Expert sample, limiting model robustness. Future work includes SMOTE or more data.



Notes

Running All Cells: Regenerating files by running the notebook ensures consistency and demonstrates the full pipeline. Pre-generated files are included for convenience but may not reflect the latest notebook changes.
Security: The ngrok API key is stored in Colab Secrets, not hardcoded, ensuring security. Users must set their own key to run the app.
Dependencies: All libraries are installed in the notebook. No local setup is needed.
Limitations: The model’s ~100% accuracy is inflated due to class imbalance (115 Novice, 12 Intermediate, 1 Expert). Cross-validation or synthetic data generation is recommended for production.

Contact
For questions, contact the DataLab Research group at The University of Zambia or the project team (Team 32, CSC4792, 2025).
