# econ3916-lab17-classification
# Classification: When 90% Accurate Is Worthless

## Objective
I wanted to find out why accuracy is a poor guide for a loan-default classifier, and to pick a decision threshold based on what each kind of error costs instead.

## Methodology
- I worked with 6,000 simulated loan applications. The default rate was 9.6%, so a rule that approves everyone is already 90.4% accurate. I used that as my baseline.
- I fitted a logistic regression and checked it at the usual 0.5 threshold, recording its accuracy and how many defaults it predicted.
- I read the coefficients two ways: as changes in log-odds and as odds ratios. I then took the odds ratio for one more prior default and showed that the same ratio means a different change in probability depending on the applicant's starting probability.
- I traced precision and recall across six thresholds to see how they trade off.
- I gave a cost to each type of error (a missed default and a wrongly rejected good applicant), then chose the threshold that gave the lowest expected cost. I compared it with the threshold given by the closed-form result.
- I wrote a small function, `precision_recall_at()`, that returns a classifier's precision and recall at any threshold I give it.
- (Extension) I checked how well the model's predicted probabilities were calibrated.

## Key Findings
- At the 0.5 threshold the model was 90.4% accurate but predicted only 0 defaults. Its accuracy looks good until you compare it with the 90.4% I get by approving everyone.
- One more prior default multiplies the odds of default by 1.63. That fixed ratio does not translate into a fixed change in probability: the effect depends on where an applicant starts.
- The threshold that minimised expected cost was 0.121, close to the closed-form value of 0.118.
- At that threshold the expected cost was 944 per applicant, against 1,147 at 0.5.
- At the closed-form threshold, precision was 0.181 and recall was 0.477.
- (Extension) Calibration: [YOUR RESULT]

The main lesson for me was that the right threshold depends on the cost of each mistake, not on accuracy, and that 0.5 is rarely the right choice when one class is rare.
