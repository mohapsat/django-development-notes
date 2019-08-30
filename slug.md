### How to us a combination of PK and slugs in place of PK for URL
--------

1. in urls.py define path as combination of pk and slug
```path('bot/<int:pk>-<slug:slug>/', views.pri_bot_interaction, name='pri_bot_interaction'),```

2. in views, use both pk and slug to check for objects
```bot = get_object_or_404(Bot, pk=pk, slug=slug)```

3. in models
    - Import slugify > `from django.utils.text import slugify`
    - create a slug field
    
    `slug = models.SlugField(null=True, unique=True)`
    - add a method to class to save slug and assign to col, name in this case
    
    #### method to assign col to slug
    def save(self, *args, **kwargs):
        self.slug = slugify(self.name)
        super(Bot, self).save(*args, **kwargs)
      
    - Makemigrations and migrate
    
4. In template <html>
  refer as 
  
  ```<td><a href="{% url 'pri_bot_interaction' bot.pk bot.slug %}">{{ bot.name }}</a></td>```

-----------
