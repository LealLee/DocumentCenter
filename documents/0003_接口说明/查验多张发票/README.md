# 查验多张发票

您可以调用此接口，并提供发票号码、发票代码、开票日期和校验码，来获取多张发票验证结果。此接口可查询任意增值税发票，包含电子发票和纸质的增值税普通发票和专用发票。

请求格式：

```
http://平台服务器地址/mobile/validate/batch
```

请求方式：POST

请求header：

```
Content-Type: application/json
```

发送数据格式：发票信息

***注意：一次最多可查询10张发票数据。***

## 发送数据示例

```
[{"code":"031001600211", "number":"06615020", "issueDate":"20160708", "crc":"585006"},
 {"code":"031001600211", "number":"06615002", "issueDate":"20160430", "crc":"050595"},
 {"code":"031001600211", "number":"06615016", "issueDate":"20160530", "crc":"765219"},
 {"code":"011001600111", "number":"21479350", "issueDate":"20160530", "crc":"727008"}]
```

### 参数说明

| **参数**    | **示例**       | **长度** | **说明**                                   |
| --------- | ------------ | ------ | ---------------------------------------- |
| number    | 12345678     | 8      | 发票号码                                     |
| code      | 123456781234 | 10或12  | 发票代码                                     |
| issueDate | 20160501     | 8      | 开票日期                                     |
| crc       | NA           | 无限制    | 查询增值税普通发票、增值税电子发票、增值税卷式发票时，输入校验码后六位；查询其他发票时，输入税前金额 |

## 正确返回结果示例

多张发票的查验返回结果会被包含在同一份文件里:

- 如果单张发票查验正确，将会显示发票的详细信息，如发票号码、发票代码、卖方信息和买方信息等；
- 如果单张发票查验错误，将会显示一行错误代码。


```
{
  "21479350": "VALIDATION_EXPIRE_DAYLIMIT",
  "06615020": {
    "code": "031001600211",
    "number": "06615020",
    "issueDate": "2016-07-08 00:07:00",
    "crc": "585006",
    "from": "上海",
    "price": 1669.81,
    "tax": 100.19,
    "total": 1770,
    "totalInChinese": "壹仟柒佰柒拾园整",
    "sellerName": "<公司名称>",
    "sellerId": "91310000664332534E",
    "sellerOfficeInfo": "<公司地址信息>",
    "sellerBankInfo": "<公司账户信息>",
    "buyerName": "<买方名称>",
    "buyerId": " ",
    "buyerOfficeInfo": " ",
    "buyerBankInfo": " ",
    "deviceId": "499099123929",
    "wares": [
      {
        "wareName": "<费用名称>",
        "wareType": " ",
        "wareUnit": "次",
        "wareCount": 6,
        "unitPrice": 1669.81,
        "totalPrice": 1669.81,
        "taxRate": 1,
        "taxNumber": 100.19
      }
    ]
  },
  "06615002": {
    "code": "031001600211",
    "number": "06615002",
    "issueDate": "2016-04-30 00:04:00",
    "crc": "050595",
    "from": "上海",
    "price": -10,
    "tax": -0.6,
    "total": -10.6,
    "totalInChinese": "欠壹拾园陆角",
    "sellerName": "<公司名称>",
    "sellerId": "91310000664332534E",
    "sellerOfficeInfo": "<公司地址信息>",
    "sellerBankInfo": "<公司账户信息>",
    "buyerName": "<买方名称>",
    "buyerId": " ",
    "buyerOfficeInfo": " ",
    "buyerBankInfo": " ",
    "deviceId": "499099123929",
    "wares": [
      {
        "wareName": "<费用名称>",
        "wareType": " ",
        "wareUnit": "件",
        "wareCount": 6,
        "unitPrice": 10,
        "totalPrice": -10,
        "taxRate": -1,
        "taxNumber": -0.6
      }
    ]
  }
......
}
```

### 单张发票错误代码说明

| **错误代码**                        | **说明**                          |
| ------------------------------- | ------------------------------- |
| VALIDATION_EXPIRE_DAYLIMIT      | 超过该张发票的单日查验次数(5次)，请于24小时之后再进行查验 |
| VALIDATION_EXPIRE_IPLIMIT       | 本IP地址提交的查验请求过于频繁，请稍后再试          |
| VALIDATION_EXPIRE_SERVERLIMIT   | 超过服务器最大请求数，请稍后访问                |
| VALIDATION_ERROR_FORMAT         | 请求不合法                           |
| VALIDATION_INCONSISTANCE        | 不一致                             |
| VALIDATION_INVOICE_INEXIST      | 查无此票                            |
| VALIDATION_PROVINCE_UNAVAILABLE | 票据所在省份还未开通查询                    |

## 错误返回结果

如果请求数据格式不正确，系统将返回如下错误信息：

```
{"code": "VALIDATION_BODY_ERRORFORMAT"}
```