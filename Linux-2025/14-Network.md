# פעולות רשת בלינוקס - מדריך מקיף

## הגדרות רשת בסיסיות

### בדיקת מצב רשת
```bash
# הצגת כל ממשקי הרשת
ip addr show
ifconfig

# בדיקת חיבור רשת
ping google.com
ping -c 4 8.8.8.8

# הצגת טבלת ניתוב
ip route show
route -n

# בדיקת שמות DNS
cat /etc/resolv.conf
```

### הגדרת ממשק רשת
```bash
# הגדרת כתובת IP
sudo ip addr add 192.168.1.100/24 dev eth0
sudo ifconfig eth0 192.168.1.100 netmask 255.255.255.0

# הפעלה/כיבוי ממשק
sudo ip link set eth0 up
sudo ip link set eth0 down

# הגדרת DNS
sudo nano /etc/resolv.conf
```

## כלי רשת בסיסיים

### בדיקת קישוריות
```bash
# בדיקת מסלול חבילות
traceroute google.com
tracepath google.com

# בדיקת זמן תגובה
ping -c 4 google.com

# בדיקת DNS
nslookup google.com
dig google.com
```

### הורדת קבצים
```bash
# הורדה עם wget
wget https://example.com/file.txt
wget -c https://example.com/file.txt    # המשך הורדה שנקטעה
wget -r https://example.com             # הורדה רקורסיבית

# הורדה עם curl
curl -O https://example.com/file.txt
curl -C - -O https://example.com/file.txt  # המשך הורדה שנקטעה
```

## עבודה עם SSH

### התחברות מרחוק
```bash
# התחברות בסיסית
ssh user@hostname

# התחברות עם פורט ספציפי
ssh -p 2222 user@hostname

# התחברות עם מפתח
ssh -i ~/.ssh/id_rsa user@hostname

# העברת X11
ssh -X user@hostname
```

### העברת קבצים
```bash
# העתקת קובץ למחשב מרוחק
scp file.txt user@hostname:/path/to/destination

# העתקת קובץ ממחשב מרוחק
scp user@hostname:/path/to/file.txt local_directory

# העתקת תיקייה
scp -r directory user@hostname:/path/to/destination
```

### הגדרות SSH
```bash
# יצירת מפתחות
ssh-keygen -t rsa -b 4096

# העברת מפתח ציבורי
ssh-copy-id user@hostname

# קובץ הגדרות SSH
nano ~/.ssh/config

# דוגמה לקובץ הגדרות:
Host server1
    HostName example.com
    User username
    Port 2222
    IdentityFile ~/.ssh/id_rsa
```

## ניטור רשת

### ניטור תעבורה
```bash
# הצגת חיבורים פעילים
netstat -tuln
ss -tuln

# ניטור תעבורה בזמן אמת
iftop
nethogs

# הצגת סטטיסטיקות רשת
vnstat
```

### Wireshark
```bash
# התקנה
sudo apt install wireshark

# הרשאות
sudo usermod -aG wireshark $USER

# שימוש בסיסי:
1. בחר ממשק רשת
2. התחל הקלטה
3. הגדר פילטרים (למשל: tcp port 80)
4. נתח את התעבורה
```

## הגדרת שרתים

### שרת Apache
```bash
# התקנה
sudo apt install apache2

# הפעלה/עצירה
sudo systemctl start apache2
sudo systemctl stop apache2

# הגדרת תיקיות
DocumentRoot: /var/www/html
Configs: /etc/apache2/
```

### שרת Nginx
```bash
# התקנה
sudo apt install nginx

# הפעלה/עצירה
sudo systemctl start nginx
sudo systemctl stop nginx

# הגדרת תיקיות
DocumentRoot: /var/www/html
Configs: /etc/nginx/
```

## אבטחת רשת

### חומת אש (UFW)
```bash
# התקנה
sudo apt install ufw

# פקודות בסיסיות
sudo ufw enable
sudo ufw disable
sudo ufw status

# הוספת חוקים
sudo ufw allow 22
sudo ufw deny 80
sudo ufw allow from 192.168.1.0/24
```

### בדיקות אבטחה
```bash
# סריקת פורטים
nmap localhost
nmap -sV hostname

# בדיקת SSL
openssl s_client -connect hostname:443

# בדיקת תעודות
ssl-cert-check -s hostname
```

## פתרון בעיות

### בעיות תקשורת
```bash
# בדיקת חיבור רשת
ping gateway
ip route get 8.8.8.8

# בדיקת DNS
dig +trace google.com
host google.com

# בדיקת פורטים
telnet hostname 80
nc -zv hostname 80
```

### בעיות SSL/TLS
```bash
# בדיקת תעודה
openssl x509 -in cert.pem -text

# בדיקת תוקף
openssl x509 -enddate -noout -in cert.pem

# בדיקת שרשרת תעודות
openssl verify -CAfile chain.pem cert.pem
```

### רישום ודיבוג
```bash
# צפייה בלוגים של מערכת
journalctl -u networking
tail -f /var/log/syslog

# צפייה בלוגי אפאצ'י
tail -f /var/log/apache2/access.log
tail -f /var/log/apache2/error.log

# דיבוג DNS
dig +trace google.com
dig +short google.com
```

## טיפים מתקדמים

### טונלים SSH
```bash
# העברת פורט מקומי
ssh -L 8080:localhost:80 user@hostname

# העברת פורט מרוחק
ssh -R 8080:localhost:80 user@hostname

# טונל SOCKS
ssh -D 8080 user@hostname
```

### סקריפטים שימושיים
```bash
# בדיקת זמינות שרת
#!/bin/bash
while true; do
    ping -c 1 server >/dev/null && echo "Up" || echo "Down"
    sleep 60
done

# ניטור שימוש ברוחב פס
#!/bin/bash
while true; do
    ifconfig eth0 | grep bytes
    sleep 1
done
```
