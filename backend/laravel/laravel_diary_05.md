# 削除機能の作成
## 学ぶこと
このカリキュラムでは、削除機能の作成を通して以下のことを学びます。  
1. ブラウザからURLを入力して、画面が表示されるまでの流れ(復習)
2. データを削除する方法


## ルートの設定
今まで同様ルートの設定を行います。  

```php
// routes/web.php

Route::delete('diary/{id}/delete', 'DiaryController@destroy')->name('diary.destroy'); // 削除処理
```

1箇所今までと異なる部分があります。  
`diary/{id}/delete` の`{id}`には任意の値が入ります。  
今回削除機能で想定しているのは、diariesテーブルのidです。  
削除する場合は、削除するレコードを特定する必要があるため、  
各レコードのidをURLに組み込みます。  

## 一覧画面に削除ボタンを追加
削除ボタンの作成方法は投稿ボタンとほとんど同じです。

2点異なる箇所があります。  
1. フォームのメソッドの指定方法
2. routeに第2引数がある

### フォームのメソッドの指定方法
HTMLの仕様上GETとPOST以外のメソッドを使用できないため、  
フォームのmethodはPOSTにして、実際使用したいメソッドは、  
`@method('delete')`といった形でフォームの中に書きます。  

```php
// resources/views/diaries/index.blade.php

<p>{{ $diary->created_at }}</p>
<form action="{{ route('diary.destroy', ['id' => $diary->id]) }}" method="POST" class="d-inline">
    @csrf
    @method('delete')
    <button class="btn btn-danger">削除</button>
</form>
```

### routeに第2引数がある
ルートで{$id}といった形で、  
任意の値を受け取る場合、画面でURLを作成する時は、  
`{{ route('diary.destroy', ['id' => $diary->id]) }}`のように、  
第2引数を連想配列で記述します。  


## コントローラーの編集(削除処理)
最後に削除ボタンが押された後の処理です。  

```php
// app/Http/Controllers/DiaryController

public function destroy(int $id)
{
    //Diaryモデルを使用して、diariesテーブルから$idと一致するidをもつデータを取得
    $diary = Diary::find($id); 

    //取得したデータを削除
    $diary->delete();

    return redirect()->route('diary.index');
}
```

`destroy(int $id)`の`$id`には、  
画面のURLで指定したid、 つまり選択されたデータのidが入ります。  

そのidを元にDBからデータを取得して削除します。  


## まとめ
これで削除機能の作成は完了です。  

このカリキュラムでは、以下のことを学びました。  
1. ブラウザからURLを入力して、画面が表示されるまでの流れ(復習)
2. データを削除する方法