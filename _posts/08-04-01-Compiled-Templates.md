---
isChild: true
title: Kompajlirani templejti
anchor: compiled_templates
---

## Kompajlirani templejti {#compiled_templates_title}

PHP jeste evoluirao u zreo, objektno-orijenisan jezik, ali [nije mnogo napredovao][article_templating_engines]
kao templejt jezik. Kompajlirani templejt sistemi (template engines), kao što su [Twig], [Brainy], ili [Smarty]*, upotpunjuju ovaj
aspekt sa novom sintaksom osmišljenom upravo za potrebe templejta. Od automatskog escape-ovanja,
preko nasleđivanja i pojednostavljenih kontrolnih struktura, kompajlirani templejti su mnogo
čitljiviji, lakši za pisanje, ali i bezbedniji. Oni takođe mogu biti kompatibilni sa više različitih
programskih jezika, za šta je dobar primer [Mustache]. Pošto se templejti moraju kompajlirati,
neizbežan je određeni negativan uticaj na performanse, koji je ipak zanemarljiv ako se keširanje ispravno koristi.

**Smarty omogućava automatsko _escape-ovanje_, ali ova funkcionalnost NIJE podrazumevano uključena.*

### Jednostavan primer kompajliranog templejta

Primer baziran na [Twig] biblioteci.

{% highlight html+jinja %}
{% raw %}
{% include 'header.html' with {'title': 'User Profile'} %}

<h1>User Profile</h1>
<p>Hello, {{ name }}</p>

{% include 'footer.html' %}
{% endraw %}
{% endhighlight %}

### Primer kompajliranog templejta koji koristi nasleđivanje

Primer baziran na [Twig] biblioteci.

{% highlight html+jinja %}
{% raw %}
// template.html

<html>
<head>
    <title>{% block title %}{% endblock %}</title>
</head>
<body>

<main>
    {% block content %}{% endblock %}
</main>

</body>
</html>
{% endraw %}
{% endhighlight %}

{% highlight html+jinja %}
{% raw %}
// user_profile.html

{% extends "template.html" %}

{% block title %}User Profile{% endblock %}
{% block content %}
    <h1>User Profile</h1>
    <p>Hello, {{ name }}</p>
{% endblock %}
{% endraw %}
{% endhighlight %}


[article_templating_engines]: http://fabien.potencier.org/article/34/templating-engines-in-php
[Twig]: http://twig.sensiolabs.org/
[Brainy]: https://github.com/box/brainy
[Smarty]: http://www.smarty.net/
[Mustache]: http://mustache.github.io/
