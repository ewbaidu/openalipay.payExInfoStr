# 海关跨境电商进口统一版信息化系统平台数据实时获取接口（php+js）


## 一、方案通知等附件
附件1 <br>
跨境电子商务零售进口统一版信息化系统原始数据实时获取方案<br>
2018年8月

1.文档说明
本文档描述跨境电商平台企业向海关开放支付相关原始数据接口，供海关实时获取的总体方案。
2.文档对象
序号	企业类别	说明
1	跨境电商平台企业	开展跨境业务的电商平台，参照本方案开放接口。
3.方案介绍
3.1.系统流程

1、跨境电商平台存储与支付企业的原始交易数据。
2、海关关员通过海关通关管理系统，实时对跨境电商平台支付相关原始数据抓取并进行验核。
3.2.网络通道
1、互联网+安全验证
通过互联网接入电子口岸对外接入网。
2、虚拟网关（VPN）
通过虚拟专线接入电子口岸对外接入网。
3、网络传输专线
通过物理专线接入电子口岸对外接入网。
3.3.部署开放数据接口
电商平台企业开放符合海关技术规范的原始数据接口（rest等方式），并需保证数据的真实性、完整性和不可否认性。
3.4.安全要求
根据业务需要，为了保证获取原始数据的安全性，需要对原始数据进行符合海关标准的加签加密。
3.5.接口内容
接口内容
元素	中文名称	名称	类型	说明	必填
payExchangeInfoHead
支付原始数据表头	系统唯一序号	Guid	C..36	企业系统生成36位唯一序号（英文字母大写）。	是
	原始请求	initalRequest	C..8000	跨境电商平台企业向支付企业发送的原始信息	是
	原始响应	initalResponse	C..8000	支付企业向跨境电商平台企业反馈的原始信息	是
	电商平台代码	ebpCode	C..18	电商平台的海关注册登记编号。	是
	支付企业代码	payCode	C..18	支付企业的海关注册登记编号。	是
	交易流水号	payTransactionId	C..60	交易唯一编号（可在央行认可的机构验证）	是
	交易金额	totalAmount	N19,5	实际交易金额	是
	币制	currency	C..4	实际交易币制（海关编码）	是
	验核机构	verDept	C1	1-银联 2-网联 3-其他	是
	支付类型	payType	C1	用户支付的类型。1-APP 2-PC 3-扫码 4-其他	否
	交易成功时间	tradingTime	C..14	交易支付时间。	是
	备注	note	C..1000		否
payExchangeInfoList
支付原始数据表体	订单编号	orderNo	C..60	交易平台的订单编号，同一交易平台的订单编号应唯一。订单编号长度不能超过60位。	是
	商品名称	gname	C..250	商品名称应据实填报。	是
	商品展示链接地址	itemLink	C..3000	商品展示链接地址应据实填报。	是
	收款账号	recpAccount	C..60	交易商品的卖方商户账号。电商平台自营商户应填写自营商户的收款账户；非自营电商应填写非自营商户的收款账户。	是
	收款企业代码	recpCode	C..18	应填写收款企业代码（境内企业为统一社会信用代码；境外企业可不填写）	否
	收款企业名称	recpName	C..100	应填写收款企业名称。	是
