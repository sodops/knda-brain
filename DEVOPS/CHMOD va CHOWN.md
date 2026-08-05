[[LINUX]]

# CHMOD - Change Mod
Tizimdagi Fayllarning katologlarning  ruhsatlarini o'zgartirish uchun foydalaniladigan buyruq

- **r (read)** = 4
- **w (write)** = 2
- **x (execute)** = 1
- **- (hech narsa)** = 0
e.g :
    **`-(rw-)(r--)(r--)`**
    1. "-"  fayl turi
    2. 1- bracket - Ega(owner)
	     - 4 + 2 + 0 = 6 
	     - 4 + 0 + 0 = 4   ==>    644
	     - 4 + 0 + 0 = 4
Ko'pincha havsizlik jihatdan serverlarda **755** - folderlar uchun
664 - fayllar uchun ruhsat beriladi


# CHOWN - Change Owner 
fayl yoki katalogning egasini o'zgartirish uchun ishlatiladi









#### 1. Farqi nimada?

- **`chown` (Change Owner):** Bu "Fayl **kimniki**?" degan savolga javob beradi.
    > Masalan: "Bu uy Sodiqniki".
- **`chmod` (Change Mode):** Bu "Egasining yoki boshqalarning **nima qilishga haqqi bor**?" degan savolga javob beradi.
    
    > Masalan: "Sodiq uyni bo'yay oladi (write), mehmonlar esa faqat ko'ra oladi (read)".

---

### 2. Faqat `chmod` bilan qilsa bo'lmaydimi?

Nazariy jihatdan bo'ladi, lekin bu **xavfsizlik uchun juda yomon**.

Agar siz `chown` qilmasdan, Nginx saytni o'qishi uchun `chmod 777` (hamma narsa qilishga hamma uchun ruxsat) bersangiz:

1. Serverdagi har qanday foydalanuvchi sizning kodingizni o'chirib yuborishi yoki o'zgartirishi mumkin.
    
2. Xakerlar bitta teshik topsa, butun tizimga o'tishlari osonlashadi.
    

**To'g'ri strategiya:** Uyning (faylning) kalitini faqat u bilan ishlaydigan odamga (`www-data`) berish (`chown`) va unga faqat kerakli ruxsatlarni berish (`chmod`).