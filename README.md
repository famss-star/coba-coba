# Redis

## Masuk
docker exec -it redis_leaderboard redis-cli

## Tambah Data
ZADD leaderboard 100 PemainA
ZADD leaderboard 150 PemainB
ZADD leaderboard 120 PemainC
ZADD leaderboard 90 PemainD
ZADD leaderboard 110 PemainE
ZREVRANGE leaderboard 0 2 WITHSCORES
ZREVRANK leaderboard PemainA
ZSCORE leaderboard PemainA
ZINCRBY leaderboard 50 PemainB

## Panggil Data
ZADD leaderboard 100 PemainA
ZADD leaderboard 150 PemainB
ZREVRANGE leaderboard 0 2 WITHSCORES

## Keluar
exit

# Mongo

## Masuk
docker exec -it mongodb_blog mongosh

## Tambah Data
### 1. Menyisipkan 2 postingan blog (dengan komentar disematkan)
use blog
db.posts.insertMany([
  {
    title: "Belajar MongoDB",
    author: "Rifa",
    tags: ["mongodb", "database", "nosql"],
    content: "MongoDB adalah database NoSQL yang fleksibel.",
    comments: [
      { user: "Ali", comment: "Sangat membantu!", date: new Date() }
    ]
  },
  {
    title: "Tips NoSQL",
    author: "Budi",
    tags: ["nosql", "tips"],
    content: "Beberapa tips menggunakan NoSQL.",
    comments: [
      { user: "Salma", comment: "Terima kasih tipsnya!", date: new Date() }
    ]
  }
])

### 2. Mencari postingan berdasarkan penulis
db.posts.find({ author: "Rifa" })

### 3. Mencari postingan dengan tag tertentu
db.posts.find({ tags: "nosql" })

### 4. Menambahkan komentar baru ke postingan
db.posts.updateOne(
  { title: "Belajar MongoDB" },
  { $push: { comments: { user: "Budi", comment: "Artikel bagus!", date: new Date() } } }
)

### 5. Memperbarui konten salah satu postingan
db.posts.updateOne(
  { title: "Tips NoSQL" },
  { $set: { content: "Tips terbaru menggunakan NoSQL untuk pemula." } }
)

## Keluar
exit

# Casandra
## Masuk
docker exec -it cassandra_iot cqlsh

### 1. Membuat keyspace dan tabel untuk sensor IoT
CREATE KEYSPACE iot WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 1};
USE iot;
CREATE TABLE sensor_data (
    sensor_id text,
    timestamp timestamp,
    value double,
    PRIMARY KEY (sensor_id, timestamp)
) WITH CLUSTERING ORDER BY (timestamp DESC);

### 2. Menyisipkan 10 pembacaan dari 3 sensor berbeda
INSERT INTO sensor_data (sensor_id, timestamp, value) VALUES ('sensorA', toTimestamp(now()), 23.5);
INSERT INTO sensor_data (sensor_id, timestamp, value) VALUES ('sensorA', toTimestamp(now()), 24.1);
INSERT INTO sensor_data (sensor_id, timestamp, value) VALUES ('sensorA', toTimestamp(now()), 22.8);
INSERT INTO sensor_data (sensor_id, timestamp, value) VALUES ('sensorB', toTimestamp(now()), 30.2);
INSERT INTO sensor_data (sensor_id, timestamp, value) VALUES ('sensorB', toTimestamp(now()), 29.9);
INSERT INTO sensor_data (sensor_id, timestamp, value) VALUES ('sensorB', toTimestamp(now()), 31.0);
INSERT INTO sensor_data (sensor_id, timestamp, value) VALUES ('sensorC', toTimestamp(now()), 18.7);
INSERT INTO sensor_data (sensor_id, timestamp, value) VALUES ('sensorC', toTimestamp(now()), 19.2);
INSERT INTO sensor_data (sensor_id, timestamp, value) VALUES ('sensorC', toTimestamp(now()), 18.9);
INSERT INTO sensor_data (sensor_id, timestamp, value) VALUES ('sensorC', toTimestamp(now()), 19.0);

### 3. Mengambil semua data berdasarkan sensor tertentu, diurutkan berdasarkan waktu
SELECT * FROM sensor_data WHERE sensor_id = 'sensorA';

### 4. Mengambil data dalam rentang waktu tertentu untuk satu sensor
SELECT * FROM sensor_data WHERE sensor_id = 'sensorA' AND timestamp >= '2024-05-01 00:00:00' AND timestamp <= '2024-05-31 23:59:59';

## Keluar
:exit