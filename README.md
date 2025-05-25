# NoSQL Labs
# redish
This project contains various labs demonstrating the use of different NoSQL databases. Each lab is set up with Docker Compose to facilitate easy deployment and experimentation. Below are the details for each lab.

## Labs Overview

### 1. Redis Lab
- **Location:** `redis-lab/docker-compose.yml`
- **Purpose:** This lab uses Redis to create a real-time leaderboard.
- **Configuration:**
  - Redis image: `redis:latest`
  - Container name: `redis_leaderboard`
  - Port mapping: `6379:6379`

### 2. MongoDB Lab
- **Location:** `mongodb-lab/docker-compose.yml`
- **Purpose:** This lab uses MongoDB to implement a blogging system.
- **Configuration:**
  - MongoDB image: `mongo:latest`
  - Container name: `mongodb_blog`
  - Port mapping: `27017:27017`

### 3. Cassandra Lab
- **Location:** `cassandra-lab/docker-compose.yml`
- **Purpose:** This lab uses Apache Cassandra for managing IoT data.
- **Configuration:**
  - Cassandra image: `cassandra:latest`
  - Container name: `cassandra_iot`
  - Port mapping: `9042:9042`

### 4. Neo4j Lab
- **Location:** `neo4j-lab/docker-compose.yml`
- **Purpose:** This lab uses Neo4j for a movie recommendation system.
- **Configuration:**
  - Neo4j image: `neo4j:latest`
  - Container name: `neo4j_recommendation`
  - Port mapping: `7474:7474` and `7687:7687`
  - Environment variable: `NEO4J_AUTH=neo4j/password`

## Getting Started

To set up and run each lab environment, navigate to the respective lab directory and use Docker Compose commands:

1. **Navigate to the lab directory:**
   ```bash
   cd <lab-directory>
   ```

2. **Start the service:**
   ```bash
   docker-compose up
   ```

3. **Access the service:**
   - For Redis: `localhost:6379`
   - For MongoDB: `localhost:27017`
   - For Cassandra: `localhost:9042`
   - For Neo4j: `localhost:7474`

## Conclusion

This project provides a hands-on approach to understanding and working with various NoSQL databases. Each lab is designed to showcase specific features and use cases of the respective database technology.