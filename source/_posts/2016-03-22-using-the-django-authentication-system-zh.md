---
title: 【译】使用 Django 认证系统
date: 2016-03-22 22:31:20
tags:
- Django
categories:
- Translation
---

> 译自 [Django Documentation](https://docs.djangoproject.com/en/1.9/topics/auth/default/)，版本1.9。没有逐字逐句翻译，啰嗦的内容都省去了。

本文介绍了 Django 认证系统在默认配置下的使用。默认配置已经发展到能够满足大多数项目需求，处理相当数量的任务，而且具备严谨的密码和权限实现。对于有自定义验证需求的项目，Django 支持[扩展验证](https://docs.djangoproject.com/en/1.9/topics/auth/customizing/)。
Django 认证系统提供认证和授权功能，由于两部分功能有耦合，因此通常简称为认证系统。

## User 对象

[User](https://docs.djangoproject.com/en/1.9/ref/contrib/auth/#django.contrib.auth.models.User) 对象是认证系统的核心。该对象一般抽象表示与网站进行交互的用户，被用来进行权限控制，信息注册，关联内容及其创建者。Django 框架中只存在一种 User 类，像`superusers`，`staff`只是具有一些特殊属性的 User 对象，而不是不同类的 User 对象。

默认的 user 有如下主要属性：
- [username](https://docs.djangoproject.com/en/1.9/ref/contrib/auth/#django.contrib.auth.models.User.username)
- [password](https://docs.djangoproject.com/en/1.9/ref/contrib/auth/#django.contrib.auth.models.User.password)
- [email](https://docs.djangoproject.com/en/1.9/ref/contrib/auth/#django.contrib.auth.models.User.email)
- [first_name](https://docs.djangoproject.com/en/1.9/ref/contrib/auth/#django.contrib.auth.models.User.first_name)
- [last_name](https://docs.djangoproject.com/en/1.9/ref/contrib/auth/#django.contrib.auth.models.User.last_name)

全面的参考请阅读[完整 API 文档](https://docs.djangoproject.com/en/1.9/ref/contrib/auth/#django.contrib.auth.models.User)，下文更偏向业务导向。

### 创建 users

创建 user 最直接的方式是调用内置的 `create_user()` 辅助方法：
``` bash
>>> from django.contrib.auth.models import User
>>> user = User.objects.create_user('john', 'lennon@thebeatles.com', 'johnpassword')

# At this point, user is a User object that has already been saved
# to the database. You can continue to change its attributes
# if you want to change other fields.
>>> user.last_name = 'Lennon'
>>> user.save()
```
如果已经安装了 `Django admin` ，也可以[交互式创建 users](https://docs.djangoproject.com/en/1.9/topics/auth/default/#auth-admin)。
**************************************
### 创建 superusers

使用 `createsuperuser` 命令创建 superusers：
```bash
$ python manage.py createsuperuser --username=joe --email=joe@example.com
```
控制台会提示输入密码，输入密码后，superuser 就创建完成了。如果没有加上 [--username](https://docs.djangoproject.com/en/1.9/ref/django-admin/#cmdoption-createsuperuser--username) 或 [--email](https://docs.djangoproject.com/en/1.9/ref/django-admin/#cmdoption-createsuperuser--email) 选项，控制台会提示输入对应值。
**************************************
### 修改密码

Django 不会在 user 模型里存储原密码（明文），而是哈希值（详情参阅[密码是如何管理的](https://docs.djangoproject.com/en/1.9/topics/auth/passwords/)）。因此，不要试图直接操作 user 密码。这就是为什么要使用辅助函数创建 user 。

要修改用户密码，有如下几种选择：
[manage.py changepassword *username*](https://docs.djangoproject.com/en/1.9/ref/django-admin/#django-admin-changepassword) 提供了由命令行修改用户密码的方法。它会提示你必须输入两次密码以对原密码进行修改，如果两次输入一致，新密码生效。如果没有指定 user ，则控制台会尝试修改与当前系统用户名相匹配的 user 密码。

也可以通过程序代码修改密码，使用函数 [set_password()](https://docs.djangoproject.com/en/1.9/ref/contrib/auth/#django.contrib.auth.models.User.set_password):
``` python
from django.contrib.auth.models import User
u = User.objects.get(username='john')
u.set_password('new password')
u.save()
```
如果已经安装了 Django admin，也可以在[认证系统管理员页](https://docs.djangoproject.com/en/1.9/topics/auth/default/#auth-admin)修改密码。
Django 同时提供可能会用于用户修改自己密码的 [views](https://docs.djangoproject.com/en/1.9/topics/auth/default/#built-in-auth-views) 和 [forms](https://docs.djangoproject.com/en/1.9/topics/auth/default/#built-in-auth-forms)。
如果 Django 的 [SessionAuthenticationMiddleware](https://docs.djangoproject.com/en/1.9/ref/middleware/#django.contrib.auth.middleware.SessionAuthenticationMiddleware) 已开启，则修改用户密码会登出改用户的所有 session。具体细节查阅[修改密码导致 session 失效](https://docs.djangoproject.com/en/1.9/topics/auth/default/#session-invalidation-on-password-change)。
*************************************
### 验证 users
**<font color="green">authenticate(\*\*credentials)<font>[[source](https://docs.djangoproject.com/en/1.9/_modules/django/contrib/auth/#authenticate)]**
要验证给定的用户名和密码，使用 [authenticate()](https://docs.djangoproject.com/en/1.9/topics/auth/default/#django.contrib.auth.authenticate) 方法。它的入参形式为 keyword ，默认的设置为 `username` 和 `password`，如果验证通过，会返回一个 `User` 对象，如果验证失败，则返回 None 。例子如下：
``` python
from django.contrib.auth import authenticate
user = authenticate(username='john', password='secret')
if user is not None:
    # the password verified for the user
    if user.is_active:
        print("User is valid, active and authenticated")
    else:
        print("The password is valid, but the account has been disabled!")
else:
    # the authentication system was unable to verify the username and password
    print("The username and password were incorrect.")
```
> 注
> 这是一个低层次的验证方法；举例来说，它在 [RemoteUserMiddleware](https://docs.djangoproject.com/en/1.9/ref/middleware/#django.contrib.auth.middleware.RemoteUserMiddleware) 中使用。除非要编写自定义的认证系统，否则可能并不需要使用它。如果需要一个限制登录用户操作的方法，参考 [login_required()](https://docs.djangoproject.com/en/1.9/topics/auth/default/#django.contrib.auth.decorators.login_required)。

## 权限和认证

Django 内置一个简单的权限系统。它提供了分配权限给指定用户和指定分组用户的方法。
Django admin site 使用了权限系统，但也可以在自己的代码里使用它。
Django admin site 使用的权限如下所示：
- 查看 "add" 表单和限制拥有该对象 "add" 资格的用户执行 add 操作的权限
- 查看 "change" 列表、"change" 表单和限制拥有该对象 "change" 资格的用户执行 change 操作的权限
- 限制拥有指定对象 "delete" 资格的用户执行 delete 操作的权限
权限不仅可以针对每个对象类型设置，还可以针对具体的对象实例进行设置。通过调用 [ModelAdmin](https://docs.djangoproject.com/en/1.9/ref/contrib/admin/#django.contrib.admin.ModelAdmin) 类提供的 [has_add_permission()](https://docs.djangoproject.com/en/1.9/ref/contrib/admin/#django.contrib.admin.ModelAdmin.has_add_permission)、[has_change_permission()](https://docs.djangoproject.com/en/1.9/ref/contrib/admin/#django.contrib.admin.ModelAdmin.has_change_permission)和[has_delete_permission()](https://docs.djangoproject.com/en/1.9/ref/contrib/admin/#django.contrib.admin.ModelAdmin.has_delete_permission)方法，可以实现对同一对象的不同实体的自定义权限。
User 对象有两个 many-to-many 字段：**group** 和 **user_permissions**。User 对象可以通过和其他 [Django model](https://docs.djangoproject.com/en/1.9/topics/db/models/) 一样的方式访问和它相关的对象：
``` python
myuser.groups = [group_list]
myuser.groups.add(group, group, ...)
myuser.groups.remove(group, group, ...)
myuser.groups.clear()
myuser.user_permissions = [permission_list]
myuser.user_permissions.add(permission, permission, ...)
myuser.user_permissions.remove(permission, permission, ...)
myuser.user_permissions.clear()
```

### 默认权限

当 setting 配置里 [INSTALLED_APPS](https://docs.djangoproject.com/en/1.9/ref/settings/#std:setting-INSTALLED_APPS) 列表里有 **django.contrib.auth**,它会确保为已安装的 Django 应用下的每个 Django model 创建三个权限——add、change 和 delete。
这些权限会在你执行 **[manage.py migrate](https://docs.djangoproject.com/en/1.9/ref/django-admin/#django-admin-migrate)** 时创建；在 **INSTALLED_APPS** 里添加 **django.contrib.auth** 后第一次运行 **migrate** 时，Django 会给之前安装和正在安装的 model 建立默认权限。此后，当你每次执行 **manage.py migrate** 时，会为新安装的 model 创建默认权限（创建权限的方法被 **[post_migrate()](https://docs.djangoproject.com/en/1.9/ref/signals/#django.db.models.signals.post_migrate)** 信号关联）。
假设你安装了 **[app_label](https://docs.djangoproject.com/en/1.9/ref/models/options/#django.db.models.Options.app_label)** 为 **foo** ，model 名为 **Bar** 的应用，我们可以用如下方式测试其基本权限：
- add: **user.has_perm('foo.add_bar')**
- change: **user.has_perm('foo.change_bar')**
- delete: **user.has_perm('foo.delete_bar')**
很少会直接调用 **[permission](https://docs.djangoproject.com/en/1.9/ref/contrib/auth/#django.contrib.auth.models.Permission)** model。
**********************************************
### 组
**[django.contrib.auth.models.Group](https://docs.djangoproject.com/en/1.9/ref/contrib/auth/#django.contrib.auth.models.Group)** model 是用户分类的通用方式，通过它可以应用权限或其他标签到用户上。一个用户可以归属于任意数量的组。