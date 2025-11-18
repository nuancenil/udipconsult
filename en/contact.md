---
layout: default
title: Contact
lang: en
zh_url: /contact/
permalink: /en/contact/
---

If you would like to discuss a project or potential collaboration, feel free to contact us:

- Email: [genius@eudaimonia-ip.com](mailto:genius@eudaimonia-ip.com)

You can also leave a short description (target market, technology area, timeline and budget).
We will get back to you within 2 business days.

## Leave us a message

<div id="comments"></div>

<form id="comment-form">
  <p>
    <label>Your name:<br>
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
    <label>Email (required, will not be shown publicly; used only to reply to you):<br>
      <input
        type="email"
        id="email"
        name="email"
        required
        maxlength="100"
        autocomplete="off">
    </label>
  </p>
  <p style="display:none;">
    <label>Please leave this field empty:<br>
      <input
        type="text"
        id="honeypot"
        name="honeypot"
        autocomplete="off">
    </label>
  </p>
  <p>
    <label>Your message:<br>
      <textarea
        id="message"
        name="message"
        required
        maxlength="500"
        rows="6"></textarea>
    </label>
  </p>
  <p>
    <button type="submit">Send message</button>
  </p>
</form>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
  import { 
    getFirestore, collection, addDoc, onSnapshot,
    query, orderBy, serverTimestamp, limit
  } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";

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
    if (!name) return "Anonymous";
    const trimmed = name.trim();
    const firstChar = trimmed[0];
    return firstChar + "**";
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

  form.addEventListener("submit", async (e) => {
    e.preventDefault();

    if (button.disabled) return;

    const name  = nameInput.value.trim();
    const email = emailInput.value.trim();
    const msg   = msgInput.value.trim();
    const trap  = honeypotInput.value.trim();

    // If the hidden field is filled, treat it as a bot and ignore
    if (trap) {
      return;
    }

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

    setTimeout(() => {
      button.disabled = false;
    }, 30000);
  });

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

      p.textContent = `${safeName} left a message at ${timeText}.`;
      commentsDiv.appendChild(p);
    });
  });
</script>
