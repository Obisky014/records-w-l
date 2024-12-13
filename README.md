# Serie A Standings Prediction with XGBoost

This project uses historical data to predict the final standings of Serie A for the 2023-2024 season after 38 games. The model uses XGBoost to predict the points for each team based on their current performance and features.

# Project Overview
We predict the final Serie A standings using the following approach:

# Dataset:

We use data for the 2023-2024 Serie A season up to the 15th matchday for each team,which was obtained from understat.com, which includes:
Matches Played (MP)

Wins (W)

Draws (D)

Losses (L)

Goals For (GF)

Goals Against (GA)

Expected Goals (xG)

Expected Goals Against (xGA)

Goal Difference (GD)

Points (PTS)

# Goal:

The model's aim is to predict the final standings based on the data from the first 15 matches.
Steps:

# Data Preparation: 
Clean and preprocess the dataset, including encoding categorical features like Team into numeric values.
# Modeling:
Use XGBoost for regression to predict the points each team will accumulate by the end of the season.
# Simulation: 
Simulate the points accumulation for the remaining 23 games, and calculate the final standings after 38 games.
# Results: 
Sort teams by their total predicted points.

# Steps to Run the Project
Install Required Libraries

Load the dataset with pandas (explained a bit below)

# Load the dataset
using the syntax format, df = pd.read_csv('your_data_name.csv')

Preprocessing
   
Encode the Team feature using LabelEncoder.

Drop unnecessary columns (like FormScore).

Train the Model


# Split dataset

which is usually done by dropping features and selecting target features(in my case i only dropped one feature, FormScore. So only points needed to be dropped). The syntax I used was;

X = df.drop(columns=['Points'])

y = df['Points']

# Train-test split
The synatx I used for this process is found below as;

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Train the XGBoost model
model = XGBRegressor(n_estimators=100, learning_rate=0.07, max_depth=4, random_state=42)

Then you fit the model;

model.fit(X_train, y_train)

# Predicting Final Standings
Which is done by using the .predict function (refer to my code above the README file for full work)

# Simulate points for the remaining games
The syntax for which is;

remaining_games = 23

predicted_points_for_remaining_games = model.predict(X)

# Add the predicted points for the remaining games to the current points
df['Predicted_Final_Points'] = df['Points'] + (predicted_points_for_remaining_games * remaining_games / 15)

# Sort teams by predicted points
df_sorted = df.sort_values(by='Predicted_Final_Points', ascending=False)

# Show final predicted standings
df_sorted[['Team', 'Predicted_Final_Points']]

Results

The final standings are displayed by sorting teams in descending order of predicted points.

# Conclusion
This project uses XGBoost to predict the outcome of the remaining matches in Serie A based on historical performance data. The approach can be extended to include more sophisticated features and improve the accuracy of predictions.

