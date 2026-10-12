<script setup>
const sendMessage = () => {
  alert('Pesan berhasil disiapkan. Ini masih contoh form praktikum.')
}
</script>

<template>
  <div class="content-page contact-page">
    <header class="page-header">
      <h1>Contact Us</h1>
      <p>We'd love to hear from you. Please fill out the form below or reach out via our contact info.</p>
    </header>

    <div class="contact-content">
      <div class="contact-info">
        <div class="info-item">
          <div class="info-icon">⌖</div>
          <div><h3>Our Office</h3><p>123 Event Street, Tech City, 10101</p></div>
        </div>
        <div class="info-item">
          <div class="info-icon">☎</div>
          <div><h3>Phone</h3><p>+62 812 3456 7890</p></div>
        </div>
        <div class="info-item">
          <div class="info-icon">✉</div>
          <div><h3>Email</h3><p>hello@gatherly.com</p></div>
        </div>
      </div>

      <div class="contact-form">
        <form @submit.prevent="sendMessage">
          <div class="form-group">
            <label for="name">Name</label>
            <input id="name" type="text" placeholder="John Doe" class="form-control" required />
          </div>
          <div class="form-group">
            <label for="email">Email</label>
            <input id="email" type="email" placeholder="john@example.com" class="form-control" required />
          </div>
          <div class="form-group">
            <label for="message">Message</label>
            <textarea id="message" placeholder="How can we help you?" rows="5" class="form-control" required></textarea>
          </div>
          <button class="btn btn-primary" type="submit">Send Message</button>
        </form>
      </div>
    </div>
  </div>
</template>
