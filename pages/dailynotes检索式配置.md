---
title: DailyNotes检索式配置
---

## 最终效果
:PROPERTIES:
:heading: true
:END:
### ![2021_01_15_image.png](https://cdn.logseq.com/%2F746ad3ba-7f05-4be2-85b1-b28c6223ef440d55ba28-c0a5-450f-bb08-8e4d9b94b0462021_01_15_image.png?Expires=4764318057&Signature=AU2Pud9u~SJ9gaVE64gtFGvUdjT60B~TpWHAKU9ea03SjagBuPhS-mS6lqTu~Xh2Necdu7BWprP7-btYPvNmIk8zN~sbbaqYzvy35Xd0G2HcbUBvP5NRsxEyshcpHujERZHz9IsESoNvDtm6upavC~VRFZV-Eh8JHMN3VnYhV5iEhs1kxc7R0VdwV5k8NujtUhpw7PvDu9RIvICFKdUD-cHD9ohzVAd6tWjwsfdqUDLPmDzLYioQ8FLOYMXb87wIV0f91BSYXtKRsablwGwuhBW2gUYBlElPIqVBSLoeA5Fmdql13h0Ar~OOZbS6eGgJ7IDnSYI8dw80k71vFfchEA__&Key-Pair-Id=APKAJE5CCD6X7MP6PTEA)
##

## 修改config.edn

:PROPERTIES:
:heading: true
:END:

### 头像 > 设置

#### 或者，所有文件中查找；或者，直接检索
![](https://raw.githubusercontent.com/xulei-shl/picgo/main/img/20210116215023.png)
### 将检索式新增在： `:default-queries {:journals[   ]}` 即可
![](https://raw.githubusercontent.com/xulei-shl/picgo/main/img/20210116215157.png)
## 笔记漫游

:PROPERTIES:
:heading: true
:END:

- 随机回顾有特定tag的block

### 个人使用场景

#### 文献阅读后，会给其打1-5💗星级tag。笔记漫游检索式就是检索3.5-5💗的笔记，并随机得到5个结果

### 检索式

```
{:title "🏄 文档漫游"
 :query [:find (pull ?b [*])
         :where
         [?p :page/name ?name]
         [?b :block/ref-pages ?p]
         [(contains? #{"3.5💗️" "4💗️" "4.5💗️" "5💗️"} ?name)]]
:result-transform (fn [blocks]
                     (take 5 (shuffle (take 100 blocks))))}
```

##

## 待读文献
:PROPERTIES:
:heading: true
:END:


- 检索tag为`#待读`的所有block
### 个人使用场景

#### 阅读某篇文献时，施引、被引等相关文献，或其他计划阅读文献，都可以先在logseq中生成笔记block或page，并打上`#待读` 标签。然后利用检索式在Daily Notes中自动检索获取所有待读计划文献

### 具体使用步骤

#### 首先，利用Zotero收集这些文献

#### 然后，利用[[Mdnotes插件]]导出文献的Markdown格式笔记，默认已经加上了`#待读`标签

#### 每日Daily Notes生成时，就会自动将此类文献笔记检索聚集起来

### 检索式

```
{:title "📚 待读文献"
 :query [:find (pull ?b [*])
         :where
         [?p :page/name "待读"]
         [?b :block/ref-pages ?p]]
  :collapsed? true}
```

##
:PROPERTIES:
:heading: true
:END:

## DeadLine

:PROPERTIES:
:heading: true
:END:

- 7天内的待办事项

### 检索式

```
{:title "📅 临近DeadLine"
:query [:find (pull ?b [*])
:in $ ?start ?next
:where
[?b :block/deadline ?d]
[?b :block/marker ?marker]
[(> ?d ?start)]
[(< ?d ?next)]
[(contains? #{"NOW" "LATER" "DOING" "TODO"} ?marker)]]
:inputs [:today :7d-after]
:collapsed? false}
```

## 最近更新

:PROPERTIES:
:heading: true
:END:

- 检索最近更新的4个页面
- 非原创，直接复用了Github网友的分享，https://github.com/71/logseq-snippets

### 检索式

```
{:title "🖋 最近更新"
 :query [:find (pull ?p [*])
         :in $ ?start
         :where
         [?p :page/last-modified-at ?d]
         [?p :page/name ?n]
         [(>= ?d ?start)]
         [(not= ?n "contents")]]
 :inputs [:4d-before]
 :view (fn [result]
  (for [p (take 4 (sort-by :page/last-modified-at > result))]
    [:div.ls-block.flex.flex-col.pt-1
      [:div.flex-1.flex-row
        [:div.mr-2.flex.flex-row.items-center
          {:style {:height "24px" :margin-top "0" :float "left"}}
          [:a.block-control.opacity-50.hover:opacity-100
            {:style {:min-width "0" :height "16px" :margin-right "2px"}}
            [:span]]
          [:a
            {:href (str "/page/" (:page/name p))}
            [:span.bullet-container.cursor
              [:span.bullet]]]]
        [:div.flex.relative
          [:div.flex-1.flex-col.relative.block-content
            [:div
              [:span.page-reference
                [:a.page-ref
                  {:href (str "/page/" (:page/name p))}
                  (-> p :page/properties :title)]]]]]]]))}
```



## 其他注意事项

:PROPERTIES:
:heading: true
:END:

### 检索式在 :default-queries {:journals[ ]}中的排列顺序就是页面中的顺序

### 检索式里的 `:collapsed?`表示结果是否折叠，缺省表示展开

## 致谢

:PROPERTIES:
:heading: true
:END:

### 天生在微信群对随机结果检索式的回答

### discord上网友的讨论

### github上网友的分享
