# 🛠 SimpleMySQL

**SimpleMySQL** is a lightweight PHP class for interacting with MySQL databases via `mysqli`.  
It supports safe queries, transactions, JSON cache reading, and server variable access.

---

## 📦 Features

- 🔐 Safe prepared statements with parameter binding  
- 🔁 Full transaction control (`start()`, `finish()`, `stop()`)  
- 📄 Fetch single row or full result  
- 💾 JSON file reading support  
- ⚙ Access server variables like `max_connections`  
- 🌐 UTF-8 charset by default + autocommit disabled

---

## 🚀 Usage

### 🧱 Initialize the class

<pre><code>
require_once 'SimpleMySQL.php';
$db = new SimpleMySQL();
</code></pre>

---

### 🔍 Fetch a single row

<pre><code>
$user = $db->fetch("SELECT * FROM users WHERE id = ?", [1]);
echo $user['name'];
</code></pre>

---

### 📋 Fetch all rows

<pre><code>
$users = $db->fetchAll("SELECT * FROM users WHERE role = ?", ['admin']);
foreach ($users as $user) {
    echo $user['email'] . "&lt;br&gt;";
}
</code></pre>

---

### 📝 Execute update / insert / delete

<pre><code>
$db->execute("UPDATE users SET name = ? WHERE id = ?", ['Temirkhan', 2]);
</code></pre>

---

### 🔢 Get last inserted ID

<pre><code>
$db->execute("INSERT INTO users (name) VALUES (?)", ['NewUser']);
$id = $db->lastInsertId();
</code></pre>

---

### 🔄 Transaction control

<pre><code>
$db->start();

try {
    $db->execute("INSERT INTO logs (action) VALUES (?)", ['test']);
    $db->execute("UPDATE users SET status = ? WHERE id = ?", ['active', 1]);
    $db->finish(); // Commit
} catch (Exception $e) {
    $db->stop(); // Rollback
}
</code></pre>

---

### 📥 Read data from JSON cache file

<pre><code>
$data = $db->readCache('cache/users.json');
if ($data) {
    foreach ($data as $row) {
        echo $row['name'] . "&lt;br&gt;";
    }
}
</code></pre>

---

### ⚙ Get server variable

<pre><code>
echo $db->getVariable("max_connections");
</code></pre>

---

### ❎ Close connection

<pre><code>
$db->close();
</code></pre>

---

## 📄 License

MIT — free to use and modify.

> Developer: <strong>Temirkhan</strong>  
> <a href="https://www.instagram.com/temirkhanrustemov/">@temirkhanrustemov</a> • <code>temirkhan.onyx@gmail.com</code>
