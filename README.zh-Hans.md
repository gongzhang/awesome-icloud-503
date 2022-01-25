# Awesome iCloud 503
帮助 Apple 跟踪和解决 iCloud 503 服务不可用的问题。

## 2021年11月 - iCloud 发生了什么？
我是一个苹果平台的独立应用开发者。大概从2021年11月（也许是10月）开始，陆续有用户向我报告我 App 中的 iCloud 同步功能完全无法工作了。典型的错误消息是：

```
<CKError: "Service Unavailable" (6/2022); "Request failed with http status code 503"; uuid = ...>
```

虽然这个错误在以往也出现过，但都是临时的，会很快自动恢复。但是这次情况不同：一旦用户遇到 iCloud 503 错误，就似乎再也没有办法自行恢复了。通过分析数据得知，我的应用大约有 1% - 2% 的用户受此问题困扰。

经过一番调研，我发现很多应用都遇到了相同问题。显然是 iCloud 自身出了毛病。由于没有有效的解决办法，遇到问题的用户只能彻底放弃使用应用中的 iCloud 同步功能，甚至直接放弃整个 App。

## 2021年12月 - 转机

2021 年 12 月中旬，情况开始出现转机。我应用的分析后台数据显示 iCloud 503 错误急剧减少。苹果似乎意识到了 iCloud 的问题，并进行了修复。然而不幸的是，同等数量的另一种 iCloud 错误开始出现：

```
<CKError: "Server Record Changed" (14/2004); server message = "record to insert already exists"; uuid = ...>
```

这个错误是我在使用 `CKModifyRecordsOperation` 更新一条数据时得到的。iCloud 似乎在告诉我：「你不能更新这条数据，因为这条数据已经存在了」。完全无法理解。

好消息是，我发现现在只要删除旧的 iCloud 数据后再重新写入一次，问题就可以完全解决。至此，我的用户们似乎有救了。

## 2022年1月10日 - 长达12小时的iCloud事故

2022年1月10日下午8点左右（CST），我突然发现我所有设备上的 iCloud 同步功能都无法工作了，不仅是我自己的 App，还包括第三方 App，甚至包括苹果的 App。没错，再次出现了 iCloud 503 错误，而且似乎是全球性的。

<img src="images/AppleSystemStatus.jpeg" width="200">

第二天早上（已过去 12 个小时），[苹果官方服务状态](https://www.apple.com/support/systemstatus/)页面开始暴露问题。大约又过了 1-2 小时，iCloud 服务逐渐恢复正常。

## 2022年1月下旬 - 回到原点

在1月10日的事故之后，我非常沮丧的发现 iCloud 503 问题似乎回到了原点。又开始有小部分用户遇到 iCloud 503 错误，且永远无法恢复。我至今没有帮我的用户们找到有效的解决办法。

## 相关报道和讨论

- [GoodNotes: iCloud sync stops working due to "Request failed with HTTP Status Code 503" error.](https://support.goodnotes.com/hc/en-us/articles/4410195261327-iCloud-sync-stops-working-due-to-Request-failed-with-HTTP-Status-Code-503-error-)
- [MacRumors: Developers Unhappy With Bug Causing iCloud Unreliability](https://www.macrumors.com/2022/01/24/developers-icloud-unreliability-bug/)
- [cnBeta.COM: 开发者抱怨iCloud服务器出现稳定问题 导致无法正常同步](https://www.cnbeta.com/articles/tech/1229847.htm)
