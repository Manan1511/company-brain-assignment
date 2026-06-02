# Redis as a Caching Layer

## Component
Caching Layer

## Proposed Technology
Redis

## What does this component do?
When building fast websites or apps, we need a way to fetch data instantly. Normally, fetching data from a main database is like driving to a large warehouse miles away. Redis acts like a small desk drawer right next to you, where you store the things you use most often.

Without caching, the app will have to constantly fetch data from the main database which will take a hit on the overall perforamce. Efficient caching is vital for smooth performance

## Why did you choose this technology?

1. Super Fast Speed (In-Memory Storage)
   Instead of saving data on slow hard drives, Redis keeps everything in the computer's temporary memory (RAM). Reading from memory is incredibly fast, meaning your app can retrieve information in a fraction of a millisecond.
   
2. Simple Key-Value Setup
   Redis works like a dictionary. You give it a unique name (the key) and the information you want to store (the value). For example:
   Key: user:123:profile
   Value: {"name": "abc", "role": "xyz"}
   When you need the profile, you just ask Redis for user:123:profile, and it hands it to you immediately.

3. Handles Huge Traffic Easily
   If thousands of users open your app at the same time, your main database might crash under the pressure. Redis stands in front of the database, answering most of the questions so the main database doesn't get overwhelmed.

## Advantages

1. Automatic Expiry (Time-to-Live / TTL)
By setting an expiration time, Redis automatically deletes the old data. The next time a user asks for it, your app gets the fresh version from the main database and saves it in Redis again.

2. Eviction Policies (LRU - Least Recently Used)
When Redis runs out of memory, it automatically deletes the items you haven't touched in a long time (Least Recently Used) to make room for new, popular items. You don't have to clean up manually.

3. Hashes (Mini-Folders)
A Hash is like a small folder. Inside the folder user:123, you can have separate labels: name, email, and theme. If you only want to change the user's theme, you can update just that single label without reloading the whole folder.

4. Sorted Sets (Leaderboards and Lists)
Redis can automatically keep a list sorted by a score or a timestamp. You can ask for the "top 10 items" instantly without making your main database do heavy math.

## Limitations

1. Data Loss Risk
2. Memory Constraints
3. Complexity

## Flow

1. Check Redis first: When a user requests data, always ask Redis for it first.
2. If found (Cache Hit)
3. If not found (Cache Miss)

References:
Redis Official Caching Guide:https://redis.io/docs/latest/develop/use/caching/
Redis Data Types Documentation:https://redis.io/docs/latest/develop/data-types/
AWS Caching Best Practices: https://aws.amazon.com/caching/database-caching/
Redis Overview YT Video: https://www.youtube.com/watch?v=z_NbVtbgBJw&pp=ygUNcmVkaXMgY2FjaGluZw%3D%3D