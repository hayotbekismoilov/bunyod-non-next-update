NONVOYXONA ERP TIZIMI:
## 1. LOYIHANING IJROCHI HAQIDA UMUMIY MA'LUMOT

### 1.1 Loyiha nomi

### 1.2 Loyiha toifasi

Non ishlab chiqarish korxonalari uchun korporativ darajadagi monolit CRM/ERP/POS platformasi.

### 1.3 Rivojlanish standarti

Ushbu dastur Django REST Frameworksiz, Reactsiz, Node.jssiz va tashqi SPA bog'liqlikisiz sof Django 5/6 arxitekturasidan foydalangan holda to'liq server tomonida ko'rsatiladigan monolit sifatida ishlab chiqilishi kerak.

### 1.4 Asosiy texnologiya to'plami* Shtrix-kodni skanerlash mexanizmi: JavaScript kamerasi/USB skanerini o‘quvchi
* Termal kvitansiya mexanizmi: ESC/POS printerini qo‘llab-quvvatlash
* Diagrammalar: Chart.js CDN
* Ko‘p tilli vosita: Django i18n + maxsus tilni o‘zgartiruvchi
* Joylashtirish: Linux VPS/Nginx/Gunicorn/PostgreSQL

### 1.5 Asosiy maqsad* Onlayn savdoga tayyorlik kengaytirilishi mumkin

---

## 3. GLOBAL TIZIM MODULLARI

 Loyihada quyidagi Django ilovalari mavjud:

1. asosiy
2. hisoblar
3. mahsulotlar
4. ishlab chiqarish
5. inventar
6. filiallar
7. pos
8. buxgalteriya hisobi
9. kadrlar bo'limi
10. attendance_ai
11. bildirishnomalar
12. integratsiyalar
13. hisobotlar
14. settings_app

Har bir ilova mustaqil boʻlishi kerak:

* models.py
* views.py
* urls.py
* forms.py
* services.py
* shablonlar papkasi
* admin.py
* kerak bo'lganda signals.py

---

## 4. AUTHENTICATION VA KIRISHNI BOSHQARISH MODULI

### 4.1 Tizimga kirish talabi

Tizim hech qanday ichki sahifani autentifikatsiyasiz ko‘rsatmasligi kerak.
Faqat superadmin yoki administrator tomonidan yaratilgan foydalanuvchilar quyidagi ma’lumotlar yordamida tizimga kirishi mumkin:

* foydalanuvchi nomi/login
* parol

### 4.2 Kirish Oqimi

Foydalanuvchi hisobga olish ma'lumotlarini kiritadi -> Django autentifikatsiyasi tasdiqlanadi -> rol ruxsati yuklanadi -> boshqaruv paneli ko'rsatiladi.

### 4.3 Foydalanuvchi rollari

Tizim rolga asoslangan kirishni boshqarishni qo'llab-quvvatlashi kerak:

* Super Admin
* Bosh direktor
* Ishlab chiqarish menejeri
* Ombor mudiri
* Kassir
* Filial sotuvchisi
* Buxgalter
* HR menejeri
* Kuzatuvchi/Faqat o'qish uchun

### 4.4 Ruxsat berish mantig'i

Har bir menyu va har bir CRUD operatsiyasi rolga qarab cheklanishi kerak.

---

## 5. TO'LIQ KO'P TILLI TALAB

Mijoz ko'radigan butun interfeys quyidagilarni qo'llab-quvvatlashi kerak:

* O'zbek lotin
* O'zbek kirill alifbosi
* Rus tili

Foydalanuvchi panelida tarjima qilinmagan inglizcha matnga ruxsat berilmaydi.

Misollar:

* Filial -> Filial / Filial
* Mahsulot qo'shish -> Mahsulot qo'shish / Mahsulot qo'shish
* Qabul qilingan -> Qabul qilindi / Qabul qilindi

Tilni o'zgartirgich yuqori navigatsiyada ko'rinadigan bo'lishi kerak.
Barcha yorliqlar, tugmalar, shakl o'rinlari, jadval sarlavhalari, modal sarlavhalar, ogohlantirishlar, chop etish kvitansiyalari va hisobotlari dinamik ravishda tarjima qilinishi kerak.

---

## 6. MAHSULOTLARNI BOSHQARISH MODULI

### 6.1 Talab

Tizim administratorga interfeysdan mahsulotlarni qo'lda yaratishga imkon berishi kerak.
Mavhum kodlangan mahsulotlar ro'yxatiga ruxsat berilmaydi.

### 6.2 Mahsulot yaratish uchun shakl maydonlari

* mahsulot_nomi_uzlotin
* mahsulot_nomi_kirillcha
* mahsulot_nomi_ru
* shtrix-kod
* turkum
* savdo_narxi_naqd pul
* savdo_narxi_terminal
* savdo_narxi_onlayn
* ishlab chiqarish_narxi
* birlik_turi(parcha/kg)
* faol_holat
* mahsulot_tasvir(ixtiyoriy)

