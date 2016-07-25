# 查验单张发票

您可以调用此接口，并提供发票号码、发票代码、开票日期和校验码，来获取发票验证结果。此接口可查询任意增值税发票，包含电子发票和纸质的增值税普通发票和专用发票。

请求格式：

```http
http://<平台服务器地址>/mobile/validate/simple?code={invoiceCode}&crc={crcCode}&issueDate={issueDate}&number={invoiceNumber}
```

请求方式：GET

## 参数说明

| **参数**        | **示例**       | **长度** | **说明**                                   |
| ------------- | ------------ | ------ | ---------------------------------------- |
| invoiceNumber | 12345678     | 8      | 发票号码                                     |
| invoiceCode   | 123456781234 | 10或12  | 发票代码                                     |
| issueDate     | 20160501     | 8      | 开票日期                                     |
| crcCode       | NA           | 无限制    | 查询增值税普通发票、增值税电子发票、增值税卷式发票时，输入校验码后六位; 查询其他发票时，输入税前金额 |

## 正确返回结果示例

```
{
code: "031001600211",
number: "06615015",
issueDate: "2016-05-30 00:05:00",
crc: "274074",
from: "上海",
price: 113.21,
tax: 6.79,
total: 120,
totalInChinese: "壹佰贰拾园整",
sellerName: "<公司名称>",
sellerId: "91310000664332534E",
sellerOfficeInfo: "<公司地址信息>",
sellerBankInfo: "<公司银行账号信息>",
buyerName: "<买方名称>",
buyerId: " ",
buyerOfficeInfo: " ",
buyerBankInfo: " ",
deviceId: "499099123929",
wares: [
{
wareName: "<费用名称>",
wareType: " ",
wareUnit: "次",
wareCount: 6,
unitPrice: 113.21,
totalPrice: 113.21,
taxRate: 1,
taxNumber: 6.79
}
]
}
```

## 错误返回结果示例

```
{"code": "VALIDATION_EXPIRE_DAYLIMIT"}
```

### 错误代码说明

| **错误代码**                        | **错误说明**                        |
| ------------------------------- | ------------------------------- |
| VALIDATION_BODY_ERRORFORMAT     | 请求body格式有误                      |
| VALIDATION_EXPIRE_DAYLIMIT      | 超过该张发票的单日查验次数(5次)，请于24小时之后再进行查验 |
| VALIDATION_EXPIRE_IPLIMIT       | 本IP地址提交的查验请求过于频繁，请稍后再试          |
| VALIDATION_EXPIRE_SERVERLIMIT   | 超过服务器最大请求数，请稍后访问                |
| VALIDATION_ERROR_FORMAT         | 请求不合法                           |
| VALIDATION_INCONSISTANCE        | 不一致                             |
| VALIDATION_INVOICE_INEXIST      | 查无此票                            |
| VALIDATION_PROVINCE_UNAVAILABLE | 票据所在省份还未开通查询                    |