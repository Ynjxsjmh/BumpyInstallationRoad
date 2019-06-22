<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-generate-toc again -->
**Table of Contents**

- [精简参数](#精简参数)

<!-- markdown-toc end -->


# 精简参数
搜索的时候，我们可能会在地址栏发现 Google 的搜索格式是：

```
https://www.google.com/search?q=Define+Word&oq=Define+Word&aqs=chrome..69i57j69i60l3j69i61l2.617j0j7&sourceid=chrome&ie=UTF-8
```

前面的 q 我们比较好理解，就是指我们的搜索词。但是后面的那一大串是什么呢？我们可以在`设置->搜索引擎->管理搜索引擎`的 Google 中找到：

```
{google:baseURL}search?q=%s&client=ubuntu&channel=cs&{google:RLZ}{google:originalQueryForSuggestion}{google:assistedQueryStats}{google:searchFieldtrialParameter}{google:searchClient}{google:sourceId}{google:instantExtendedEnabledParameter}{google:omniboxStartMarginParameter}ie={inputEncoding}
```

所以，我们只需要将 q 后面的参数全部去掉就可以了。但是遗憾的是，我们不能直接修改原来的`网址格式`。

想要做到精简的目的，我们要做四步：
1. 首先需要先添加一个新的搜索引擎，这里我就叫做 `SimpleGoogle`
2. 然后在`网址格式`中添加 `{google:baseURL}search?q=%s`
3. 接下来我们在`关键字`中填上 `google.com` 就可以了
4. 最后我们还需要将新添加的 SimpleGoogle 设置为默认搜索引擎

需要注意的是，添加`关键字`的时候可能会提醒 invalid，我是把 m 去掉，然后保存就可以了。再查看的时候就会发现它自己变成了 google.com

参考：
- [How to remove Google Chrome's Google search engine parameters?](https://superuser.com/questions/1408742/how-to-remove-google-chromes-google-search-engine-parameters)
- [What is the AQS parameter in Google search query?](https://superuser.com/questions/653295/what-is-the-aqs-parameter-in-google-search-query)