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
 
 
