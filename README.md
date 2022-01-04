## ワードプレス一覧にカスタムフィールドを追加する方法
テーマのfunctions.php に以下のような記述を追加します。

~~~PHP
function manage_posts_columns($columns) {
 $columns['カスタムフィールドのKey'] = "カラム名";
 return $columns;
}
function add_column($column_name, $post_id) {
 if( $column_name == 'カスタムフィールドのKey' ) {
 $stitle = get_post_meta($post_id, 'カスタムフィールドのKey', true);
 }
 if ( isset($stitle) && $stitle ) {
 echo attribute_escape($stitle);
 } else {
 echo __('');
 }
}
add_filter( 'manage_posts_columns', 'manage_posts_columns' );
add_action( 'manage_posts_custom_column', 'add_column', 10, 2 );
~~~
 
*「カスタムフィールドのKey」の部分と「カラム名」の部分は、ブログ記事に合わせて変更してみてください。

## 複数のカスタムフィールドの値のカラムを追加
先の「カスタムフィールドの値のカラムを追加」の記述を少し触って、複数のカラムを出力することも可能です。

~~~PHP
function manage_posts_columns($columns) {
 $columns['カスタムフィールドのKey1'] = "カラム名1";
 $columns['カスタムフィールドのKey2'] = "カラム名2";
 return $columns;
}
function add_column($column_name, $post_id) {
 if( $column_name == 'カスタムフィールドのKey1' ) {
 $stitle = get_post_meta($post_id, 'カラム名1', true);
 }
 if( $column_name == 'カスタムフィールドのKey2' ) {
 $stitle = get_post_meta($post_id, 'カラム名2', true);
 }
 if ( isset($stitle) && $stitle ) {
 echo attribute_escape($stitle);
 } else {
 echo __('');
 }
}
add_filter( 'manage_posts_columns', 'manage_posts_columns' );
add_action( 'manage_posts_custom_column', 'add_column', 10, 2 );
~~~
