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

1.  **Daily Snapshots:** The first step is to take a daily "snapshot" of the `users` and `posts` tables and store them in a data lake [20:03]. This creates a historical record. Now, even if

