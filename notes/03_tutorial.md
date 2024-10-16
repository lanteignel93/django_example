# Django Notes

https://docs.djangoproject.com/en/4.1/intro/tutorial03/

## Overview¶

A view is a “type” of web page in your Django application that generally serves a specific function and has a specific template. For example, in a blog application, you might have the following views:

    Blog homepage – displays the latest few entries.
    Entry “detail” page – permalink page for a single entry.
    Year-based archive page – displays all months with entries in the given year.
    Month-based archive page – displays all days with entries in the given month.
    Day-based archive page – displays all entries in the given day.
    Comment action – handles posting comments to a given entry.

In our poll application, we’ll have the following four views:

    Question “index” page – displays the latest few questions.
    Question “detail” page – displays a question text, with no results but with a form to vote.
    Question “results” page – displays results for a particular question.
    Vote action – handles voting for a particular choice in a particular question.

When somebody requests a page from your website – say, “/polls/34/”, Django will load the **mysite.urls** Python module because it’s pointed to by the ROOT_URLCONF setting.
It finds the variable named urlpatterns and traverses the patterns in order.
After finding the match at 'polls/', it strips off the matching text ("polls/") and sends the remaining text – "34/" – to the ‘polls.urls’ URLconf for further processing.
There it matches '<int:question_id>/', resulting in a call to the detail() view like so:

```python
detail(request=<HttpRequest object>, question_id=34)
```
