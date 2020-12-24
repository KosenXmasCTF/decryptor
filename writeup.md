# 脆弱性

こちらが暗号文を選んで復号することができるので、選択暗号文攻撃が可能です。

また、フラグの暗号文も教えられているので適応的選択暗号文攻撃 (CCA2) が可能です。

# 解法

こちらの記事が詳しいです。

http://inaz2.hatenablog.com/entry/2016/01/26/222303

フラグをmf, フラグを暗号化した文字列をcfとします。

RSAの暗号化の式は`c = m^e mod N`、復号化の式は`m = c^d mod N`です。

フラグを復号化したいですが、そのままでは弾かれるので工夫して回避する必要があります。

フラグをmf、暗号化されたフラグをcfとすると、式より`cf = mf^e mod N`です。

cfに何かをしてから暗号文として送信して、復号の式を`m = (cfと何か)^d mod N`の形にできれば`mfと何か`という平文が返ってくるんじゃないか？と考えます。

cfに何をするかですが、累乗には`a^c * b^c = (ab)^c`という性質があります。

これを使います。適当な数rを決めて、`cf * r^e`を暗号文として入れてみます。

すると、cfの式より`m = (mf * r)^e mod N`という式になり、`mf * r`が平文として得られます。

あとはそれをrで割れば、mfが得られます。