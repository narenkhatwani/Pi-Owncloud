
# Steps to deploy owncloud

**Step 1**

```bash
sudo apt-get update

sudo apt-get upgrade
```

[https://lh3.googleusercontent.com/9l22r_3rpuj45HYlhSNoX2ld6XqOBAWkMIGMQxjc5v0jG2dBYtFUYeJrkGrbKskV8achk-M6qh9F3jhu7bNAF7areXDXMs3cdOEoIhkKsquS7Ar6CN4H4z9oIj4pHeEgrolEiNJA](https://lh3.googleusercontent.com/9l22r_3rpuj45HYlhSNoX2ld6XqOBAWkMIGMQxjc5v0jG2dBYtFUYeJrkGrbKskV8achk-M6qh9F3jhu7bNAF7areXDXMs3cdOEoIhkKsquS7Ar6CN4H4z9oIj4pHeEgrolEiNJA)

**Step 2**

```bash
sudo apt-get install apache2 libapache2-mod-php7.2 openssl php-imagick php7.2-common php7.2-curl php7.2-gd php7.2-imap php7.2-intl php7.2-json php7.2-ldap php7.2-mbstring php7.2-mysql php7.2-pgsql php-smbclient php-ssh2 php7.2-sqlite3 php7.2-xml php7.2-zip
```

**Step 3 - Check Apache installation**

```bash
sudo dpkg -l apache2
```

[https://lh4.googleusercontent.com/Ckk2RwqroGhuDTppN7NznhrjhighRuTppVtRaeoVnncVy_MRwz5PJ8h227rfdw1xPprvZmMDdU55YtMNQ97zS0kXCOZ0QkdmuteTutZ7ZUcsJQZUpdlLGzTPPFMNqskbw3E3lM2v](https://lh4.googleusercontent.com/Ckk2RwqroGhuDTppN7NznhrjhighRuTppVtRaeoVnncVy_MRwz5PJ8h227rfdw1xPprvZmMDdU55YtMNQ97zS0kXCOZ0QkdmuteTutZ7ZUcsJQZUpdlLGzTPPFMNqskbw3E3lM2v)

**Step 4 - Enable apache to start on boot**

```bash
sudo systemctl start apache2

sudo systemctl enable apache2
```

[https://lh5.googleusercontent.com/ZtxR96bl-YffNHctW5DgLVLtDjPOovjujZMjB9elMB_34nncFWjIJXMEnoCVL297eKCywq4u7-nrXQXVopk2CsqIsCbJx_CNOYak3dj27Y3fBujZxNmvnInSVIIwaLDwfsgqFZj5](https://lh5.googleusercontent.com/ZtxR96bl-YffNHctW5DgLVLtDjPOovjujZMjB9elMB_34nncFWjIJXMEnoCVL297eKCywq4u7-nrXQXVopk2CsqIsCbJx_CNOYak3dj27Y3fBujZxNmvnInSVIIwaLDwfsgqFZj5)

**Step 5 - Check if the server is working or not**

https:/server-ip

Write this in your URL bar and check if the server is working or not

**In my case 192.168.0.182**

[https://lh4.googleusercontent.com/PAuX1tODFWsXnBMC8WMyyyfn8LYNlP5TLGWlXP8jhnOonJT4GKTOOiFL0i29O446u2mJT1ugxz7qUiDlMrKayFEa7A-Lu08OInkaIqygfQag1R1EYbfPUL8bmRtpC6UD7rXfznPm](https://lh4.googleusercontent.com/PAuX1tODFWsXnBMC8WMyyyfn8LYNlP5TLGWlXP8jhnOonJT4GKTOOiFL0i29O446u2mJT1ugxz7qUiDlMrKayFEa7A-Lu08OInkaIqygfQag1R1EYbfPUL8bmRtpC6UD7rXfznPm)

**Step 6 - Check if php installed**

```bash
php -v
```
