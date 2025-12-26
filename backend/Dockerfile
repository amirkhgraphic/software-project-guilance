# مرحله 1: استفاده از ایمیج پایه رسمی Python
FROM python:3.11-slim

# مرحله 2: تنظیم پوشه کاری داخل کانتینر
WORKDIR /app

# مرحله 3: کپی فایل نیازمندی‌ها و نصب کتابخانه‌های پایتون
# از pip install --no-cache-dir استفاده می‌کنیم تا فایل‌های موقت را ذخیره نکند.
COPY requirements.txt /app/
RUN pip install --no-cache-dir -r requirements.txt

# مرحله 4: کپی کردن سورس‌کد پروژه
COPY . /app/

# مرحله 5: اجرای دستورات اولیه جنگو (makemigrations و migrate)
# ما این دستورات را در یک اسکریپت شل جداگانه (یا مستقیماً در CMD) می‌گذاریم.
# نکته: ENTRYPOINT یا CMD را فقط یک بار می‌توان استفاده کرد. برای اجرای چند دستور،
# بهترین راهکار این است که دستورات آماده‌سازی را در قالب یک شل اسکریپت کوچک
# یا در همان آرگومان CMD قبل از دستور اصلی اجرای سرور قرار دهیم.
# اما برای سادگی برای مبتدیان، ما از یک خط شل استفاده می‌کنیم:

# اجرای makemigrations، سپس migrate، و در نهایت اجرای سرور
CMD python manage.py makemigrations \
    && python manage.py migrate \
    && python manage.py runserver 0.0.0.0:8000