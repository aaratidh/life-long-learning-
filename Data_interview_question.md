### how you can describe your experience designing and implementing a data warehouse and schema at a senior level, tied to your projects:

### what is  Relational data modeling ? 
- helpful in OLTP
- not in Analytic purpose
- Production data
- Great for single Entity access
### what is kimball/dimensional data Modeling? 
- OLAP analytic purpose
- Analysis Data
- Dimesnional modeling one fact tabel another dimensional Table
- SCD dimension 


Example of  one problem faced by the Data Engineering scenarion? 
In the video you referenced, the speaker uses a hypothetical scenario about Facebook to illustrate a common data engineering problem and its solution. Here's a breakdown of the example:

### The Situation:

Imagine you're a data engineer at Facebook. You have access to several key pieces of data:

* **`users` table:** This contains information about each user, like their ID, name, and country.
* **`posts` table:** This holds the content of each post, including a user ID to link it to the person who wrote it.
* **`post_actions` log:** This is a continuous stream of events related to posts, such as likes, comments, and shares. It logs the post ID, the user ID of the person who took the action, the type of action, and when it happened.

### The Problem:

A product manager comes to you with a seemingly simple question: **"How many posts that contain the phrase 'SQL sucks' have been deleted?"** [18:52]

This question highlights a key challenge in data engineering:

* **Deleted Data is Gone:** When a post is deleted from the main `posts` table, it's gone. You can't just query the current database to find it.
* **Logs Have Limited Information:** While the `post_actions` log might show that a post was deleted, it doesn't contain the actual text of the post.

### The Solution (and its evolution):


The speaker walks through a multi-step solution that data engineers often employ:
1.  **Daily Snapshots:** The first step is to take a daily "snapshot" of the `users` and `posts` tables and store them in a data lake [20:03]. This creates a historical record. Now, even if a post is deleted from the live database, you have a copy of it from a previous day's snapshot.
2.  **Identifying Deleted Posts:** By comparing two consecutive daily snapshots (e.g., yesterday's and today's), you can identify which posts have been deleted. If a post ID exists in yesterday's snapshot but not in today's, it has been deleted [23:04].
3.  **Slowly Changing Dimensions (SCDs):** To make this more efficient, the speaker introduces the concept of Slowly Changing Dimensions (SCDs) [24:32]. Instead of storing a full copy of the data every day, you only track the changes. For example, for the `posts` table, you could have columns like `is_deleted` and `post_text` that are updated as changes occur, along with start and end dates for each version of the record.
4.  **One Big Table (OBT):** For even more complex questions, like "How many likes does a post containing 'SQL sucks' get before it's deleted?", the speaker proposes a "One Big Table" (OBT) approach [32:11]. In this model, you would create a single, wide table for each post. This table would include the post's information and an array of all the actions that have ever happened to that post (likes, comments, etc.).
    * **Benefit:** This makes it very fast to analyze the entire history of a post without having to join large tables. You can easily filter and analyze the actions within the array.
    * **Trade-off:** This approach uses more storage because you are duplicating some data.

The speaker concludes by mentioning that this OBT architecture was used at Facebook to analyze long-term trends after a drop in growth, demonstrating its real-world application for complex analysis

###  describe one challanbge bug you covered in your work experince?

```txt
"Absolutely! At Capital One, I noticed that our PySpark ETL jobs processing large financial transaction data were experiencing unpredictable runtimes and sometimes failing due to skewed data partitions.

Instead of simply scaling up clusters (which increases costs), I took an innovative approach. I designed a dynamic partitioning strategy where the job analyzes the distribution of keys before executing transformations.

I built a small pre-processing module in Python that samples the data, calculates approximate record counts per key, and dynamically adjusts partition ranges and sizes based on that distribution. I integrated this module as a reusable component into our Airflow DAGs, so every job could automatically adjust partitions at runtime.

This drastically reduced shuffle-heavy operations, decreased job runtimes by about 35%, and significantly lowered EMR costs.

Moreover, I extended this concept to create a custom Spark listener that tracked stage-level metrics and automatically recommended further optimizations for future runs — something not supported out-of-the-box.

This solution not only improved pipeline efficiency but also empowered the team to adopt a more data-driven approach to job tuning, moving away from guesswork and manual tweaking."

```
## Challange in recent project  

- Problem was: data skewed ko
- How did you find ma - Spark ui metrics
- causes :  Uneven key  
- Solution was: 
         - salting
         - Adaptive query execution
## What did you do for cost  optimization and what did you do to make sure it  does not impact data quality and completeness ?
- Added Validation check point
- Hash checks between pre- and post optimization
- end to end lineage USe Delta lake ACIDIC trasncation for consistency during merge
  
  








