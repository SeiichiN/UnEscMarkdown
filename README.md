# UnEscMarkdown
unEscape Markdown

## 作った動機

Webの中の一つの文章をMarkdownでMarkdownで記述すると表現力がアップしてわかりやすくなるが、
Javascriptなどのスクリプトが動くのが困る。

Webの中の文章は、htmlspecialchars関数でスクリプトを無効化するが、Markdownで記述した
文章をhtmlspecialchars関数を通すと、コードを表示する部分が無効化される。

たとえば、以下のような記述では、

    ## Sample
    ```
    <?php
      phpinfo();
    ?>
    ```
このようになる。  
![Sample1](sample1.png)

だから、コードの中だけ、htmlspecialchars関数での処理を元に戻せばいい。

ついでに、引用を示す部分も処理を元に戻す。

## 使い方

### MarkdownExtraのインストール

php Markdown のページ -> [ダウンロード](https://michelf.ca/projects/php-markdown/)

この中のMichelfフォルダをプロジェクトフォルダに入れる。  
phpファイルに以下の記述を入れる。

```PHP
require_once('Michelf/MarkdownExtra.inc.php');
use Michelf\MarkdownExtra;
```
### unEscMarkdownの使い方

さきほどのMarkdownExtra記法の文は、
これが $text に入っているとして、以下のようにする。

```
$newtext = unEscMark(htmlspecialchars($text, ENT_QUOTE, "UTF-8"));
$html = MarkdownExtra::defaultTransform($newtext);

<html><body>
  <?php echo $html; ?>
</body></html>
```
このようになる  
![Sample2](sample2.png)

***
&copy; 2018 Seiichi Nukayama