附件2 <br>
海关总署2018年165、179号公告相关企业接入流程和常见问题
近期，海关总署先后发布了2018年第165号、179号公告，要求自2019年1月1日起，参与跨境电子商务零售进口业务的跨境电商平台企业应当向海关开放支付相关原始数据，供海关验核。
距离2019年不足一个月，跨境电商平台企业如何按时完成企业接入工作？接入过程中遇到问题如何处理？为帮助企业尽快完成技术接入工作，在总署跨境电子商务统一版通关服务平台建设单位东方物通科技（北京）有限公司的支持下，我们收集和整理了企业接入流程和常见问题，供大家参考。
一、企业接入流程
（一）接口开发
企业参照海关总署2018年第179号公告内容，进行接口开发。
公告地址：
http://www.customs.gov.cn/customs/302249/302266/302269/2125253/index.html
（二）联调测试
1、接口开发完毕，电商平台企业联系中国电子口岸数据中心进行联调测试，由于电商平台企业较多，数据中心会根据实际情况为企业排期，开展联调测试工作。
2、企业可通过调用通关服务系统接口进行测试数据上传，企业通过联调realTimeDataUp接口返回实时数据。
联调realTimeDataUp接口地址：
https://swapptest.singlewindow.cn/ceb2grab/grab/realTimeDataUpload?
测试成功结果：
{"code":"10000","message":"上传成功","total":0,"serviceTime":1542337661665}?
测试失败结果：
{"code":"20000","message":"上传失败","total":0,"serviceTime":1542338687081}?
企业收到“上传成功”视为测试通过。
?3、企业联系联调时间尽量集中在12月15日—12月25日，也可以提前联系联调测试，错开高峰时段。
（三）线上接入
1、电商平台企业联调测试通过之后，即可进行线上接入。企业在通关服务系统注册实时数据抓取接口地址、证书信息，通关服务系统根据海关业务需求调用接口进行实时抓取，企业通过线上realTimeDataUp接口返回实时数据。
线上realTimeDataUp接口地址：
https://customs.chinaport.gov.cn/ceb2grab/grab/realTimeDataUpload
2、跨境通关服务系统会对企业注册的数据抓取服务地址进行业务测试，测试通过会将服务地址审核状态更置为审核通过。业务测试会随机抽取企业当天订单，在有效时间内返回结果视为通过，否则更置状态为审核不通过。
（四）正式启用
企业可对审核通过的地址勾选启用，企业可通过勾选启用的地址开放服务，供海关调用。
（五）其他说明
1、有关联通测试和系统对接等方面的疑问，请咨询中国电子口岸服务热线010-95198解决。联系人：张磊18652937075、丁鑫15901197073。
2、参照电子商务法，企业应留存至少三年的交易信息，海关根据监管需要抓取数据。
3、企业应保证其上传数据为真实、未加工的原始数据。
4、电商平台为数据的责任主体，电商平台对所提数据使用数字签名技术。
二、常见问题
1、如何对接海关，向海关提供实时数据？
参照总署发布的165、179号公告，开发服务接口，完成联调、对接上线，向海关返回实时数据。
2、是否需要通过地方公服、数据分中心进行数据交换？
根据总署公告要求，该类数据由电商平台企业直接与中国电子口岸数据中心对接获取。
3、若2019年1月1日未完成企业接入工作，有什么影响？
根据海关总署公告要求，相关支付原始数据作为海关验核依据。如果企业在规定时间未完成数据接入工作，海关监管过程中因无法获取验核数据，可能造成通关查验率提高，影响通关效率。
4、数据如何加签？
海关总署2018年179号公告对数据加签进行了详细说明，请参照公告对数据进行加签。
5、数据如何加密？
海关总署2018年179号公告对数据加密进行了详细说明，请参照公告对数据进行加密。由于数据涉密，企业通过https协议保证连接加密。
6、验核机构字段如何解读？
如果填1，根据支付企业返回的交易唯一编号与银联验核；如果填2，根据支付企业返回的交易唯一编号与网联验核；如果是3，可按实际情况填写。
7、交易唯一编号是否可以填写第三方支付平台系统内部流水号?
若该笔订单涉及的支付信息无法在银联或网联验核，即可填写系统内部流水号。
8、订单表体中一个商品有多个商品链接怎么办？
以“;”间隔开。
9、支付企业的返回结果不包含海关要求的字段怎么办?
建议电商平台与支付企业沟通解决。
10、“证书编号”是指什么？
企业在电子口岸申请证书后对应的序列号。
附件3 <br>
1.平台开放实时数据获取接口
1.1.服务说明
服务由通关管理系统通过通关服务系统调用企业应用系统的平台支付相关实时数据获取接口，由企业返回支付相关实时数据。
1.2.集成方式
http协议，method:post 请求调用。
1.3.数据接入
企业通过联调环境数据上传测试后，可在线上环境进行服务注册及上线。
1.3.1.数据上传测试
企业通过调用通关服务系统接口进行测试数据上传，企业通过联调企业返回实时数据接口返回实时数据。

