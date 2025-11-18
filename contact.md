---
layout: default
title: 聯絡我們
lang: zh
en_url: /en/contact/
permalink: /contact/
---



如果你想與我們討論項目或合作，歡迎來信：
- Email：[genius@eudaimonia-ip.com](mailto:genius@eudaimonia-ip.com)

你也可以留下需求重點（目標市場、技術領域、時程與預算），我們會在 2 個工作日內回覆。

## 留言給我們

<div id="comments"></div>

<form id="comment-form">
  <p>
    <label>您的稱呼：<br>
      <input type="text" id="name" required maxlength="40">
    </label>
  </p>
  <p>
    <label>留言內容：<br>
      <textarea id="message" required maxlength="500"></textarea>
    </label>
  </p>
  <p>
    <button type="submit">送出留言</button>
  </p>
</form>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
  import { 
    getFirestore, collection, addDoc, onSnapshot,
    query, orderBy, serverTimestamp
  } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";

  // 🔹 在這一行下面貼上你從 Firebase 拿到的那段 firebaseConfig
  const firebaseConfig = {
  apiKey: "AIzaSyCdgL9VmR4U54lU8ovgezaADJNNSq_Mg9w",
  authDomain: "udip-comments-web.firebaseapp.com",
  projectId: "udip-comments-web",
  storageBucket: "udip-comments-web.firebasestorage.app",
  messagingSenderId: "642386138134",
  appId: "1:642386138134:web:ac05906d1af96eef7b5137",
  measurementId: "G-5B48YFYV3M"
};

  const app = initializeApp(firebaseConfig);
  const db = getFirestore(app);
  const commentsCol = collection(db, "comments");

  const commentsDiv = document.getElementById("comments");
  const form = document.getElementById("comment-form");
  const nameInput = document.getElementById("name");
  const msgInput = document.getElementById("message");

  form.addEventListener("submit", async (e) => {
    e.preventDefault();
    const name = nameInput.value.trim();
    const msg = msgInput.value.trim();
    if (!name || !msg) return;

    await addDoc(commentsCol, {
      name,
      msg,
      createdAt: serverTimestamp()
    });

    msgInput.value = "";
  });

  const q = query(commentsCol, orderBy("createdAt", "desc"));
  onSnapshot(q, (snapshot) => {
    commentsDiv.innerHTML = "";
    snapshot.forEach((doc) => {
      const data = doc.data();
      const p = document.createElement("p");
      p.innerHTML = `<strong>${data.name}</strong>：${data.msg}`;
      commentsDiv.appendChild(p);
    });
  });
</script>
