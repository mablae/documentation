# Hierarchical PSR-6 cache pool 

This is a PSR-6 implementation of a hierarchical cache architecture.  

If you have a cache key like `|users|:uid|followers|:fid|likes` where `:uid` and `:fid` are arbitrary integers, you
 may flush all followers by flushing `|users|:uid|followers`.
 
```php
$user = 4711;
for ($i = 0; $i < 100; $i++) {
  $item = $pool->getItem(sprintf('|users|%d|followers|%d|likes', $user, $i));
  $item->set('Justin Bieber');
  $pool->save($item);
}

$pool->hasItem('|users|4711|followers|12|likes'); // True

$pool->deleteItem('|users|4711|followers');

$pool->hasItem('|users|4711|followers|12|likes'); // False
```
