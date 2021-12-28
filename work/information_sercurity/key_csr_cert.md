# 1 密钥、证书请求、证书
在证书**申请、签发**的过程中，客户端涉及到密钥、证书请求、证书这几个概念，一直搞不清楚这两者之间的关系，一头雾水。现在以*申请证书的*流程来说明三者的关系。客户端（相对于证书颁发者*CA*）在申请证书的时候，大致上有三个步骤：

- 第一步：生成客户端密钥。 即生成客户端的**公私钥对**，**<font color=#ff0000> 私钥只能自己留存</font>**。
- 第二步: 以客户端的密钥（公私钥）和客户端自己的信息（国家、机构、域名、邮箱等）为输入，生成证书请求文件。其中客户端的**公钥和客户端的信息**的信息是<font color=#ff0000> 明文</font>保存在证书请求文件中的。客户端的私钥作用是对客户端的公钥以及客户端信息签名。_**私钥自身是不会被放进证书中的**_。签名文件放到证书请求文件中，然后把证书请求文件发送给CA机构。
- 第三步： CA机构收到证书请求文件后，首先校验其签名，校验通过后，审核客户端的信息，最后CA机构使用自己的私钥为证书请求签名，生成证书文件，下发给客户端。此证书就是客户端的身份证，用来表明客户端的身份。

至此，客户端申请证书的流程结束，其中涉及到证书签发机构CA, CA是绝对被信任的。如果把证书比作身份证，那么CA就是颁发身份证的机构，以https为例，说明证书的用处：
- https握手阶段，服务器首先把自己的证书发送给客户端(*浏览器*)，
- 浏览器查看证书中的发证机构，然后在机器内置的证书中（在pc或者手机上，内置了世界上许多著名的CA机构证书）查找对应的CA证书，然后使用内置的证书公钥校验服务器传来的证书的真伪。如果校验失败，浏览器回提示证书有问题，询问用户是否继续。

# 2 openssl req 命令说明
```shell
openssl req [-inform PEM|DER] [-outform PEM|DER] [-in filename] [-passin arg] [-out filename] [-passout arg] [-text] [-pubkey] [-noout] [-verify] [-modulus] [-new] [-rand file(s)] [-newkey rsa:bits][-newkey alg:file] [-nodes] [-key filename] [-keyform PEM|DER] [-keyout filename] [-keygen_engine id] [-[digest]] [-config filename] [-subj arg] [-multivalue-rdn] [-x509] [-days n] [-set_serial n][-asn1-kludge] [-no-asn1-kludge] [-newhdr] [-extensions section] [-reqexts section] [-utf8] [-nameopt] [-reqopt] [-subject] [-subj arg] [-batch] [-verbose] [-engine id]
```
req的基本功能主要有两个：**生成证书请求**和**生成自签名证书** </br>
[new/x509]
当使用-new选取的时候，说明是要生成证书请求，当使用x509选项的时候，说明是要生成自签名证书。

- new/x509: -new 说明生成证书请求，x509生成自签名证书
- key/newkey/keyout: key/newkey互斥，key制定已有的密钥文件，newkey在生成证书请求或者证书时自动生成密钥，然后生成的密钥名称有keyout参数指定。当指定newkey选项时，后面指定rsa:bits说明产生rsa密钥，位数由bits指定。指定dsa:file说明产生dsa密钥，file是指生成dsa密钥的参数文件(由dsaparam生成)

- in/out/inform/outform/keyform： 
 - in选项指定证书请求文件，当查看证书请求内容或者生成自签名证书的时候使用 </br>
 - out选项指定证书请求或者自签名证书文件名，或者公钥文件名(当使用pubkey选项时用到)，以及其他一些输出信息。</br>
 - inform、outform、keyform分别指定了in、out、key选项指定的文件格式，默认是PEM格式。</br>

# 3 直接看openssl req 实例
- 利用原有的密钥生成证书请求
``` bash
openssl genrsa -out rsa_private.pem #生成rsa私钥
openssl rsa -pubout -in rsa_private.pem -out rsa_public.pem #生成公钥

openssl req -new -key rsa_private.pem -passin pass:123456 -out cert.csr #生成证书请求
#根据输入证书主体相关信息， 如国家、省份、城市、用户、邮箱等
```

- 自动生成新的证书请求
```bash
#使用新生成的密钥来生成证书请求
openssl req -new -newkey rsa:1024 -out cert.csr -keyout RSA.pem -batch -nodes #生成证书请求 生成新的密钥
openssl req -in cert.csr -noout -text -subject #查看证书请求文件主体
```
- 校验证书请求
```bash
penssl req -verify -in cert.csr -noout #校验证书请求，实质上就是用证书请求中的公钥验证其中的签名文件
```



[参考文章点我](https://www.cnblogs.com/gordon0918/p/5409286.html)
