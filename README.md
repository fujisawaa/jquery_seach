jquery_seach
======================

MTを使ったサイトでjqueryを使って簡単に検索機能を作れないかと思って挑戦  

##用件
#####カテゴリー > サブカテゴリー毎に絞り込み検索
同じカテゴリー内のサブカテゴリーに複数チェック → or検索  
別カテゴリー内のサブカテゴリーに複数チェック → and検索  
カテゴリー・サブカテゴリーはMTのカテゴリーに沿うこと  

#####フリーワード検索
ページ内の単語もヒットさせる  
半角スペース区切り  

#####他
絞り込み検索とフリーワード検索はタブ切り替え  


##MT側
#####絞り込み検索
```html
<section class="contentsSection" id="newTopics">
<h2>新着情報</h2>
<ul class="newsList">
<MTEntries sort_by="authored_on" sort_order="descend" lastn="4">
<li class="<MTEntryCategories glue=" "><$MTCategoryBasename$></MTEntryCategories>">
<div class="thum"><MTEntryDataBlogThumAsset><img src="<$MTAssetURL$>" alt=""></MTEntryDataBlogThumAsset></div>
<div class="text"><span class="date">[<$MTEntryDate format="%Y.%m.%d"$>]</span>
<a href="<$MTEntryPermalink$>" target="_blank"><$MTEntryTitle$></a></div>
</li>
</MTEntries>
</ul>
<p class="alignR"><a class="iconLink inlineB" href="list.html">新着症例一覧</a></p>
</section><!-- /.contentsSection -->

<section class="contentsSection" id="searchResultWrap">
<h2>検索結果</h2>
<ul class="newsList">
<MTEntries sort_by="authored_on" sort_order="descend">
<li class="<MTEntryCategories glue=" "><$MTCategoryBasename$></MTEntryCategories>">
<div class="thum"><MTEntryDataBlogThumAsset><img src="<$MTAssetURL$>" alt=""></MTEntryDataBlogThumAsset></div>
<div class="text"><span class="date">[<$MTEntryDate format="%Y.%m.%d"$>]</span>
<a href="<$MTEntryPermalink$>" target="_blank"><$MTEntryTitle$></a></div>
</li>
</MTEntries>
<li id="searchNoResult">検索結果はありません</li>
</ul>
</section><!-- /.contentsSection -->

```
#####フリーワード検索
アーカイブマッピングでxmlとしてデータを吐き出しておく  
```html
<?xml version="1.0" encoding="UTF-8" ?>
<info>


<MTEntries sort_by="authored_on" sort_order="descend">
<item>
<thum><MTEntryDataBlogThumAsset><$MTAssetURL$></MTEntryDataBlogThumAsset></thum>
<date>[<$MTEntryDate format="%Y.%m.%d"$>]</date>
<url><$MTEntryPermalink$></url>
<title><$MTEntryTitle encode_xml="1"$></title>
<bodytxt><$MTEntryBody encode_xml="1"$></bodytxt>
<drname><$MTEntryExcerpt encode_xml="1"$></drname>
</item>
</MTEntries>

</info>

```
