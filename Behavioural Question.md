## The project in Capital one: 
## conflict resolution example

- Transcation Analystics and prediction project :
- data science team wanted immediate access to raw ride data for real time fradulent prediction
- But,  we As a data engineer, I insisted on routing all data through our ETL pipeline first to ensure data quality, schema consistency, and compliance before it hit warehouse  for analytics teams. 
- So there was a concern of data complinace and goverance and privacy. 
- But data scinetist felt that downstrm pipline will slow the down experimentation

- I suggested a two-layer approach — we built a sandbox table that received live data from Kafka every few minutes with sensitive details hidden.
- Our main ETL still processed clean, verified data for reports.
- This way, data scientists got quick access to fresh data for testing, while we kept production data accurate and secure
