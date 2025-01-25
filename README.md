# nginx-demo

This repository demonstrates a simple Nginx configuration to serve a static website. It contains three interlinked HTML pages and an Nginx configuration file.

## Files in this Repository

- `index.html`: The homepage of the site.
- `contact.html`: The contact page.
- `about.html`: The about page.
- `nginx.conf`: Nginx configuration file to set up the server.

## Prerequisites

Ensure you have the following:
- Nginx installed on your system.
- Access to the Nginx configuration directory (usually `/etc/nginx/`).
- Proper permissions to edit files and restart the Nginx service.

## Instructions to Set Up

### 1. Place the HTML Files
1. Copy the `index.html`, `contact.html`, and `about.html` files to your web root directory. For most systems, this is `/var/www/html/`. Use the following command:
   ```bash
   sudo cp index.html contact.html about.html /var/www/html/
   ```
2. Set appropriate permissions so that Nginx can serve the files:
   ```bash
   sudo chmod 644 /var/www/html/index.html /var/www/html/contact.html /var/www/html/about.html
   ```

### 2. Configure Nginx
1. Copy the `nginx.conf` file to the Nginx configuration directory:
   ```bash
   sudo cp nginx.conf /etc/nginx/sites-available/nginx-demo
   ```
2. Create a symbolic link in the `sites-enabled` directory:
   ```bash
   sudo ln -s /etc/nginx/sites-available/nginx-demo /etc/nginx/sites-enabled/
   ```
3. Test the Nginx configuration:
   ```bash
   sudo nginx -t
   ```
   If there are no errors, proceed to the next step.
4. Restart Nginx to apply the configuration:
   ```bash
   sudo systemctl restart nginx
   ```

### 3. Verify the Setup
1. Open your browser and visit `http://localhost/` to view the homepage.
2. Test navigation to the `about.html` and `contact.html` pages via the links on the homepage.

## Sample Nginx Configuration (nginx.conf)
```nginx
server {
    listen 80;
    server_name localhost;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

## Notes
- The three pages (`index.html`, `contact.html`, `about.html`) are interlinked. Make sure all files are in the same directory specified in the `root` directive of the Nginx configuration.
- Use `sudo` if your user does not have direct permissions for the Nginx directories.

## Future Enhancements
This is a basic setup. You can enhance it by:
- Adding SSL/TLS for secure connections.
- Setting up a custom 404 page.
- Configuring Nginx to serve dynamic content using a backend like PHP or Node.js.

---

Happy learning with Nginx! If you encounter any issues, feel free to open a discussion or raise an issue in this repository.

