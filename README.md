# 🛠️ SimpleMySQL — Lightweight MySQL Library for PHP

**SimpleMySQL** is a lightweight 💡 and minimalistic 📦 PHP library for working with MySQL using `mysqli`.  
It’s designed to make SQL interaction in your PHP projects easier, cleaner, and safer — **no frameworks required!**

---

## ✨ Key Features

- 🔐 Safe prepared statements with parameter binding  
- 🔁 Full transaction control: <code>start()</code> / <code>finish()</code> / <code>stop()</code>  
- 📋 Fetch one or many rows easily  
- 📂 Read cached JSON files for fast offline access  
- ⚙ Get server variables like <code>max_connections</code>  
- 🌐 UTF-8 charset by default  
- 🧩 Fully standalone — no dependencies!

---

## 🚀 Quick Start

### 📦 Initialize the class

<pre><code>
require_once 'database.php';
$db = new SimpleMySQL();
</code></pre>

---

### 🔍 Fetch a single row

<pre><code>
$user = $db->fetch("SELECT * FROM users WHERE id = ?", [1]);
echo $user['name'];
</code></pre>

---

### 📄 Fetch multiple rows

<pre><code>
$users = $db->fetchAll("SELECT * FROM users WHERE status = ?", ['active']);
foreach ($users as $user) {
    echo $user['email'] . "&lt;br&gt;";
}
</code></pre>

---

### 📝 Execute insert / update / delete

<pre><code>
$db->execute("UPDATE users SET role = ? WHERE id = ?", ['admin', 3]);
</code></pre>

---

### 🆔 Get last inserted ID

<pre><code>
$db->execute("INSERT INTO logs (message) VALUES (?)", ['User added']);
$id = $db->lastInsertId();
</code></pre>

---

### 🔁 Transaction example

<pre><code>
$db->start();

try {
    $db->execute("DELETE FROM sessions WHERE user_id = ?", [2]);
    $db->execute("UPDATE users SET status = ? WHERE id = ?", ['inactive', 2]);
    $db->finish(); // ✅ commit
} catch (Exception $e) {
    $db->stop(); // ❌ rollback
}
</code></pre>

---

### 📥 Read data from JSON cache

<pre><code>
$data = $db->readCache('cache/data.json');
if ($data) {
    foreach ($data as $row) {
        echo $row['title'] . "&lt;br&gt;";
    }
}
</code></pre>

---

### ⚙ Get MySQL server variable

<pre><code>
echo "Max Connections: " . $db->getVariable("max_connections");
</code></pre>

---

### ❎ Close connection

<pre><code>
$db->close();
</code></pre>

---

## ✅ When to Use It?

- You need a lightweight PHP tool to connect to MySQL ✅  
- You don’t want heavy frameworks ❌  
- You want safety and clarity 🔐  
- You just want to get things done 🧠

---

## 📄 License

MIT — free to use and modify.

> Built with ❤️ by <strong>Temirkhan</strong>  
> <a href="https://www.instagram.com/temirkhanrustemov/">@temirkhanrustemov</a> • <code>temirkhan.onyx@gmail.com</code>
