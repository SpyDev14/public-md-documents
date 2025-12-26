> Составлено @Prisma4
# Сигнал

```python
from django.db.models.signals import post_save  
from django.dispatch import receiver  
from django.core.mail import send_mail  
from django.conf import settings

@receiver(post_save, sender=Моделька)  
def send_email_on_creation(sender, instance, created, **kwargs):  
    if created:  
        subject = f"Новый объект {instance.__class__.__name__} создан"        message = f"Был создан новый объект {instance.__class__.__name__} с ID: {instance.pk}."  
        from_email = settings.DEFAULT_FROM_EMAIL  
        recipient_list = settings.EMAIL_RECIPIENTS  
        send_mail(subject, message, from_email, recipient_list)
```

# Settings.py

```python
...

# EMAIL

EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend'  
EMAIL_RECIPIENTS = os.environ.get('email_recipients').split(',')  
EMAIL_HOST = os.environ.get('email_host')  
EMAIL_PORT = os.environ.get('email_port')  
EMAIL_USE_TLS = os.environ.get('email_use_tls')  
EMAIL_HOST_USER = os.environ.get('email_user')  
EMAIL_HOST_PASSWORD = os.environ.get('email_password')  
DEFAULT_FROM_EMAIL = os.environ.get('email_from')

...
```

# ./Apps.py

```python
class ...Config(AppConfig):  
    default_auto_field = 'django.db.models.BigAutoField'  
    name = '...'  
  
    def ready(self):  
        import .signals
```