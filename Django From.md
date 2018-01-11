#Form
##什么是From?什么是Django From?
django表单系统中，所有的表单类都有作为 django.froms.From 的子类创建，包括ModelFrom

###关于django的表单系统，主要有两种
1. 基于django.froms.From:所有表单类的父类
2. 基于django.froms.modelForm 可以和模型类绑定的Form

##案例：
实现添加出版社信息的功能。


##不使用Django From的情况
	def add_publisher(request):
		if(request.method == "POST"):
			# 如果为psot提交，介绍首用户提交过了的数据
			name = request.POST.get('name')
			address = request.POST.get('address')
			city = request.POST.get('city')
			state_province = request.POST.get('state_province')
			country = request.POST.get('country')
			website = request.POST.get('website')
			Publisher.objects.create(
				name = name,
				address = address,
				city = city,
				state_province = state_province,
				country = country,
				website = website,
			)
			return HttpResponse('添加出版社信息成功！')
		else:
			return render(request,'add_publisher.html',locals())
##使用From的情况
	 {{ publisher_form.as_p }}


	from django import forms
	
	class  PublisherForm(forms.Form):
	    name = forms.CharField()
	    address = forms.CharField()
	    city = forms.CharField()
	    state_province = forms.CharField()
	    country = forms.CharField()
	    website = forms.URLField()

	publisher_form = PublisherForm(request.POST)
			if publisher_form.is_valid(): #验证表单填写的内容是否合法
				Publisher.objects.create(
					name = publisher_form.cleaned_data['name'],
					address = publisher_form.cleaned_data['address'],
					city = publisher_form.cleaned_data['city'],
					state_province = publisher_form.cleaned_data['state_province'],
					country = publisher_form.cleaned_data['country'],
					website = publisher_form.cleaned_data['website'],
				)
			return HttpResponse('添加出版社信息成功！')
##使用ModelFrom的情况
	class  PublisherForm(forms.ModelForm):
		    class Meta:
		        model = Publisher
		        exclude=('id',)
	# 使用Django ModelForm的情况
		publisher_form = PublisherForm(request.POST)
		if publisher_form.is_valid():  # 验证表单填写的内容是否合法
			publisher_form.save()
			return HttpResponse('添加出版社信息成功！')

##总结
使用Django中的From可以大大简化代码，常用的表单功能特性都整合到了Form中，而ModelForm可以和Model进行绑定，进一步简化操作

##资料
[https://docs.djangoproject.com/en/1.11/ref/forms/api/](https://docs.djangoproject.com/en/1.11/ref/forms/api/)

[https://docs.djangoproject.com/en/1.11/ref/forms/fields/](https://docs.djangoproject.com/en/1.11/ref/forms/fields/)

##From的验证
Django提供了3中方式来验证

1.  表单字段验证器
[https://docs.djangoproject.com/en/1.11/ref/validators/](https://docs.djangoproject.com/en/1.11/ref/validators/)

     表单字段的验证器

		def validate_even(value):
		    try:
		        Publisher.objects.get(name=value)
		        raise ValidationError("%s的信息已经存在" % value)
		    except Publisher.DoesNotExist:
		        pass

	>PublisherForm

		name = forms.CharField(label='名称' ,validators = [validate_even])
2.  clean_filedname,验证字段 针对某个字段进行验证

	    def clean_name(self):
	        value = self.cleaned_data.get('name')
	        try:
	            Publisher.objects.get(name=value)
	            raise ValidationError("%s的信息已经存在" % value)
	        except Publisher.DoesNotExist:
	            pass
	
	        return value

3. 表单clean方法，可针对整个表单进行验证

案例：
自定义验证，不能插入重名的出版社名称