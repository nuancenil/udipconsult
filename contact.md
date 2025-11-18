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

<form id="comment-form">
  <p>
    <label>您的稱呼：<br>
      <input
        type="text"
        id="name"
        name="name"
        required
        maxlength="40"
        autocomplete="off">
    </label>
  </p>
  <p>
    <label>Email（必填，不會公開顯示，只用於回覆）：<br>
      <input
        type="email"
        id="email"
        name="email"
        required
        maxlength="100"
        autocomplete="off">
    </label>
  </p>
  <p>
    <label>留言內容：<br>
      <textarea
        id="message"
        name="message"
        required
        maxlength="500"
        rows="6"
        style="height: 180px;"></textarea>
    </label>
    </p>
    <p style="display:none;">
    <label>請留空：<br>
    <input type="text" id="honeypot" name="honeypot">
    </label>
    </p>
    <p>
        <button type="submit">送出留言</button>
    </p>
</form>


<div id="comments"></div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
  import { 
    getFirestore, collection, addDoc, onSnapshot,
    query, orderBy, serverTimestamp, limit
  } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";

  // 這裡用你現在那段 firebaseConfig，直接貼過來就好
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

  const form = document.getElementById("comment-form");
  const commentsDiv = document.getElementById("comments");
  const nameInput = document.getElementById("name");
  const emailInput = document.getElementById("email");
  const msgInput = document.getElementById("message");
  const honeypotInput = document.getElementById("honeypot");
  const button = form.querySelector("button[type=submit]");

  function maskName(name) {
    if (!name) return "匿名";
    const trimmed = name.trim();
    const firstChar = trimmed[0];
    return firstChar + "＊＊";
  }

  function formatTimestamp(ts) {
    if (!ts || !ts.toDate) return "";
    const d = ts.toDate();
    const yyyy = d.getFullYear();
    const mm = String(d.getMonth() + 1).padStart(2, "0");
    const dd = String(d.getDate()).padStart(2, "0");
    const hh = String(d.getHours()).padStart(2, "0");
    const mi = String(d.getMinutes()).padStart(2, "0");
    return `${yyyy}-${mm}-${dd} ${hh}:${mi}`;
  }

  // ★ 這一整段就是「submit 裡」會執行的程式
  form.addEventListener("submit", async (e) => {
    e.preventDefault();

    // 冷卻：按了之後 30 秒內不能再按
    if (button.disabled) return;

    const name  = nameInput.value.trim();
    const email = emailInput.value.trim();
    const msg   = msgInput.value.trim();
    const trap  = honeypotInput.value.trim(); // 蜜罐欄位

    // 如果蜜罐有被填，當作機器人，直接丟掉
    if (trap) {
      return;
    }

    // 三個必填欄位有任何一個空白，就不送
    if (!name || !email || !msg) {
      return;
    }

    button.disabled = true;

    await addDoc(commentsCol, {
      name,
      email,
      msg,
      createdAt: serverTimestamp()
    });

    nameInput.value = "";
    emailInput.value = "";
    msgInput.value = "";

    // 30 秒後可以再送
    setTimeout(() => {
      button.disabled = false;
    }, 30000);
  });

  // 只抓最近 50 則留言
  const q = query(
    commentsCol,
    orderBy("createdAt", "desc"),
    limit(50)
  );

  onSnapshot(q, (snapshot) => {
    commentsDiv.innerHTML = "";
    snapshot.forEach((doc) => {
      const data = doc.data();
      const p = document.createElement("p");

      const safeName = maskName(data.name);
      const timeText = formatTimestamp(data.createdAt);

      p.textContent = `${safeName} 於 ${timeText} 留下一則訊息。`;
      commentsDiv.appendChild(p);
    });
  });
</script>
