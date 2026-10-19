---
layout: page
title: Contact
permalink: /contact
redirect_from:
  - /support
  - /contact/
comments: false
---

<form action="https://formspree.io/f/xqknondj" method="POST" id="contact-form">
<p class="mb-4" id="contact-intro">Please send your message to {{site.name}}. We will reply as soon as possible!</p>
<div class="form-group row">
<div class="col-md-6">
<input class="form-control" type="text" name="name" placeholder="Name*" required>
</div>
<div class="col-md-6">
<input class="form-control" type="email" name="_replyto" placeholder="E-mail Address*" required>
</div>
</div>

<input class="form-control mb-3" type="text" name="app-name" id="app-name" placeholder="App Name (optional)">
<input type="hidden" name="_subject" id="contact-subject" value="Contact from {{site.name}}">

<textarea rows="8" class="form-control mb-3" name="message" placeholder="Message*" required></textarea>
<input class="btn btn-dark" type="submit" value="Send">
</form>

<script>
(function () {
  var app = new URLSearchParams(window.location.search).get('app');
  if (!app) { return; }
  app = app.replace(/[^\w .&+'-]/g, '').trim().slice(0, 60);
  if (!app) { return; }
  var field = document.getElementById('app-name');
  field.value = app;
  field.readOnly = true;
  field.classList.add('bg-light');
  document.getElementById('contact-subject').value = app + ' support request';
  document.getElementById('contact-intro').textContent =
    'Ask us anything about ' + app + '. We will reply as soon as possible!';
})();
</script>
