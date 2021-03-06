Pagination
==========

<<<<<<< HEAD
When there's too much data to be displayed on a single page at once it's often divided into
parts each containing some data items and displayed one part at a time. Such parts are called
pages thus the name pagination.
  
If you're using [data provider](output-data-providers.md) with one of the [data widgets](output-data-widgets.md)
pagination is already sorted out for you automatically. If not, you need to create [[\yii\data\Pagination]]
object, fill it with data such as [[\yii\data\Pagination::$totalCount|total item count]],
[[\yii\data\Pagination::$pageSize|page size]] and [[\yii\data\Pagination::$page|current page]], apply
it to the query and then feed it to [[\yii\widgets\LinkPager|link pager]].


First of all in controller action we're creating pagination object and filling it with data:

```php
function actionIndex()
{
    $query = Article::find()->where(['status' => 1]);
    $countQuery = clone $query;
    $pages = new Pagination(['totalCount' => $countQuery->count()]);
    $models = $query->offset($pages->offset)
        ->limit($pages->limit)
        ->all();

    return $this->render('index', [
         'models' => $models,
         'pages' => $pages,
    ]);
}
```

Then in a view we're outputting models for the current page and passing pagination object to the link pager:

```php
foreach ($models as $model) {
    // display $model here
}

// display pagination
echo LinkPager::widget([
    'pagination' => $pages,
]);
```
=======
When there are too much data to be displayed on a single page, a common strategy is to display them in multiple
pages and on each page only display a small portion of the data. This strategy is known as *pagination*.

Yii uses a [[yii\data\Pagination]] object to represent the information about a pagination scheme. In particular,

* [[yii\data\Pagination::$totalCount|total count]] specifies the total number of data items. Note that this
  is usually much more than the number of data items needed to display on a single page.
* [[yii\data\Pagination::$pageSize|page size]] specifies how many data items each page contains. The default
  value is 20.
* [[yii\data\Pagination::$page|current page]] gives the current page number (zero-based). The default value
  value is 0, meaning the first page.

With a fully specified [[yii\data\Pagination]] object, you can retrieve and display data partially. For example,
if you are fetching data from a database, you can specify the `OFFSET` and `LIMIT` clause of the DB query with
the corresponding values provided by the pagination. Below is an example, 

```php
use yii\data\Pagination;

// build a DB query to get all articles with status = 1
$query = Article::find()->where(['status' => 1]);

// get the total number of articles (but do not fetch the article data yet)
$count = $query->count();

// create a pagination object with the total count
$pagination = new Pagination(['totalCount' => $count]);

// limit the query using the pagination and retrieve the articles
$articles = $query->offset($pages->offset)
    ->limit($pages->limit)
    ->all();
```

Which page of articles will be returned in the above example? It depends on whether a query parameter named `page`
is given. By default, the pagination will attempt to set the [[yii\data\Pagination::$page|current page]] to be
the value of the `page` parameter. If the parameter is not provided, then it will default to 0.

To facilitate building the UI element that supports pagination, Yii provides the [[yii\widgets\LinkPager]] widget
that displays a list of page buttons upon which users can click to indicate which page of data should be displayed.
The widget takes a pagination object so that it knows what is the current page and how many page buttons should
be displayed. For example,

```php
use yii\widgets\LinkPager;

echo LinkPager::widget([
    'pagination' => $pagination,
]);
```

If you want to build UI element manually, you may use [[yii\data\Pagination::createUrl()]] to create URLs that
would lead to different pages. The method requires a page parameter and will create a properly formatted URL
containing the page parameter. For example,

```php
// specifies the route that the URL to be created should use
// If you do not specify this, the currently requested route will be used
$pagination->route = 'article/index';

// displays: /index.php?r=article/index&page=100
echo $pagination->createUrl(100);

// displays: /index.php?r=article/index&page=101
echo $pagination->createUrl(101);
```

> Tip: You can customize the name of the `page` query parameter by configuring the
  [[yii\data\Pagination::pageParam|pageParam]] property when creating the pagination object.
>>>>>>> yiichina/master
