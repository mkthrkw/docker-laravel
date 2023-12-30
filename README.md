# docker-laravel

### プロジェクト作成
1. docker compose up -d でコンテナ作る  
（vendorをvolume mountをコメントアウトしておく。bind mountになる）
2. docker compose exec app bash でコンテナに入る
3. コンテナの/var/www/html/を空にする  
```rm -rf /var/www/html```
4. 「composer create-project "laravel/laravel=10.*" .」でプロジェクト作成
5. envのDB情報などを修正しておく
```
DB_HOST=dbのコンテナ名
DB_PORT=3306
DB_DATABASE=compose.ymlで設定
DB_USERNAME=compose.ymlで設定
DB_PASSWORD=compose.ymlで設定
```
6. 一度exit でコンテナから出て、vendorをvolume mounteに修正
7. 再度docker compose up -d --build で再ビルド
8. 「docker cp ./src/vendor {コンテナID}:/var/www/html/」にてコンテナ内にvendorの中身をコピー  
※docker ps でコンテナID調べる
9. もう一度docker compose exec app bash でコンテナに入る
10. storageディレクトリの所有者変更「chown -R www-data:www-data storage/*」
