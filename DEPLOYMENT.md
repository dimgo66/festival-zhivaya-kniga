# 🚀 Руководство по развёртыванию

Это руководство поможет вам развернуть сайт фестиваля «Живая книга» на различных платформах.

## 📋 Предварительные требования

- Все файлы проекта скачаны
- Доступ к хостингу или платформе развёртывания
- (Опционально) Git установлен для работы с репозиторием

## 🌐 Методы развёртывания

### 1. GitHub Pages (Бесплатно)

Идеально для статических сайтов:

```bash
# 1. Создайте репозиторий на GitHub
# 2. Инициализируйте Git в папке проекта
git init
git add .
git commit -m "Initial commit: Festival Zhivaya Kniga website"

# 3. Добавьте remote репозиторий
git remote add origin https://github.com/ваш-username/festival-zhivaya-kniga.git

# 4. Отправьте код
git push -u origin main

# 5. В настройках репозитория GitHub:
# Settings → Pages → Source: main branch → Save
```

Ваш сайт будет доступен по адресу: `https://ваш-username.github.io/festival-zhivaya-kniga/`

### 2. Netlify (Бесплатно, рекомендуется)

Простое развёртывание с автоматическими обновлениями:

#### Способ A: Через веб-интерфейс (Drag & Drop)
1. Зайдите на [netlify.com](https://www.netlify.com/)
2. Создайте аккаунт (можно через GitHub)
3. Перетащите папку проекта в область "Sites"
4. Сайт автоматически опубликуется

#### Способ B: Через Git
```bash
# 1. Свяжите проект с GitHub (см. выше)
# 2. На Netlify: New site from Git
# 3. Выберите ваш репозиторий
# 4. Build settings оставьте пустыми (статический сайт)
# 5. Deploy site
```

**Преимущества Netlify:**
- Автоматическое HTTPS
- Собственный домен (бесплатно)
- Автоматические обновления при push в Git
- CDN по всему миру
- Форм-обработчики

### 3. Vercel (Бесплатно)

Похож на Netlify:

```bash
# 1. Установите Vercel CLI
npm i -g vercel

# 2. В папке проекта запустите
vercel

# 3. Следуйте инструкциям в терминале
```

Или через веб-интерфейс:
1. [vercel.com](https://vercel.com/) → Import Project
2. Подключите Git репозиторий
3. Deploy

### 4. Обычный хостинг (Shared Hosting)

Для провайдеров типа Beget, TimeWeb, reg.ru:

1. Подключитесь к хостингу через FTP/SFTP:
   - Хост: ftp.ваш-домен.ru
   - Порт: 21 (FTP) или 22 (SFTP)
   - Логин и пароль от хостинга

2. Загрузите все файлы в корневую папку сайта (обычно `/public_html/` или `/www/`)

3. Структура должна быть такой:
```
/public_html/
  ├── index.html
  ├── README.md
  ├── css/
  ├── js/
  └── images/
```

4. Откройте браузер и перейдите на ваш домен

### 5. Firebase Hosting (Google)

```bash
# 1. Установите Firebase CLI
npm install -g firebase-tools

# 2. Авторизуйтесь
firebase login

# 3. Инициализируйте проект
firebase init hosting

# Выберите:
# - Use an existing project или Create new project
# - Public directory: . (текущая папка)
# - Single-page app: No
# - Automatic builds: No

# 4. Разверните
firebase deploy
```

### 6. Cloudflare Pages

1. Зайдите на [pages.cloudflare.com](https://pages.cloudflare.com/)
2. Connect to Git → выберите репозиторий
3. Build settings:
   - Build command: (оставьте пустым)
   - Build output directory: /
4. Save and Deploy

## 🔧 Настройка после развёртывания

### Собственный домен

#### На Netlify:
1. Domain settings → Add custom domain
2. Добавьте ваш домен
3. Настройте DNS записи у регистратора:
```
Type: CNAME
Name: www
Value: ваш-сайт.netlify.app
```

#### На обычном хостинге:
- Домен обычно настраивается автоматически через панель управления

### SSL сертификат (HTTPS)

- **Netlify/Vercel/GitHub Pages:** автоматически
- **Обычный хостинг:** через панель управления (cPanel, ISPmanager)
  - Let's Encrypt - бесплатный SSL
- **Cloudflare:** автоматически + дополнительная защита

### Google Analytics (опционально)

Добавьте перед закрывающим `</head>`:

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_MEASUREMENT_ID');
</script>
```

### Яндекс.Метрика (опционально)

Добавьте перед закрывающим `</body>`:

```html
<!-- Yandex.Metrika counter -->
<script type="text/javascript" >
   (function(m,e,t,r,i,k,a){m[i]=m[i]||function(){(m[i].a=m[i].a||[]).push(arguments)};
   m[i].l=1*new Date();
   for (var j = 0; j < document.scripts.length; j++) {if (document.scripts[j].src === r) { return; }}
   k=e.createElement(t),a=e.getElementsByTagName(t)[0],k.async=1,k.src=r,a.parentNode.insertBefore(k,a)})
   (window, document, "script", "https://mc.yandex.ru/metrika/tag.js", "ym");

   ym(XXXXXXXX, "init", {
        clickmap:true,
        trackLinks:true,
        accurateTrackBounce:true,
        webvisor:true
   });
</script>
```

## 🔍 SEO настройки

### Создайте robots.txt в корне:

```
User-agent: *
Allow: /

Sitemap: https://ваш-домен.ru/sitemap.xml
```

### Создайте sitemap.xml:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://ваш-домен.ru/</loc>
    <lastmod>2024-12-02</lastmod>
    <changefreq>monthly</changefreq>
    <priority>1.0</priority>
  </url>
</urlset>
```

### Зарегистрируйте сайт в поисковиках:

1. **Google Search Console:** [search.google.com/search-console](https://search.google.com/search-console)
2. **Яндекс.Вебмастер:** [webmaster.yandex.ru](https://webmaster.yandex.ru)

## ⚡ Оптимизация производительности

### 1. Минификация CSS и JS (опционально)

Используйте онлайн-инструменты:
- CSS: [cssminifier.com](https://cssminifier.com/)
- JS: [javascript-minifier.com](https://javascript-minifier.com/)

### 2. Оптимизация изображений

- Используйте [tinypng.com](https://tinypng.com/) или [squoosh.app](https://squoosh.app/)
- Конвертируйте в WebP формат для лучшего сжатия

### 3. Кэширование (для обычного хостинга)

Создайте `.htaccess` в корне:

```apache
# Enable GZIP compression
<IfModule mod_deflate.c>
  AddOutputFilterByType DEFLATE text/html text/plain text/xml text/css text/javascript application/javascript
</IfModule>

# Browser caching
<IfModule mod_expires.c>
  ExpiresActive On
  ExpiresByType image/jpg "access plus 1 year"
  ExpiresByType image/jpeg "access plus 1 year"
  ExpiresByType image/gif "access plus 1 year"
  ExpiresByType image/png "access plus 1 year"
  ExpiresByType text/css "access plus 1 month"
  ExpiresByType application/javascript "access plus 1 month"
  ExpiresByType text/html "access plus 1 hour"
</IfModule>
```

## 🔐 Безопасность

### Security Headers (для обычного хостинга)

Добавьте в `.htaccess`:

```apache
# Security Headers
<IfModule mod_headers.c>
  Header set X-Content-Type-Options "nosniff"
  Header set X-Frame-Options "SAMEORIGIN"
  Header set X-XSS-Protection "1; mode=block"
  Header set Referrer-Policy "no-referrer-when-downgrade"
</IfModule>
```

## 📊 Мониторинг

После развёртывания проверьте:

1. **PageSpeed Insights:** [pagespeed.web.dev](https://pagespeed.web.dev/)
2. **GTmetrix:** [gtmetrix.com](https://gtmetrix.com/)
3. **Mobile-Friendly Test:** [search.google.com/test/mobile-friendly](https://search.google.com/test/mobile-friendly)

## 🆘 Решение проблем

### Сайт не открывается
- Проверьте, что `index.html` находится в корневой папке
- Убедитесь, что файл называется именно `index.html` (не `Index.html`)
- Проверьте права доступа к файлам (должны быть 644)

### CSS/JS не загружаются
- Проверьте пути в HTML (должны быть относительные: `css/style.css`)
- Убедитесь, что файлы загружены в правильные папки
- Проверьте консоль браузера (F12) на ошибки

### Изображения не отображаются
- Проверьте пути к изображениям
- Убедитесь, что файлы загружены в папку `images/`
- Проверьте расширения файлов (.png, .jpg, не .PNG, .JPG)

### Ошибка 404
- Проверьте настройки хостинга
- Убедитесь, что файлы в правильной директории
- Для SPA настройте перенаправления (не нужно для этого проекта)

## 📱 Тестирование

Протестируйте на разных устройствах:
- [ ] Desktop (Chrome, Firefox, Safari, Edge)
- [ ] Tablet (iPad, Android tablets)
- [ ] Mobile (iPhone, Android phones)

Проверьте функциональность:
- [ ] Навигация работает
- [ ] Все ссылки открываются
- [ ] Видео загружаются
- [ ] Мобильное меню работает
- [ ] Формы отправляются (если есть)
- [ ] Анимации работают плавно

## 🎉 Поздравляем!

Ваш сайт фестиваля «Живая книга» успешно развёрнут! 

Не забудьте сообщить URL Софии Агачер и добавить ссылку на официальных страницах фестиваля.

---

**Нужна помощь?** Напишите на info@agacher.com