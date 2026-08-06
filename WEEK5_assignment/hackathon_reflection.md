# Hackathon #1 Reflection

**Biggest technical hurdle:** the handover between roles broke in a way
that wasn't obvious until validation time. As Validation & Analytics Lead,
I received `predictions.csv` from the ML Engineer, but it had been exported
with `index=False`, silently dropping the row index needed to match
predictions back to their timestamps. Without timestamps, I could only
measure performance per sensor reading, not per actual failure event —
which meant I couldn't build the "caught 3 of 4 failures with 24 hours'
notice" story an ROI pitch actually needs. The handed-off model file also
turned out to be unfitted (pickled before `.fit()` was called), and a
"clean" dataset I received later turned out to be a partial slice missing
the real failure events entirely.

**How I resolved it:** I traced each gap back to its source instead of
working around it silently — fixed the export step to include timestamps,
re-fit and re-saved the model, and re-ran the full pipeline myself to
produce a verified, fully-executed notebook. Where real data wasn't
available in time, I used clearly-labeled synthetic placeholders rather
than let incomplete data pass as a real result.

**What I'd do differently:** agree on the exact handover schema — columns,
index behavior, file locations — before anyone starts exporting files, not
after validation breaks. A two-line data contract at kickoff would have
caught all three issues before they cost time.
