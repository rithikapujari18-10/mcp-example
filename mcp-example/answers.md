# Assignment Answers

## 1. Tool counts and client changes

The server listed 8 tools in Part 1 and 9 in Part 3. I did not change
anything in the client to make `predict_both` appear. I only edited the
server. The client asks the server for its tool list each time it runs,
so the new tool was discovered automatically.

## 2. Disagreements

The two models disagree on 8 of the 114 test patients.

| Patient | True Diagnosis | Logistic Regression | KNN | Correct Model |
|---|---|---|---|---|
| 3 | benign | benign | malignant | Logistic Regression |
| 25 | benign | benign | malignant | Logistic Regression |
| 48 | benign | benign | malignant | Logistic Regression |
| 53 | malignant | benign | malignant | KNN |
| 76 | malignant | malignant | benign | Logistic Regression |
| 80 | benign | benign | malignant | Logistic Regression |
| 99 | benign | benign | malignant | Logistic Regression |
| 102 | malignant | malignant | benign | Logistic Regression |

## 3. Which model was right more often

Logistic Regression was correct in 7 of the 8 disagreements, and KNN in 1.
This shows Logistic Regression did better on these cases, but it does not
by itself establish that it performs better overall. KNN mostly predicted
malignant for benign patients (false alarms), but it also missed two
cancers (patients 76 and 102). Logistic Regression missed one (patient 53).

## 4. Why the description matters

An AI app cannot read the tool's code. It only sees the tool's name, its
inputs, and the description in triple quotes. It uses the description to
decide whether the tool fits the user's request, for example choosing
`predict_both` over `predict_knn`. A vague or missing description means
the tool might not be chosen, or might be misused.

## 5. Why logging every call is useful

The log records which tool was called, with what request ID, and whether
it succeeded. This helps with debugging, accountability, and reviewing a
surprising prediction later, which matters in a medical setting. In my
run, the audit log showed `hw-sample` and `hw-both` calls all with
status `success`.