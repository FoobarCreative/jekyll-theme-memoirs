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
<textarea name="diagnostics" id="diagnostics" hidden></textarea>
<p class="text-muted small mb-3" id="diag-note" hidden></p>

<textarea rows="8" class="form-control mb-3" name="message" placeholder="Message*" required></textarea>
<input class="btn btn-dark" type="submit" value="Send">
</form>

<script>
(function () {
  var params = new URLSearchParams(window.location.search);
  function clean(key, max) {
    var v = params.get(key);
    if (!v) { return ''; }
    return v.replace(/[^\w .,:$()+-]/g, '').trim().slice(0, max);
  }
  var app = clean('app', 60);
  if (app) {
    var field = document.getElementById('app-name');
    field.value = app;
    field.readOnly = true;
    field.classList.add('bg-light');
    document.getElementById('contact-subject').value = app + ' support request';
    document.getElementById('contact-intro').textContent =
      'Ask us anything about ' + app + '. We will reply as soon as possible!';
  }
  var version = clean('version', 20);
  var build = clean('build', 20);
  var device = clean('device', 40);
  var os = clean('os', 40);
  var rows = [
    ['App', app],
    ['Version', version],
    ['Build', build],
    ['Device', device],
    ['OS', os],
    ['Install ID', clean('installId', 64)],
    ['RevenueCat ID', clean('rcid', 80)]
  ].filter(function (row) { return row[1]; });
  if (rows.length < 2) { return; }
  document.getElementById('diagnostics').value =
    rows.map(function (row) { return row[0] + ': ' + row[1]; }).join('\n');
  var summary = [];
  if (version) { summary.push('v' + version + (build ? ' (' + build + ')' : '')); }
  else if (build) { summary.push('build ' + build); }
  if (device) { summary.push(device); }
  if (os) { summary.push(os); }
  var note = document.getElementById('diag-note');
  note.textContent = 'Diagnostic info attached' + (summary.length ? ': ' + summary.join(', ') : '') + '.';
  note.hidden = false;
})();
</script>
