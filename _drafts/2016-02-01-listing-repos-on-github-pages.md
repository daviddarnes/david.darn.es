---
title: Listing GitHub Repos on GitHub Pages
---

{% highlight liquid %}
{% raw %}

{% if site.github.public_repositories %}
  <ul class="list  list--repos">
    {% for repo in site.github.public_repositories %}
      <li class="item  item--repo">
        <a href="{{ repo.homepage }}">{{ repo.name }}</a>
      </li>
    {% endfor %}
  </ul>
{% endif %}

{% endraw %}
{% endhighlight %}
