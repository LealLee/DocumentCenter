# 查询及下载单张发票版式文件

您可以调用此接口，并提供发票号码和发票代码，来查询、下载单张发票版式文件。
请求格式：

```http
http://<平台服务器地址>/einvoice/integration/e-invoices/file?invoiceNumber={invoiceNumber}&invoiceCode={invoiceCode}&tax_num={tax_num}
```

请求方式：GET

## 参数说明

| **参数**        | **示例**             | **长度** | **说明** |
| ------------- | ------------------ | ------ | ------ |
| invoiceNumber | 12345678           | 8      | 发票号码   |
| invoiceCode   | 123456781234       | 12     | 发票代码   |
| tax_num       | 110109004357777777 | 20     | 税号     |

## 正确返回结果

以流的方式返回版式文件。

### 返回头相关信息

```
Content-Disposition →attachment;filename=74d1e54e-7027-4ffb-a5ba-0ff91b4e4a48.pdf
Content-Type →application/pdf; charset=UTF-8
```

## 错误返回示例

```
{"code": "INVOICE_QUERY_FACTORS_INCOMPLETE"}
```

### 错误代码说明

| **错误代码**                         | **错误说明**  |
| -------------------------------- | --------- |
| INVOICE_QUERY_FACTORS_INCOMPLETE | 请求参数不完整   |
| INVOICE_NOT_EXISTS               | 发票数据不存在   |
| INVOICE_WITHOUT_COMPONENT        | 发票版式文件不存在 |
| GENERIC_API_ERROR_CODE           | 服务器程序异常   |