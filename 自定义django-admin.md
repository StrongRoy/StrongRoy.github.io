本地化djangoadmin    'django.middleware.locale.LocaleMiddleware',
定制UserAdmin  
	`from django.contrib.auth.admin import UserAdmin
	from django.contrib.auth.models import User

	class MyUserAdmin(UserAdmin):
	    list_display = ('email','first_name','last_name','is_staff')
	    list_filter = ('is_staff',)
	    search_fields = ('last_name',)
	admin.site.unregister(User)
	admin.site.register(User,MyUserAdmin)`
#定制ModeAdmin
	    `class PoemModelAdmin(admin.ModelAdmin):
	    list_display = ('title','timestamp','author')
	    list_display_links = ('author',)
	    search_fields = ('title',)
	    list_editable = ['title']
	    list_filter = ['title']
	    change_form_template ='change_form.html'
	    class Meta:
	        model = Poem
	
	admin.site.register(Poem,PoemModelAdmin)`
# 自定义admin widget

##修改字段默认widget
 widgets = {
            'author':forms.Textarea，
            'type':forms.RadioSelect,
        }
##设置widget属性
 widgets = {
            'author':forms.Textarea(attrs={'cols':20,'rows':1}),
            'type':forms.RadioSelect,
        }
##自定义widget
class SubInput(forms.TextInput):
    class Media:
        css={
            'all':('input.css',)
        }
 widgets = {
            'author':forms.Textarea(attrs={'cols':20,'rows':1}),
            'title':SubInput(),
            'type':forms.RadioSelect,
        }
#自定义admin操作
##如何定义普通操作
##如何定义中间页面
##整个站点应用操作
##不同ModeAdmin应用操作



 #国际化之时区支持
django如何设置时区
Form和Model里时区问题

时区敏感

python的datetime.datetime对象会有tzinfo属性来存储时区信息。
当这个属性被设置了，他就是时区敏感，否则就是原生的。

可以用django.utils.timezone 
is _aware  is_naive 来判断



