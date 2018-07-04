# estate
October real estate plugin

## Implementing front-end pages 

The plugin provides several components for building the list page (archive), category page,  content details page and category list for the sidebar.  


## estate.htm
  
Search and categories listing


```
title = "Estate"
url = "/estate/:slug?"
layout = "default"
is_hidden = 0

[search_form]

[realty_list]
pageNumber = "{{ :page }}"
categoryFilter = 0
itemsPerPage = 15
categoryPage = "estate"
detailPage = "estate/detail"
searchPage = "estate"
colLg = 4
colMd = 6
colSm = 6
colXs = 12

[realty_category]
categoryPage = "estate"
countSub = 1
==
{% component 'search_form' %}
<hr />
<div class="row">
    <div class="col-sm-8">
        {% component 'realty_list' %}
    </div>
    <div class="col-sm-4">
        {% component 'realty_category' %}
    </div>
</div>
```

## estate/detail.htm

Content detail page

```
title = "Estate detail"
url = "/estate/detail/:slug"
layout = "default"
is_hidden = 0

[realty_detail]
slug = "{{ :slug }}"
categoryPage = "estate"
==
{% component 'realty_detail' %}
```

## For the default settings

Settings -> Real Estate -> Setting  
Tab general -> money format, show category description, show category count number (for category menu)   
Tab pages -> Optional Detail and list pages,  User definable maximum limit, page item limit   
Tan interface -> Optional include css and javascript   

----

![](http://mavitm.com/proje/october/estate/images/3.png)
![](http://mavitm.com/proje/october/estate/images/4.png)
![](http://mavitm.com/proje/october/estate/images/5.png)
![](http://mavitm.com/proje/october/estate/images/6.png)

----

![](http://mavitm.com/proje/october/estate/images/9.png)
![](http://mavitm.com/proje/october/estate/images/10.png)
