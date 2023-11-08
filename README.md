# Laravel_vue.js_practice
  
######2023/11/08  
コントローラーにどんな配列を渡すか？  
https://itsakura.com/php-json-decode  
json_decodeで配列にできる↓こんな配列でOKだった。  
{"data1":{"menu_id":"1","is_started":"true"},"data2":{"menu_id":"2","is_started":"true"}}  
$params = $request->input('arrays');  
$params = json_decode($params, true);  
  
これでarraysのデータをarrayで取得  
forEachで回す。  
配列だとパラメータの取得の仕方がこう変わった。  
https://www.sejuku.net/blog/22538  
  
if ($request->has('menu_id')) {  
    $post->menu_id = $request->input('menu_id');  
}  
↓  
if(array_key_exists('menu_id',$param)) {  
    $post->menu_id = $param['menu_id'];  
}  
  
forEach分の$postをまとめて最後に出すのは  
forEachの前に  
$res = [];  
追加登録したら、その回の$postを$resに追加  
array_push($res, $post);  
forEachが終わったら  
return response()->json($res);  
これでOK  
  
終わったと思ったら、文字列のtrue/falseがintegerのカラムに入らないエラーに  
少しハマったが、きれいに書けたと思う。  
文字列のtrue/falseをintegerのカラムに渡したらこんな感じのエラーが出た  
https://teratail.com/questions/276456  
  
文字列のtrue/falseはbool型に変えて渡すようにしました。  
if(array_key_exists('is_started',$param)){  
    $post->is_started = ($param['is_started']==="true") ? true : false;  
}  
  
https://qiita.com/B73W56H84/items/d6c0e03a754ad02ac143  
  
https://blog.nocodelab.jp/entry/remotehq  
  
