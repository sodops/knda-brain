 [[DEVOPS]]
#### 1-qadam: Loyihani joylashtirish

ZIP faylni serverga (masalan, `/var/www/mysite` papkasiga) yuklang va oching:

Bash

```
sudo apt install unzip -y
sudo unzip site.zip -d /var/www/mysite
```

#### 2-qadam: Huquqlarni sozlash (Permissions)

Web-server (Nginx/Apache) fayllarni o'qishi va yozishi uchun egasini o'zgartiring:

Bash

```
sudo chown -R www-data:www-data /var/www/mysite
sudo find /var/www/mysite -type d -exec chmod 755 {} \;
sudo find /var/www/mysite -type f -exec chmod 644 {} \;
```

#### 3-qadam: Ma'lumotlar bazasini sozlash

Bazani yarating va `.sql` faylni import qiling:

Bash

```
mysql -u root -p
# MySQL ichida:
CREATE DATABASE site_db;
EXIT;

# Import qilish:
mysql -u root -p site_db < /path/to/backup.sql
```

#### 4-qadam: Konfiguratsiya (.env)

Loyihaning konfiguratsiya faylini (masalan, `.env`) tahrirlang:

Bash

```
cd /var/www/mysite
sudo nano .env
# Bu yerda DB_DATABASE, DB_USERNAME, DB_PASSWORD qismlarini to'g'rilang
```

#### 5-qadam: Nginx-ni sozlash

Yuqoridagi darsimizda ko'rganimizdek, `/etc/nginx/sites-available/` papkasida konfig yarating va saytni yoqing.

---

### 4. Siz nimalarni bilishingiz shart?

Haqiqiy DevOpschi sifatida sizda quyidagi "qurollar" bo'lishi kerak:

- **Linux (Ubuntu/Debian) CLI:** Fayllar bilan ishlash, SSH, huquqlar.
    
- **Nginx/Apache:** Virtual xostlarni sozlash.
    
- **PHP-FPM:** PHP protsesslarini boshqarish.
    
- **MySQL/MariaDB:** Baza yaratish va import/export.
    
- **Composer:** Agar loyiha Laravel yoki zamonaviy PHP-da bo'lsa, kutubxonalarni o'rnatish uchun (`composer install`).
    
- **Logs:** Muammo bo'lsa, `/var/log/nginx/error.log` va `/var/log/php-fpm.log` fayllarini o'qish va tahlil qilish.
    

> **Kichik maslahat:** ZIP faylni serverga yuklashdan oldin uni lokal kompyuteringizda ochib ko'ring. Ba'zan dasturchilar ZIP-ni shunday qilishadiki, ichida yana bitta papka bo'ladi (nested folders). Bu Nginx `root` yo'lini belgilashda adashtirishi mumkin.