联调企业返回实时数据接口地址： 
https://swapptest.singlewindow.cn/ceb2grab/grab/realTimeDataUpload

测试成功结果：
{"code":"10000","message":"上传成功","total":0,"serviceTime":1542337661665}  
测试失败结果：
{"code":"20000","message":"上传失败","total":0,"serviceTime":1542338687081}
1.3.2.线上接入
1、服务注册
企业通过在通关服务系统注册证书信息、一个或多个实时数据抓取接口地址。通关服务系统经审核通过后，根据海关业务需求调用接口进行实时抓取，企业通过线上企业返回实时数据接口返回实时数据。
2、服务变更
企业可在通关服务系统变更实时数据抓取接口地址、证书信息，通关服务系统审核通过后，重新启用该服务。


线上企业返回实时数据接口地址： 
https://customs.chinaport.gov.cn/ceb2grab/grab/realTimeDataUpload
	
1.4.加签说明
1.将数据内容所有数据一级节点使用||分割符拼接为连续字符串，使用IC卡、Ukey、服务类密码设备进行加签，将certNo（证书编号）、signValue（加签结果）补充入请求中。
2.IC卡、Ukey加签方法见附件-1 电子口岸控件说明-企业版签名接口
3.服务类密码设备加签可联系厂商进行技术支持。

加签原文样例：
initData:
”sessionID”:”fe2374-8fnejf97-32839218”||”payExchangeInfoHead": {data}||”payExchangeInfoList": [{data},{data}]||”serviceTime”:1533271903898
1.5.加密授权说明
外部系统调用跨境电子商务管理进口子系统的https接口确保安全调用接口,可参照附件2-上传平台实时数据样例进行开发。

1.6.功能简介
1.6.1.企业实时数据获取接口（部署在电商平台）
1.6.1.1.功能说明
服务定义	platDataOpen
功能说明	企业接收海关发起的支付相关实时数据获取请求
返回值	
说明	该接口为http形式


1.6.1.2.接口参数

参数名	类型	必填	传入/出	说明
orderNo	String	Y	In	申报订单的订单编号
sessionID	string	Y	In	海关发起请求时，平台接收的会话ID。
serviceTime	Long	Y	In	调用时的系统时间
参数说明

{
	"orderNo":"ord201800002",
	"sessionID": "fe2374-8fnejf97-32839218",
	"serviceTime":1533271903898
}
1.6.1.3.返回说明
返回Json格式数据

属性	类型	说明
code	String	状态代号。10000为正常调用值。
message	String	异常信息，正常时为空值
serviceTime	Long	系统响应时间
参数说明

{
	"code":"10000",
	"message":"",
	"serviceTime":1533271903898
}
1.6.2.企业返回实时数据接口（部署在通关服务系统）
1.6.2.1.功能说明
服务定义	realTimeDataUp
功能说明	企业返回海关所需获取的支付相关实时数据
返回值	ApiResult
说明	该接口为https形式
1.6.2.2.接口参数

参数名	类型	必填	传入/出	说明
payExInfoStr	string	Y	In	完整请求内容








payExInfoStr内容说明：

参数名	类型	必填	传入/出	说明
sessionID	string	Y	In	海关发起请求时，平台接收的会话ID。
payExchangeInfoHead	String	Y	In	支付原始数据表头
payExchangeInfoList	List	Y	In	支付原始数据表体
serviceTime	Long	Y	In	返回时的系统时间
certNo	String	Y	In	证书编号
signValue	String	Y	In	签名结果值

参数说明