### 6.3 Shtrix-kod talabi

Har bir mahsulot noyob shtrix-kodga ega bo'lishi kerak.
Shtrix-kodni qo‘lda kiritish yoki avtomatik tarzda yaratish mumkin.
Shtrix-kodni chop etish yorlig‘i funksiyasi kiritilishi kerak.

---

## 7. XOM ASHYO INVENTARIZASI + ETKAZIB BERUVCHI MODULI

Administrator UI dan xom ashyo yaratishi kerak:

* Un
* Yog'
* Tuz
* Xamirturush
* Susan
* Gaz
* Suv bilan bog'liq sarf materiallari
* Qadoqlash va boshqalar.

Shakl maydonlarini yaratish:

* material_name (3 tilda)
* o'lchov birligi
* minimal zaxira haqida ogohlantirish
* joriy zaxira
* sotib olish narxi
* yetkazib beruvchi

Yetkazib beruvchidan xomashyo olish quyidagilarni talab qiladi:

* zaxirani ko'paytirish
* to'lanmagan taqdirda yetkazib beruvchiga to'lanadigan mablag'ni yaratish
* buxgalteriya operatsiyasini yaratish

---

## 8. ISHLAB CHIQARISHNI AVTOMATLASHTIRISH MODULI

Ishlab chiqarish menejeri quyidagilarni kiritadi:

* mahsulot
* ishlab chiqarish miqdori
* novvoy
* smena
* ishlab chiqarish sanasi va vaqti

Tizim avtomatik ravishda:

1. Retseptlar jadvalini o'qiydi
2. Xom ashyoni chegirib tashlaydi
3. Tayyor mahsulot zaxirasini qo'shadi
4. Non ishlab chiqarishning ish haqi miqdorini hisoblab chiqadi
5. Ishlab chiqarish daftarini yozadi

Ishlab chiqarish tasdiqlangandan keyin qo'lda zaxirani tahrirlashga ruxsat berilmaydi, ma'mur tomonidan bekor qilingan hollar bundan mustasno.

---

## 9. SMART POS BARCODE SOTISH MODULI

### 9.1 POS interfeysi

Tezkor sensorli kassa ekrani.

### 9.2 Shtrixli kodni sotish mantig'i

Kassir shtrix-kodni quyidagi vositalar orqali skanerlaydi:

* USB shtrix-kod skaneri YOKI
* kamera shtrix-kod JS skaneri

Tizim avtomatik ravishda:

* mahsulotni aniqlaydi
* belgilangan narxni oladi
* sotuv savatiga qo'shiladi
* qayta skanerlangan bo'lsa, miqdorni oshiradi

### 9.3 To'lov usullari

* Naqd pul
* Terminal
* Bosish
* Payme
* Aralash to'lov (kelajakda ixtiyoriy)

 Ma'mur ruxsati bo'lmasa, kredit sotishga ruxsat berilmaydi.

### 9.4 Sotish tugallanishi

To'liq sotilgan:

* tayyor mahsulotlar chegirib tashlandi
* tanlangan kassa apparatiga pul qo'shildi
* buxgalteriya daftaridagi tranzaksiya yaratildi
* chek raqami yaratildi
* chop etiladigan chek yaratildi

---

## 10. TERMAL Kvitansiyalarni chop etish moduli

Tizim ESC/POS termal printerini qo'llab-quvvatlashi kerak.

Har bir sotuvdan keyin kassir quyidagi amallarni bajarishi mumkin:
Kvitansiyani chop etish

Kvitansiyada quyidagilar mavjud:

* nonvoyxona nomi
* kassir
* sana va vaqt
* sotilgan mahsulotlar
* miqdor
* narxlar
* jami
* toʻlov turi
* tanlangan tildagi rahmat matni
* QR/buyurtma kodi ixtiyoriy

Kun oxiridagi Z-hisobotni chop etish mumkin.

---

## 11. FACE ID XODIMLARNING QATNASHI CRM MODULI

Bu kadrlar bo'yicha majburiy aqlli boshqaruv quyi tizimidir.

### 11.1 Xodimning yuzini ro'yxatdan o'tkazish

Har bir xodim profilida quyidagilar bo'lishi kerak:

* 1-fotosurat to'plami
* 2-fotosurat to'plami
* 3-fotosurat to'plami
* yuzni kodlash vektorlari

### 11.2 Kameraning kelish terminali

Nonvoyxonaga kiraverishda xodim veb-kamera/planshet oldida turadi.
Tizim yuzni taniydi va belgilaydi:

* kelgan vaqt
* ketish vaqti

