---
layout: post
title:  "better-exceptions를 이용한 python 디버깅 아이디어"
---
# better-exceptions를 이용한 python 디버깅 아이디어

[better-exceptions](https://github.com/Qix-/better-exceptions)라는 라이브러리가 있습니다. 예외가 발생했을 때, 아래의 그림처럼 Traceback 내용을 디버깅하기 유용하게 보여주는 라이브러리입니다.

![better-exceptions screenshot]({{ site.url }}/assets/2017-07-12-debugging-with-better-exceptions/better-exceptions-screenshot.png)

기본적으로 stdout으로만 출력을 하기 때문에 서버에서 사용하기에는 적합하지 않아보였는데, 뭔가 방법이 없을까 해서 이런 저런 방법을 시도해보다가 한가지 방법을 찾았습니다.

{% highlight python %}
def raise_exception():
    a = 30
    b = 20
    assert a == b

try:
    raise_exception()
except:
    import sys
    import better_exceptions
    exc_to_str = better_exceptions.format_exception(*sys.exc_info())
    print(exc_to_str)
{% endhighlight %}

그러니까, sys.exc_info를 이용하면 better_exceptions가 출력하는 메시지를 문자열로 전달받을 수 있습니다. 아직 직접 적용을 해본건 아니라서 조금 조심스럽긴 하지만, 이 방법을 이용하면 디버깅이 훨씬 쉬워질 것 같습니다.