{
"sessionID": "fe2374-8fnejf97-32839218",
	"payExchangeInfoHead": {
		"guid": "fe2374-8fnejf97-32839218",
		"initalRequest": "https://openapi.alipay.com/gateway.do?timestamp=2013-01-01 08:08:08&method=alipay.trade.pay&app_id=13580&sign_type=RSA2&sign=ERITJKEIJKJHKKKKKKKHJEREEEEEEEEEEE&version=1.0&charset=GBK&biz_content=\n {\n\"out_trade_no\":\"20150320010101001\",\n\"scene\":\"bar_code\",\n\"auth_code\":\"28763443825664394\",\n\"product_code\":\"FACE_TO_FACE_PAYMENT\",\n\"subject\":\"Iphone6 16G\",\n\"buyer_id\":\"2088202954065786\",\n\"seller_id\":\"2088102146225135\",\n\"total_amount\":88.88,\n\"trans_currency\":\"USD\",\n\"settle_currency\":\"USD\",\n\"discountable_amount\":8.88,\n\"body\":\"Iphone6 16G\",\n \"goods_detail\":[{\n \"goods_id\":\"apple-01\",\n\"goods_name\":\"ipad\",\n\"quantity\":1,\n\"price\":2000,\n\"goods_category\":\"34543238\",\n\"body\":\"特价手机\",\n\"show_url\":\"http://www.alipay.com/xxx.jpg\"\n }],\n\"operator_id\":\"yx_001\",\n\"store_id\":\"NJ_001\",\n\"terminal_id\":\"NJ_T_001\",\n\"extend_params\":{\n\"sys_service_provider_id\":\"2088511833207846\",\n\"industry_reflux_info\":\"{\\\\\\\"scene_code\\\\\\\":\\\\\\\"metro_tradeorder\\\\\\\",\\\\\\\"channel\\\\\\\":\\\\\\\"xxxx\\\\\\\",\\\\\\\"scene_data\\\\\\\":{\\\\\\\"asset_name\\\\\\\":\\\\\\\"ALIPAY\\\\\\\"}}\",\n\"card_type\":\"S0JP0000\"\n },\n\"timeout_express\":\"90m\",\n\"auth_confirm_mode\":\"COMPLETE：转交易支付完成结束预授权;NOT_COMPLETE：转交易支付完成不结束预授权\",\n\"terminal_params\":\"{\\\"key\\\":\\\"value\\\"}\"\n }\n",
		"initalResponse": "{\n \"alipay_trade_pay_response\": {\n \"code\": \"10000\",\n \"msg\": \"Success\",\n \"trade_no\": \"2013112011001004330000121536\",\n \"out_trade_no\": \"6823789339978248\",\n \"buyer_logon_id\": \"159****5620\",\n \"total_amount\": 120.88,\n \"trans_currency\": \"USD\",\n \"settle_currency\": \"USD\",\n \"settle_amount\": \"88.88\",\n \"pay_currency\": \"CNY\",\n \"pay_amount\": \"580.04\",\n \"settle_trans_rate\": \"1\",\n \"trans_pay_rate\": \"6.5261\",\n \"receipt_amount\": \"88.88\",\n \"buyer_pay_amount\": 8.88,\n \"point_amount\": 8.12,\n \"invoice_amount\": 12.5,\n \"gmt_payment\": \"2014-11-27 15:45:57\",\n \"fund_bill_list\": [\n {\n \"fund_channel\": \"ALIPAYACCOUNT\",\n \"bank_code\": \"CEB\",\n \"amount\": 10,\n \"real_amount\": 11.21\n }\n ],\n \"card_balance\": 98.23,\n \"store_name\": \"证大五道口店\",\n \"buyer_user_id\": \"2088101117955611\",\n \"discount_goods_detail\": \"[{\\\"goods_id\\\":\\\"STANDARD1026181538\\\",\\\"goods_name\\\":\\\"雪碧\\\",\\\"discount_amount\\\":\\\"100.00\\\",\\\"voucher_id\\\":\\\"2015102600073002039000002D5O\\\"}]\",\n \"voucher_detail_list\": [\n {\n \"id\": \"2015102600073002039000002D5O\",\n \"name\": \"XX超市5折优惠\",\n \"type\": \"ALIPAY_FIX_VOUCHER\",\n \"amount\": 10,\n \"merchant_contribute\": 9,\n \"other_contribute\": 1,\n \"memo\": \"学生专用优惠\",\n \"template_id\": \"20171030000730015359000EMZP0\",\n \"purchase_buyer_contribute\": 2.01,\n \"purchase_merchant_contribute\": 1.03,\n \"purchase_ant_contribute\": 0.82\n }\n ],\n \"auth_trade_pay_mode\": \"CREDIT_PREAUTH_PAY\",\n \"business_params\": \"{\\\"data\\\":\\\"123\\\"}\",\n \"buyer_user_type\": \"PRIVATE\",\n \"mdiscount_amount\": \"88.88\",\n \"discount_amount\": \"88.88\"\n },\n \"sign\": \"ERITJKEIJKJHKKKKKKKHJEREEEEEEEEEEE\"\n}",
		"ebpCode": "44069679AS",
		"payCode": "4403160BUF",
		"payTransactionId": "201808010XTOO180881108351",
		"totalAmount": 2000,
		"currency": "502",
		"verDept": "3",
		"payType": "1",
		"tradingTime": "20180705133320",
		"note": "备注"
	},
	"payExchangeInfoLists": [{
			"orderNo": "ord201808030001",
			"goodsInfo":[
                        {"gname": "小米盒子",
			"itemLink": "http://click.simba.taobao.com/cc_im?spm=a2e15.8261149.07626516002.1&p=?í??&s=1648065802&k=525&clk1=9f73e9cdcce965d198471b70ed0bd643&e=BmEuJDus6V0PZbqH6AbTJV0AKPHu3YhwVj/tY3U/BPnJRCjFyFQ8GHxmrU6Q+bkjDDPHzLdwU/etpQpyzbOjC5wBu0ordUSSMi7bCqPy47R1nIOYRCll+4+g7T1j2K+vML5LpUxRY23BdDKBL+XYG61TuZ6KTbzphgvsV4Ojz5jpcmo9XCws//tnCtUX8NyE5jc7bsfu1N4M1tX0LAzVL8Q/8Cb3PXX0Lg5CK0SP9A1GPZR1xBhowNfNkjqys1bd5jWRIP4BomXImyoaJy83WdBjdkAzm/0nUGlUh8jQ4hq8tVvOYh5jaAjZNGP6kg4m3CTQUO/p1GO/6+U5DeLwJLMyCLM4UCxLwYmDL9sJHo9BAnbfln/8xq83b9LkfalG081DbhBf6xDt6WwO7bF5pQdW8K5ahpAflCUwHLCjWUurCsD9ob8Lq6NckDlv0x6dd6spMGSy0l3cJNBQ7+nUY0qfAtCS17uKWJHDCg4IHl7OvKn1XZO6wl90By37YYjBRw4q/RI+UHU="},
                        {"gname": "零食",
			"itemLink": "http://click.simba.taobao.com/cc_im?spm=a2e15.8261149.07626516002.1&p=?í??&s=1648065802&k=525&clk1=9f73e9cdcce965d198471b70ed0bd643&e=BmEuJDus6V0PZbqH6AbTJV0AKPHu3YhwVj/tY3U/BPnJRCjFyFQ8GHxmrU6Q+bkjDDPHzLdwU/etpQpyzbOjC5wBu0ordUSSMi7bCqPy47R1nIOYRCll+4+g7T1j2K+vML5LpUxRY23BdDKBL+XYG61TuZ6KTbzphgvsV4Ojz5jpcmo9XCws//tnCtUX8NyE5jc7bsfu1N4M1tX0LAzVL8Q/8Cb3PXX0Lg5CK0SP9A1GPZR1xBhowNfNkjqys1bd5jWRIP4BomXImyoaJy83WdBjdkAzm/0nUGlUh8jQ4hq8tVvOYh5jaAjZNGP6kg4m3CTQUO/p1GO/6+U5DeLwJLMyCLM4UCxLwYmDL9sJHo9BAnbfln/8xq83b9LkfalG081DbhBf6xDt6WwO7bF5pQdW8K5ahpAflCUwHLCjWUurCsD9ob8Lq6NckDlv0x6dd6spMGSy0l3cJNBQ7+nUY0qfAtCS17uKWJHDCg4IHl7OvKn1XZO6wl90By37YYjBRw4q/RI+UHU="}
                         ],
			"recpAccount": "6217850100007893905",
			"recpCode": "1105910159",
			"recpName": "天猫国际有限公司"
		},
		{
			"orderNo": "ord201808030002",
			"goodsInfo":[
                        {"gname": "奶粉",
			"itemLink": "http://click.simba.taobao.com/cc_im?spm=a2e15.8261149.07626516002.1&p=?í??&s=1648065802&k=525&clk1=9f73e9cdcce965d198471b70ed0bd643&e=BmEuJDus6V0PZbqH6AbTJV0AKPHu3YhwVj/tY3U/BPnJRCjFyFQ8GHxmrU6Q+bkjDDPHzLdwU/etpQpyzbOjC5wBu0ordUSSMi7bCqPy47R1nIOYRCll+4+g7T1j2K+vML5LpUxRY23BdDKBL+XYG61TuZ6KTbzphgvsV4Ojz5jpcmo9XCws//tnCtUX8NyE5jc7bsfu1N4M1tX0LAzVL8Q/8Cb3PXX0Lg5CK0SP9A1GPZR1xBhowNfNkjqys1bd5jWRIP4BomXImyoaJy83WdBjdkAzm/0nUGlUh8jQ4hq8tVvOYh5jaAjZNGP6kg4m3CTQUO/p1GO/6+U5DeLwJLMyCLM4UCxLwYmDL9sJHo9BAnbfln/8xq83b9LkfalG081DbhBf6xDt6WwO7bF5pQdW8K5ahpAflCUwHLCjWUurCsD9ob8Lq6NckDlv0x6dd6spMGSy0l3cJNBQ7+nUY0qfAtCS17uKWJHDCg4IHl7OvKn1XZO6wl90By37YYjBRw4q/RI+UHU="},
                        {"gname": "拖鞋",
			"itemLink": "http://click.simba.taobao.com/cc_im?spm=a2e15.8261149.07626516002.1&p=?í??&s=1648065802&k=525&clk1=9f73e9cdcce965d198471b70ed0bd643&e=BmEuJDus6V0PZbqH6AbTJV0AKPHu3YhwVj/tY3U/BPnJRCjFyFQ8GHxmrU6Q+bkjDDPHzLdwU/etpQpyzbOjC5wBu0ordUSSMi7bCqPy47R1nIOYRCll+4+g7T1j2K+vML5LpUxRY23BdDKBL+XYG61TuZ6KTbzphgvsV4Ojz5jpcmo9XCws//tnCtUX8NyE5jc7bsfu1N4M1tX0LAzVL8Q/8Cb3PXX0Lg5CK0SP9A1GPZR1xBhowNfNkjqys1bd5jWRIP4BomXImyoaJy83WdBjdkAzm/0nUGlUh8jQ4hq8tVvOYh5jaAjZNGP6kg4m3CTQUO/p1GO/6+U5DeLwJLMyCLM4UCxLwYmDL9sJHo9BAnbfln/8xq83b9LkfalG081DbhBf6xDt6WwO7bF5pQdW8K5ahpAflCUwHLCjWUurCsD9ob8Lq6NckDlv0x6dd6spMGSy0l3cJNBQ7+nUY0qfAtCS17uKWJHDCg4IHl7OvKn1XZO6wl90By37YYjBRw4q/RI+UHU="}
                         ],
			"recpAccount": "6217850100007893905",
			"recpCode": "1105910159",
			"recpName": "天猫国际有限公司"
		}
	],
"serviceTime": 1533282603450,
"certNo": "1111100",
"signValue": "JANJXKMQ8WYkhuCDZC2PwhtSgrZpp+FUqvtsXUpMm7qZJxYHVTz2TSYyNUfg4KcDgAotBDyhf2ap2fK8sF2BcgHlq7s9lfyqKrSU32vObhMPu7GJEw+aD8mnHMH9EAbs7xqQrj117X4mYy7a2qEOGPd6plzfDKrCYowoDa+7yFk="
}
payExchangeInfoHead结果集属性描述
属性	类型	说明
guid	String	系统唯一序号
initalRequest	String	原始请求
initalResponse	String	原始响应
ebpCode	String	电商平台代码
payCode	String	支付企业代码
payTransactionId	String	交易流水号
totalAmount	double	交易金额
currency	String	币制
verDept	String	验核机构
payType	String	支付类型
tradingTime	String	交易成功时间
note	String	备注


