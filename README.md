from scipy.optimize import linear_sum_assignment
import numpy as np

# Define the data with updated names
men = [
    ("Daniel", "Liberal", "Running", "Rural", "Introverted"),
    ("Peter", "Liberal", "Chess", "Rural", "Outgoing"),
    ("Adam", "Conservative", "Running", "Urban", "Introverted"),
    ("Chris", "Liberal", "Running", "Rural", "Introverted"),
    ("Ronald", "Conservative", "Running", "Rural", "Introverted"),
    ("Graham", "Conservative", "Chess", "Rural", "Introverted"),
    ("Proud", "Conservative", "Chess", "Urban", "Introverted"),
    ("David", "Liberal", "Chess", "Urban", "Introverted"),
    ("Carlington", "Liberal", "Running", "Urban", "Introverted"),
    ("Samuel", "Liberal", "Running", "Urban", "Outgoing")
]

women = [
    ("Theresa", "Conservative", "Chess", "Rural", "Introverted"),
    ("Betty", "Liberal", "Running", "Rural", "Introverted"),
    ("Cassandra", "Conservative", "Chess", "Rural", "Outgoing"),
    ("Alletha", "Conservative", "Running", "Urban", "Outgoing"),
    ("Victoria", "Conservative", "Chess", "Urban", "Outgoing"),
    ("Cassie", "Liberal", "Running", "Urban", "Introverted"),
    ("Tracy", "Conservative", "Chess", "Urban", "Outgoing"),
    ("Martha", "Conservative", "Running", "Urban", "Outgoing"),
    ("Silvia", "Liberal", "Chess", "Urban", "Introverted"),
    ("Sarah", "Liberal", "Running", "Rural", "Introverted")
]

# Calculate compatibility scores
numMen = len(men)
numWomen = len(women)
scoreMatrix = np.zeros((numMen, numWomen))

for i, man in enumerate(men):
    for j, woman in enumerate(women):
        score = 0
        for k in range(1, 5):  # Compare attributes: Politics, Hobby, Living Preference, Social
            if man[k] == woman[k]:
                score += 1
        scoreMatrix[i, j] = score

# Use Hungarian algorithm to find the optimal matching
rowInd, colInd = linear_sum_assignment(-scoreMatrix)  # Negate scores for maximization

# Display the results
totalScore = 0
print("Optimal Matches:")
for i in range(len(rowInd)):
    manIdx = rowInd[i]
    womanIdx = colInd[i]
    matchScore = scoreMatrix[manIdx, womanIdx]
    totalScore += matchScore
    print(f"{men[manIdx][0]} is matched with {women[womanIdx][0]} - Score: {int(matchScore)}")

print(f"\nMaximum Total Score: {int(totalScore)}")
