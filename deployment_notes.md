What changed

  Calendly replaces the fake calendar. The widget auto-themes to match the site's dark gold palette via URL params
  (background_color=111118, primary_color=C9A84C). The chatbot's "open calendar" action still scrolls to #agenda — that still works
  correctly.

  To activate it, your girlfriend needs to:
  1. Go to calendly.com → sign up free
  2. Create an event type: "Consulta inicial" (30 min, Mon–Sat 9–19hs)
  3. Copy her username (e.g., marialuz-hmr)
  4. In the HTML, replace TU-USUARIO-CALENDLY with that username on this line:
  data-url="https://calendly.com/TU-USUARIO-CALENDLY?..."

  ---
  Deployment checklist (Hetzner)

  # 1. On Hetzner Cloud: create CX22 server, Ubuntu 24.04
  # 2. SSH in, then:
  ssh -i ~/.ssh/id_gcs root@204.168.180.32
  apt update && apt install -y nginx certbot python3-certbot-nginx

  # 3. Upload the HTML file
  scp estudio_juridico.html root@204.168.180.32:/var/www/html/index.html

  # 4. Point your .com.ar domain registrar's A record → YOUR-HETZNER-IP
  #    Wait for DNS propagation (5–30 min)

  # 5. Get SSL certificate
  certbot --nginx -d hmrestudio.com.ar -d www.hmrestudio.com.ar

  # Done. Nginx auto-renews the cert via systemd timer.

  Total monthly cost: ~€4 for the VPS + domain renewal (varies by registrar). That's it.

  ## useful ssh commands
  ssh -i ~/.ssh/id_gcs root@204.168.180.32
  scp -i ~/.ssh/id_gcs estudio_juridico.html root@204.168.180.32:/var/www/html/index.html   