payExchangeInfoList结果集属性描述
属性	类型	说明
orderNo	String	订单编号
goodsInfo	List	商品信息
recpAccount	String	收款账号
recpCode	String	收款企业代码
recpName	String	收款企业名称


goodsInfo属性描述
属性	类型	说明
gname	String	商品名称
itemLink	String	商品展示链接地址

1.6.2.3.返回说明
返回Json格式数据

属性	类型	说明
code	String	状态代号。10000为正常调用值。
message	String	异常信息，正常时为空值
serviceTime	Long	系统响应时间

参数说明

{
 "code":"10000",
"message":"",
"serviceTime":1533271903898
}


1.6.3.接口内容
接口内容
元素	中文名称	名称	类型	说明	必填
payExchangeInfoHead
支付原始数据表头	系统唯一序号	guid	C..36	企业系统生成36位唯一序号（英文字母大写）。	是
	原始请求	initalRequest	C..8000	跨境电商平台企业向支付企业发送的原始信息	是
	原始响应	initalResponse	C..8000	支付企业向跨境电商平台企业反馈的原始信息	是
	电商平台代码	ebpCode	C..18	电商平台的海关注册登记编号。	是
	支付企业代码	payCode	C..18	支付企业的海关注册登记编号。	是
	交易流水号	payTransactionId	C..60	交易唯一编号（可在央行认可的机构验证）	是
	交易金额	totalAmount	N19,5	实际交易金额	是
	币制	currency	C..4	实际交易币制（海关编码）	是
	验核机构	verDept	C1	1-银联 2-网联 3-其他	是
	支付类型	payType	C1	用户支付的类型。1-APP 2-PC 3-扫码 4-其他	否
	交易成功时间	tradingTime	C..14	交易支付时间。	是
	备注	note	C..1000		否
