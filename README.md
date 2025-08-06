<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Contact Form</title>
</head>
<body>
  <h2>Contact Us</h2>
  <form id="contactForm">
    <input type="text" name="name" placeholder="Your Name" required /><br><br>
    <input type="email" name="email" placeholder="Your Email" required /><br><br>
    <textarea name="message" placeholder="Your Message" required></textarea><br><br>
    <button type="submit">Send</button>
  </form>

  <script>
    document.getElementById('contactForm').addEventListener('submit', async function(e) {
      e.preventDefault(); // Page reload hone se roke

      // Form data ko object me le lo
      const formData = {
        name: this.name.value,
        email: this.email.value,
        message: this.message.value
      };

      try {
        // Backend ko POST request bhejo
        const response = await fetch('http://localhost:3000/contact', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(formData)
        });

        const result = await response.json();

        // User ko message dikhao
        alert(result.message);

        // Form clear kar do
        this.reset();
      } catch (error) {
        alert('Error sending message!');
        console.error(error);
      }
    });
  </script>
</body>
</html>
