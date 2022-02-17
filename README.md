# 20220217_traning

Remember-Me 認証の動作を確認するデモアプリです。

## How to use

1. Spring Boot で起動後、 `http://localhost:8080` にアクセスし、 `/login` に遷移されることを確認します。
2. `user` `password` をそれぞれ入力し、ログインします。チェックボックスは任意です。
3. `/` に遷移することを確認します。
4. ログアウトボタンをクリックした場合、 `/login` に遷移されることを確認します。  
   ログアウトボタンで意図的にログアウトした場合、自動ログインも解除されます。

## Remember-Me 認証

以下の動作を確認しています。  
Cookie はブラウザの開発者ツールで確認しています。

| 行動                                                   | 結果                                                                |
| :----------------------------------------------------- | :------------------------------------------------------------------ |
| チェックボックスなしでログイン                         | Cookie に JSESSIONID が生成                                         |
| チェックボックスありでログイン                         | Cookie に JSESSIONID と remember-me が生成                          |
| Cookie に JSESSIONID ありで `/` 遷移                   | `/` 遷移成功                                                        |
| Cookie に JSESSIONID なし・remember-me ありで `/` 遷移 | `/` 遷移成功・JSESSIONID が生成                                     |
| Cookie に JSESSIONID なし・remember-me なしで `/` 遷移 | `/` 遷移失敗( `/login` に遷移)                                      |
| ログイン後 60 秒経過してからページをリロード           | remember-me が消滅 (※有効期限は.tokenValiditySeconds()で可変します) |

## 参考サイト

[Remember-Me 認証 :: Spring Security - リファレンス](https://spring.pleiades.io/spring-security/reference/servlet/authentication/rememberme.html)  
[org.springframework.security.web.authentication.rememberme (spring-security-docs 5.6.1 API) - Javadoc](https://spring.pleiades.io/spring-security/site/docs/current/api/org/springframework/security/web/authentication/rememberme/package-summary.html)  
[RememberMeConfigurer (spring-security-docs 5.6.1 API) - Javadoc](https://spring.pleiades.io/spring-security/site/docs/current/api/org/springframework/security/config/annotation/web/configurers/RememberMeConfigurer.html)  
[Spring Security 使い方メモ　 Remember-Me - Qiita](https://qiita.com/opengl-8080/items/7c34053c74448d39e8f5#%E5%8B%95%E4%BD%9C%E7%A2%BA%E8%AA%8D)  
[Spring Security Remember Me | Baeldung](https://www.baeldung.com/spring-security-remember-me)