### 11.3 Avtomatik intizomni aniqlash

Tizim haqiqiy vaqtni belgilangan smena bilan taqqoslaydi.

Hisoblash kerak:

* o'z vaqtida
* X daqiqaga kechikib
* X daqiqaga erta chiqib ketgan
* yo'q

### 11.4 Administrator ogohlantirishlari

Agar xodim:

* kelmagan bo'lsa
* belgilangan vaqtdan kechikib
* vaqtdan oldin qoldirilgan

tizim avtomatik ravishda administrator boshqaruv paneli haqida bildirishnoma yuboradi.

Bildirishnoma misollari:
"Xamir qoruvchi Sobir 27 daqiqa kechikdi"
"Sotuvchi Dilnoza smenaga kelmadi"

---

## 12. FILIALLAR BO'YICHA TAQSIMLASH + REJALI FAKTLARNI NAZORAT

Markaziy ombor raqamli nakladnaya yordamida mahsulotlarni filiallarga jo'natadi.

Holatlarni uzatish:

* Loyiha
* Tranzitda
* Qabul qilindi

Filial qabul qilinganligini tasdiqlaganidan keyin:

* markaziy zaxiralar kamayadi
* filial zaxiralari ko'payadi

Filial nazorati kun oxirida:
Yuborilgan = sotilgan + qaytarilgan + qolgan
Agar nomuvofiqlik bo'lsa -> defitsit haqida ogohlantirish.

---

## 13. HISOB VA NAQD PUL KITOBI MODULI

Kassa registrlari:

* Asosiy kassa
* Terminal kassa
* Xarajat uchun kassa
* Onlayn to'lov uchun kassa

Har bir pul harakati o'zgarmas daftar tranzaksiyasini yaratishi kerak.

14. Tizim kuzatadigan ma'lumotlar:

* yetkazib beruvchining qarzi
* xarajatlar
* ish haqi to'lovlari
* filial yig'imlari
* POS daromadi
* kassalararo o'tkazmalar

P&L boshqaruv panelini avtomatik ravishda ishga tushirish talab qilinadi.

---

## ONLAYN SOTISH INTEGRATSIYA MODULI

Tizim arxitekturasi tashqi onlayn buyurtma manbalariga tayyor bo'lishi kerak:

* Telegram bot buyurtmalari
* Veb-sayt buyurtmalari
* Marketplace buyurtmalari
* Yetkazib berish bo'yicha hamkor buyurtmalari

Integratsiyalashgan buyurtmalar yagona savdo navbati ichida paydo bo'lishi kerak.

Tovar zaxirasi bir xil inventardan kamayishi kerak.

---

## 15. REAL VAQTDA XABARLAR MARKAZI

Dashboard topbar xabar mexanizmi ko'rsatish kerak:

* kam aktsiyalar haqida ogohlantirishlar
* xodimlar yo'q
* kechiktirilgan xodimlar
* to'lanmagan yetkazib beruvchi qarz eslatmalar
* filial taqchilligi
* muvaffaqiyatsiz transferlar
* printer xatolari(ixtiyoriy)

---

16## TO'LIQ CRUD TALABI (MUHIM)

Hech bir modul mavhum bo'lib qolmasligi kerak.
Har bir bo'limda quyidagilar bo'lishi kerak:

* Yangi ob'ekt yaratish
* Ob'ektni tahrirlash
* Ob'ektni o'chirish (ruxsatga asoslangan)
* Tafsilotlarni ko'rish
* Qidiruv/filtrlash

Admin UI-dan qo'lda yaratishi kerak:

* mahsulotlar
* xom ashyo
* filiallar
* yetkazib beruvchilar
* xodimlar
* retseptlar
* xarajatlar toifalari
* foydalanuvchilar
* kassa apparatlari
* ish haqi qoidalari
* onlayn kanallar

---

## 17. FRONTEND UI/UX STANDARTI

Dizayn uslubi yuqori darajadagi korporativ boy estetik bo'lishi kerak:

* shisha kartalar
* yon panel navigatsiyasi
* yumshoq soyalar
* nafis shakllar
* sezgir jadvallar
* modal yaratish oynalari
* ajax mini o'zaro ta'sirlari
* tezkor POS tugmalari
* planshetlar uchun qulay bo'lgan tashrif kamerasi sahifasi

Bootstrap shablonini klonlash hissi yo'q.
Maxsus ERP hissi bo'lishi kerak.

---
## 18. RIVOJLANISH
Qo'shiladigan keyingi bo'limlar:

* batafsil ma'lumotlar bazasi jadvallari
* django model maydonlari
* url arxitekturasi
* shablon sahifalari registri
* ish jarayoni diagrammalari
* bildirishnoma stsenariylari
* rivojlanish bosqichining yo'l xaritasi
* xarajatlarni baholash sxemasi
