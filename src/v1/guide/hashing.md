---
title: 哈希
type: guide
order: 231
---

## 哈希

哈希库为您提供了一些常用的哈希函数。您可以通过这些函数安全的加密用户的密码，验证文件的有效性等。

### 支持的哈希

- 一致性哈希
-- `Adler32`
-- `Crc32`

- 加密哈希
-- `BCrypt`

- 分布式哈希
-- `Murmur Hash 3`
-- `Djb Hash`

### 使用一致性哈希

您可以通过`Checksum`方法来调用一致性哈希，方法接收2个参数，一个参数为输入值，第二个参数为使用的一致性哈希算法。

``` csharp
var hashing = App.Make<IHashing>();
byte[] data; // 假定需要加密的数据
long hashCode = hashing.Checksum(data , Checksums.Crc32);
```

### 使用加密哈希

通过`HashPassword`方法您可以调用加密哈希，加密哈希接受2个参数，第一个参数为输入值，第二个参数为加密因子，加密因子默认为10，值越大则运行越慢，但越安全。加密Hash可以有效的保护您的密码。

``` csharp
var hashing = App.Make<IHashing>();
string data; // 假定需要加密的数据
long hashCode = hashing.HashPassword(data , 10);
```

**验证加密哈希和输入值是否匹配**

您可以通过`CheckPassword`来验证加密哈希和输入值是否匹配。

``` csharp
var hashing = App.Make<IHashing>();
bool isMatch = hashing.HashPassword("输入值" , "加密的哈希");
```

### 使用分布式哈希

您可以通过`HashString`方法和`HashByte`方法来进行分布式哈希。

``` csharp
var hashing = App.Make<IHashing>();
uint hashCode = hashing.HashString("输入值" , Hashes.MurmurHash);
```