payExchangeInfoList
支付原始数据表体	订单编号	orderNo	C..60	交易平台向海关申报订单的的订单编号。需返回原始请求内的所有订单。	是
	商品信息	goodsInfo[]		商品名称及商品展示链接地址列表	
	收款账号	recpAccount	C..60	交易商品的卖方商户账号。电商平台自营商户应填写自营商户的收款账户；非自营电商应填写非自营商户的收款账户。	是
	收款企业代码	recpCode	C..18	应填写收款企业代码（境内企业为统一社会信用代码；境外企业可不填写）	否
	收款企业名称	recpName	C..100	应填写收款企业名称。	是
goodsInfo
商品信息	商品名称	gname	C..250	商品名称应据实填报。	是
	商品展示链接地址	itemLink	C..3000	商品展示链接地址应据实填报。	是



1.6.4.异常错误码表
code	msg
10000	成功
20000	失败
20001~21000	异常信息等。	

## 二、对接步骤
第一步获得证书：首先准备一台前置机（需24小时开机），插入企业UKEY，进对接微信群下载debug.rar，解压后打开SignTool，打开卡验证口令读取证书（证书序列号需记下，注册和拼接原始数据需要）。
复制字符串到新建的文本文档，改文档后缀为.cer。

第二步按文档编写代码：
```
	//获取海关请求	
$openReq=stripslashes($_POST['openReq']);
	//json转数组
$openReqarr=json_decode($openReq,true);
	//反馈海关
$arr = array('code'=>10000,'message'=>'OK','serviceTime'=>$serviceTime);
echo json_encode($arr);
	//根据海关请求的orderNo字段拼接完成原始数据（值作相应替换） ，把原始数据写入数据库
"sessionID":"c5476b-28c880ea-144368bd"||"payExchangeInfoHead":"{"guid":"4EFBB04B-606B-48D5-B488-BA25582C6092","initalRequest":"https://openapi.alipay.com/gateway.do?out_trade_no=2019030466666&partner=0000000000&payment_type=1&price=88.08&sign_type=MD5&sign=d9bb64ba95f6486b95d0c689e67d9e96&charset=utf-8","initalResponse":"{s:4:code;s:6:alipay;s:8:discount;s:4:0.00;s:12:payment_type;s:1:1;s:8:trade_no;s:28:2019030422001476301029024026;}","ebpCode":"4101660000","payCode":"4403160BUF","payTransactionId":"2019030422001476301029024026","totalAmount":88.08,"currency":"142","verDept":"3","payType":"1","tradingTime":"1551634298","note":"abc"}"||"payExchangeInfoLists":"[{"orderNo":"2019030466666","goodsInfo":[{"gname":"黛尔德美深度抗皱修复纯天然日霜50ml","itemLink":"http://www.0000000.com/goods.php?id=1996"},{"gname":"黛尔德美精油滋养深度补水面霜50ml","itemLink":"http://www.00000000.com/goods.php?id=1998"}],"recpAccount":"000000.com","recpCode":"000000000M","recpName":"000000有限公司"}]"||"serviceTime":"1553047681"
	//前置机（安装中国电子口岸客户端控件）写js轮询，读到数据库中新增原始数据做加签。关键代码
$.ajax({
            type:"post",
			async: false,
            url: "http://www.0000000.com/alipay.php",//访问的链接
            dataType:"jsonp",  //数据格式设置为jsonp
			jsonp:'callback', 
            jsonpCallback:"successCallback",
			contentType: "application/json;charset=UTF-8", 
            error: function(XMLHttpRequest, textStatus, errorThrown) {
            	        //200
                        alert("status:"+XMLHttpRequest.status);
                        //4
                        alert("state:"+XMLHttpRequest.readyState);
                        //parsererror 类型转换错误 
                        alert("textstatus:"+textStatus);
                    },	
		success : function(resp){
          
             var id=JSON.stringify(resp[0].id);
		 var payExInfoStr=JSON.stringify(resp[0].payExInfoStr);
		 payExInfoStr = payExInfoStr.replace(/[\\]/g,'');
		 payExInfoStr =payExInfoStr.replace(/^\"|\"$/g,'');//去除payExInfoStr 前后的双引号
		 console.log(payExInfoStr);
		 EportClient.isInstalledTest(EportClient.cusSpcSignDataAsPEM,
			payExInfoStr,"88888888",function(msg,msgJson){
			var data=JSON.stringify(msg);
			var jsObject = JSON.parse(data); //转换为json对象
			var signdata=jsObject.Data[0];
			console.log(signdata);
			console.log(id);
			$.ajax({
					type: 'POST',
					url: "http://www.0000000.com/sign.php",//
					data: {sign:signdata,id:id},
					success: function(resp){
						     console.log(resp);
											}
  
					}); 
									});
			 
			                  }
		})
	//sign.php 获取sign和对应id
$sign= $_POST['sign'];
$id= stripslashes($_POST['id']);
$id=str_replace('"', '', $id);		
//    $sendUrl = 'https://swapptest.singlewindow.cn/ceb2grab/grab/realTimeDataUpload'; //测试接口的URL
//    $sendUrl = 'https://customs.chinaport.gov.cn/ceb2grab/grab/realTimeDataUpload'; //正式接口的URL
	//拼接加签后数据为$payExInfoStr
$payExInfoStr=array(
                "payExInfoStr" => $payExInfoStr,
      );
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL, $sendUrl);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
    curl_setopt($ch, CURLOPT_POST, 1);
    curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
    curl_setopt($ch, CURLOPT_POSTFIELDS, $payExInfoStr);
    $res = curl_exec($ch);
    curl_close($curl);
    echo  $res;
```
