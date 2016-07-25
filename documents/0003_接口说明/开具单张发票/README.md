# 开具单张发票

您可以调用此接口，发送XML报文数据，来开具单张电子发票。

请求格式：

```http
http://<平台服务器地址>/einvoice/handle/save
```

请求方式：POST
发送数据格式：XML报文数据

## 发送数据示例

```xml
<?xml version="1.0" encoding="gbk"?>
<business id="FPKJ">
<CUSTOMDATA>
<DDXXS LSH="97561137630527787265">
<DDXX>
<ZDDH>10000062</ZDDH>
</DDXX>
</DDXXS>
</CUSTOMDATA>
<REQUEST_COMMON_FPKJ>
<COMMON_FPKJ_FPT>
<FPLX>026</FPLX>
<KPLX>0</KPLX>
<XSF_NSRSBH>销售方纳税人识别号</XSF_NSRSBH>
<XSF_MC>销售方名称</XSF_MC>
<XSF_DZ>销售方地址</XSF_DZ>
<XSF_DH>销售方电话</XSF_DH>
<XSF_YHZH>销售方银行账号</XSF_YHZH>
<GMF_NSRSBH>购买方纳税人识别号</GMF_NSRSBH>
<GMF_MC>购买方名称</GMF_MC>
<GMF_DZ>购买方地址</GMF_DZ>
<GMF_DH>购买方电话</GMF_DH>
<GMF_YHZH>购买方银行账号</GMF_YHZH>
<KPR>bw0701</KPR>
<SKR>bw0701</SKR>
<FHR>bw0701</FHR>
<YFP_DM/>
<YFP_HM/>
<JSHJ>58.50</JSHJ>
<HJJE>55.19</HJJE>
<HJSE>3.31</HJSE>
<BZ>备注</BZ>
</COMMON_FPKJ_FPT>
<COMMON_FPKJ_XMXXS>
<COMMON_FPKJ_XMXX>
<FPHXZ>0</FPHXZ>
<XMMC>项目名称</XMMC>
<DW/>
<GGXH/>
<XMSL>1</XMSL>
<XMDJ>55.19</XMDJ>
<XMJE>55.19</XMJE>
<SL>0.06</SL>
<SE>3.31</SE>
<HSBZ>0</HSBZ>
</COMMON_FPKJ_XMXX>
</COMMON_FPKJ_XMXXS>
</REQUEST_COMMON_FPKJ>
</business>
```

### 参数说明

| **索引**           | **参数名**    | **含义**    | **长度** | **是否必须** | **说明**                                   |
| ---------------- | ---------- | --------- | ------ | -------- | ---------------------------------------- |
| 1                | LSH        | 交易流水号     | 20     | 是        | 对应唯一一笔开票业务，20位数字                         |
| 2                | ZDDH       | 订单号码      | 20     | 是        |                                          |
| 3                | KPLX       | 开票类型      | 4      | 否        | 0：蓝字发票  1：红字发票                           |
| 4                | XSF_NSRSBH | 销售方纳税人识别号 | 20     | 是        |                                          |
| 5                | XSF_MC     | 销售方名称     | 100    | 是        | 销售方名字需要和税控系统内的配置相对应                      |
| 6                | XSF_DZ     | 销售方地址     | 100    | 是        |                                          |
| 7                | XSF_DH     | 销售方电话     | 100    | 是        |                                          |
| 8                | XSF_YHZH   | 销售方银行账号   | 100    | 否        |                                          |
| 9                | GMF_NSRSBH | 购买方纳税人识别号 | 20     | 否        |                                          |
| 10               | GMF_MC     | 购买方名称     | 100    | 是        |                                          |
| 11               | GMF_DZ     | 购买方地址     | 100100 | 否        |                                          |
| 12               | GMF_DH     | 购买方电话     | 100    | 否        |                                          |
| 13               | GMF_YHZH   | 购买方银行账号   | 100    | 否        |                                          |
| 14               | KPR        | 开票人       | 8      | 是        | 最多10个汉字                                  |
| 15               | SKR        | 收款人       | 8      | 否        |                                          |
| 16               | FHR        | 复核人       | 8      | 否        |                                          |
| 17               | YFP_DM     | 原发票代码     | 12     | 否        | 红字发票时不可为空                                |
| 18               | YFP_HM     | 原发票号码     | 8      | 否        | 红字发票时不可为空                                |
| 19               | JSHJ       | 价税合计      |        | 是        | 单位：元（2位小数）                               |
| 20               | HJJE       | 合计金额      |        | 是        | 不含税，单位：元（2位小数）                           |
| 21               | HJSE       | 合计税额      |        | 是        | 单位：元（2位小数）                               |
| 22               | BZ         | 备注        | 255    | 否        |                                          |
| 23               | GMF_SJH    | 购买方手机号    | 48     | 否        |                                          |
| 24               | GMF_DZYX   | 购买方电子邮箱   | 100    | 否        |                                          |
| 项目明细，可多条(最大100条) |            |           |        |          |                                          |
| 25               | FPHXZ      | 发票行性质     | 1      | 是        | 0：正常行   1：折扣行  2：被折扣行                    |
| 26               | XMMC       | 项目名称      | 90     | 是        | 在发票和销货清单中，可在每一行商品下加入折扣行，折扣行商品名称栏填写“折扣（X.XXX%）”字样，其中“X”为折扣率数字，金额和税额栏以负数填写，税率与被折扣行商品税率相同，其它栏不填写。  对于相邻商品行折扣率相同的，可汇总填写折扣行，折扣行商品名称栏填写“折扣行数Y(X.XXX%)”字样，其中“Y”为汇总行数数字，汇总金额和汇总税额栏以负数填写，税率与发票税率相同，其它栏不填写。 |
| 27               | DW         | 计量单位      | 20     | 否        |                                          |
| 28               | GGXH       | 规格型号      | 40     | 否        |                                          |
| 29               | XMSL       | 项目数量      |        | 否        | 小数点后6位                                   |
| 30               | XMDJ       | 项目单价      |        | 否        | 小数点后6位，不含税                               |
| 31               | XMJE       | 项目金额      |        | 是        | 不含税，单位：元（2位小数）                           |
| 32               | SL         | 税率        |        | 是        | 2位小数，例1%为0.01                            |
| 33               | SE         | 税额        |        | 是        | 单位：元（2位小数）                               |
| 34               | HSBJ       | 含税标志      | 1      | 是        | 0：不含税  1：含税                              |

## XML响应示例

```
<rtnmsg>
<returncode>返回代码</returncode>
<returnmsg>返回信息</returnmsg>
<returndata>
<fpdm>发票代码</fpdm>
<fphm>发票号码</fphm>
<kprq>开票日期</kprq>
</returndata>
</rtnmsg>
```