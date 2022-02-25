---
layout: page
permalink: /tags
---

<div id="archives">

  <div class="tag-list">
    <ul class="tags">
      {% assign tag_sorted = site.tags | sort %}
      {% for tag in tag_sorted %}

      {% capture tag_name %}{{tag|first|slugize}}{% endcapture %}
      {% capture tag_size %}{{tag|last|size}}{% endcapture %}

      <li>
        <a href="#{{tag_name}}" onclick="showTag('#{{tag_name}}')">
          {{tag_name}} ({{tag_size}})
        </a>
      </li>
      {% endfor %}
    </ul>
  </div>

  <div class="archive-tag">
    {% for tag in site.tags %}

    {% capture tag_name %}{{tag|first|slugize}}{% endcapture %}

    <div class="archive-group" style="display:none" id="{{tag_name}}" >

      {% for post in site.tags[tag_name] %}
      <article class="archive-item">
        <ul>
          <li><h6><a href="{{ site.baseurl }}{{ post.url }}">{{post.title}}</a></h6></li>
        </ul>
      </article>
      {% endfor %}

    </div>
    {% endfor %}
  </div>

</div>


<script src="//ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
<script>
  $(document).ready(function init(){
    var url = window.location.href;
    var req = /#([^\s]+)$/.exec(url);

    if(!Array.isArray(req)) {
      return false;
    }
    var selector = '#' + req.pop();
    showTag(selector);
  });

  function showTag(selector) {
    $('.archive-group').hide();
    $(selector).show();
  }
</script>