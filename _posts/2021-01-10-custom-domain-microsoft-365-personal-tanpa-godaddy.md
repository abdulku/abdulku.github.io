---
layout: post
title: "Custom Email Microsoft 365 Personal Tanpa Domain GoDaddy"
date: 2021-01-10 21:45:36 +0700
categories: Sysadmin
author: Abdul
permalink: :title
---

Setelah beberapa pertimbangan, sekitar akhir tahun kemarin akhirnya saya memutuskan untuk berlangganan Microsoft 365 (sebelumnya Office 365) Personal.

Salah satu fitur Microsoft 365 personal adalah bisa menggunakan custom domain. Contohnya, anda punya alamat email <code>namaanda@hotmail.com</code>. Dengan menggunakan custom domain, bisa diubah menjadi <code>mail@namaanda.com</code>. Pada saat artikel ini ditulis hanya mendukung domain yang terdaftar di GoDaddy :

![Allowed GoDaddy domain only](assets/images/2021-01-10/godaddy-only.png)

Domain saya terdaftar di Namecheap yang menurut keterangan diatas, tidak dapat dipakai. Sempat terpikir untuk transfer domain ke GoDaddy agar bisa dipakai di Microsoft 365, tetapi harga transfernya lebih dari 3x lipat dari harga registrasi, meskipun sudah termasuk 2 tahun berlangganan, itu masih terlalu mahal terlebih domain saya expirenya masih lama.

<h3>Langkah Setup</h3>

Berikut cara menggunakan custom domain Microsoft 365 Personal tanpa harus daftar domain di GoDaddy:


1. Login ke outlook mail web, klik 'Manage Premium' logo berlian di kanan atas.

2. Pada bagian Personalized email address, klik Get started.

3. Akan muncul prompt seperti berikut :

   ![Personalize your email address](assets/images/2021-01-10/personalize-your-email-address.png)

4. Disinilah main objectnya, akan muncul pop-up window ke website GoDaddy.
   Pop-up tersebut akan membuka URL :

   <code>https://domainconnect.godaddy.com/v2/domainTemplates/providers/outlook.com/services/personalizedoutlookemail/apply?mxRecordValue=XXXXXXXXX&state=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX&redirect_url=</code>

5. Login ke DNS management domain yang akan digunakan. Disini menggunakan Cloudflare. Buat record DNS yang dibutuhkan sebagai berikut. Paste Unique ID pada record dibawah :


        TYPE        Name              Content                               TTL
        CNAME      autodiscover     autodiscover.outlook.com                5m
        CNAME      _domainconnect   _domainconnect.gd.domaincontrol.com     5m 
        MX         @                XXXXXXXXX.pamx1.hotmail.com             5m
        TXT        @                v=spf1 include:outlook.com -all         5m
        TXT        outlook          XXXXXXXXX                               5m


6. Close pop-up window yang muncul. Ulangi langkah 1-2.

7. Klik 'I already own a GoDaddy domain'.

8. Isikan domain anda pada kolom yang muncul, klik submit.

9. Isi alamat email yang diinginkan.

10. Reload laman Outlook web, lalu masuk ke Manage Premium.

11. Selamat! Domain anda berhasil ditambahkan ke Microsoft 365 :

    ![Personalized email address](assets/images/2021-01-10/personalized-email-address.png)


Selanjutnya anda bisa login Microsoft 365, termasuk appsnya seperti Office, Skype, dll, kirim dan terima email menggunakan alamat email custom yang sudah dibuat.

Sumber : [https://www.reddit.com/r/Office365/comments/cmk120/use_office365_personal_with_your_own_domain_no/][https://www.reddit.com/r/Office365/comments/cmk120/use_office365_personal_with_your_own_domain_no/]

[https://www.reddit.com/r/Office365/comments/cmk120/use_office365_personal_with_your_own_domain_no/]: https://www.reddit.com/r/Office365/comments/cmk120/use_office365_personal_with_your_own_domain_no/