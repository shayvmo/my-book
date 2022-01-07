## http 和 https 的区别



### 端口

- http 80
- https 443



### 安全性和服务器消耗

- http 协议运行在TCP之上，所有信息都是明文传输，客户端和服务端无法校验对方身份
- https 协议运行在SSL/TLS 之上的 http 协议，加密传输的内容，内容加密使用对称加密，对称加密的秘钥使用服务方证书进行了非对称加密。
- 相比而言，https 比 http 安全性更高，但是消耗服务器资源更多





### 对称加密

> 只有一个秘钥，加密解密同用一个秘钥，加密速度快



#### 典型对称加密算法

- DES 
- AES



### 非对称加密

> 秘钥成对出现，加密使用公钥，解密使用私钥，公私钥两者之间无法反推



#### 典型的非对称加密算法

- RSA
- DSA



#### RSA

算法流程：

（1）任意选取两个不同的大素数p和q计算乘积

![img](https://bkimg.cdn.bcebos.com/formula/f0dac18152076624d87832b62709895c.svg)

​	注：图中生僻字母读 fai 



（2）任意选取一个大整数e，满足

![img](https://bkimg.cdn.bcebos.com/formula/c33d8c66364a636b051d82f0ee202a36.svg)

 ，整数e用做加密钥（注意：e的选取是很容易的，例如，所有大于p和q的素数都可用。gcd 最大公约数）



（3）确定的解密钥d，满足

![img](https://bkimg.cdn.bcebos.com/formula/da8649c0078a0a842779394d64011776.svg)

 ，即

![img](https://bkimg.cdn.bcebos.com/formula/4dee3f4df52a81983db0e3c619f96058.svg)

 是一个任意的整数；所以，若知道e和

![img](https://bkimg.cdn.bcebos.com/formula/679e809a0d964785d0aa4cfcb4218742.svg)

，则很容易计算出d ；

（4）公开整数n和e，秘密保存d ；

（5）将明文m（m<n是一个整数）加密成密文c，加密算法为 [5] 

![img](https://bkimg.cdn.bcebos.com/formula/5947116555169dc6fe9e3f5cdf347706.svg)

（6）将密文c解密为明文m，解密算法为 [5] 

![img](https://bkimg.cdn.bcebos.com/formula/1a8b337167e4d4b2c23855d88ec4c67f.svg)

然而只根据n和e（注意：不是p和q）要计算出d是不可能的。因此，任何人都可对明文进行加密，但只有授权用户（知道d）才可对密文解密 。



