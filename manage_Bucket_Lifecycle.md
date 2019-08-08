管理文件生命周期 
您可以通过OSS的PutBucketLifecycle接口设置生命周期规则（Lifecycle），自动删除过期的对象（Object）或将到期的Object转储为低频或归档存储类型，
从而节省存储费用。

说明： 设置生命周期的API详细信息可参考[PutBucketLifecycle](../../../../cn.zh-CN/API 参考/关于Bucket的操作/PutBucketLifecycle.md#)。

生命周期规则包含如下信息：

策略：生命周期规则匹配的Object。

按前缀匹配：按指定前缀匹配Object和碎片。可创建多条规则匹配不同的前缀，前缀不能重复。

配置到整个Bucket：匹配整个Bucket内的所有Object。此种方式只能创建一条规则。

文件过期策略：设置Object的过期时间及操作。

过期天数：指定一个过期天数N，并指定Object过期后执行什么操作。Object会在其最后修改时间的N天后过期，并执行指定的操作。
过期日期：指定一个过期日期，并指定Object过期后执行什么操作。最后修改时间在该日期之前的Object全部过期，并执行指定的操作。 说明： 针对过期Object可执行的操作为：转换到低频访问型存储、转换到归档型存储、删除。
碎片过期策略：设置碎片的过期时间及操作

过期天数：可指定一个过期天数N，文件碎片会在其最后修改时间的的N天后被删除。
过期日期：指定一个过期日期，最后修改时间在该日期之前的文件碎片会被全部删除。
只要Object名称前缀和一条规则的前缀匹配，那么该规则就适用于它。例如，一个Bucket有如下几个Object：

logs/program.log.1
logs/program.log.2
logs/program.log.3
doc/readme.txt
如果一个规则指定的前缀是logs/，那么该规则就适用于前三个以logs/开头的Object；如果前缀是doc/readme.txt，那么这条规则就只对doc/readme.txt起作用。

规则支持过期删除操作。例如，您可以设置这样的规则：当前缀为logs/的Object的最后一次更新是30天前，就删除它们；也可以指定在某年某月某日删除doc/readme.txt。

当一个Object匹配到某个过期规则，执行GET和HEAD操作时，OSS在响应Header中加入x-oss-expiration头。它包含了两个参数：expiry-date的值表示Object的过期日期；rule-id的值表示相匹配的规则ID。

操作方式 
操作方式	说明
控制台	Web应用程序，直观易用
[Java SDK](../../../../cn.zh-CN/SDK 示例/Java/生命周期.md#)	丰富、完整的各类语言 SDK demo
[Python SDK](../../../../cn.zh-CN/SDK 示例/Python/生命周期.md#)	
[PHP SDK](../../../../cn.zh-CN/SDK 示例/PHP/生命周期.md#)	
[Go SDK](../../../../cn.zh-CN/SDK 示例/Go/生命周期.md#)	
[C SDK](../../../../cn.zh-CN/SDK 示例/C/生命周期.md#)	
[.NET SDK](../../../../cn.zh-CN/SDK 示例/C/生命周期.md#)	
[Node.js SDK](../../../../cn.zh-CN/SDK 示例/Node.js/生命周期.md#)	
[Ruby SDK](../../../../cn.zh-CN/SDK 示例/Ruby/生命周期.md#)	
细节分析 
前缀、标签

前缀的命名规范和Object的命名规范一样。
当前缀为空时，表明该规则适用于Bucket里的所有Object。
任意两个前缀不能有重叠。例如，同一Bucket配置了两条规则，一条前缀是logs/，一条前缀是logs/program，那么OSS会返回错误。

当规则设置为在指定日期删除Object，该日期必须是UTC午夜零点，并且符合形如2017-01-01T00:00:00.000Z的ISO8601格式。OSS会在当前时间超过2017-01-01午夜零点时删除匹配的Object。
当规则设定为天数时，OSS把Object最后更新时间（Last-Modified）加上天数，再取整到下一个UTC午夜零点。例如，一个Object的最后更新时间是UTC的2017年4月12日上午1点，相匹配的规则定义的天数是3天，那么过期时间就是UTC 2017年4月16日0点整。
OSS会在指定时间删除与规则相匹配的Object。请注意，通常Object会在指定时间稍稍延后一段时间才被删除。
通常Object的最后更新时间和创建时间相差无几。当一个Object被多次Put时，最后更新时间是最后一次Put的时间；当一个Object被Copy到自身时，最后更新时间是Copy发生时的时间。
费用

成功的生命周期异步请求操作会记录在访问日志中并产生相关的请求次数费用，失败的不会被记录和收费。

规则冲突行为

前缀+标签相同

rule	prefix	tag	action
rule1	abc	a=1	20天后删除
rule2	abc	a=1	20天后转为Archive
执行结果：所有前缀为abc，标签为a=1的Object会在20天被删除（优先执行删除操作）。此时，文件已不存在，所以第二条规则已经没有意义。

rule	prefix	tag	action
rule1	abc	a=1	365天后转为IA（低频存储）
rule2	abc	a=1	2018-03-01前转为Archive
执行结果：前缀为abc且标签为a=1的Object如果同时满足两个规则，则转换为Archive；若仅满足其中一条，则按指定规则执行。

前缀重叠+标签相同

rule	prefix	tag	action
rule1	 	a=1	20天后转为IA
rule2	abc	a=1	120天后被删除
执行结果：所有标签为a=1的Object在20天后转为IA，前缀为abc且标签为a=1的Object会在120天后被删除。

rule	prefix	tag	action
rule1	 	a=1	10天后转为Archive
rule2	abc	a=1	20天后转为IA
执行结果：所有标签为a=1的Object会在10天后被转为Archive，前缀为abc且标签为a=1的Object在20天后转为IA的规则失效，因为Archive的文件无法转为IA。

常见问题 {#section_e1n_vlx_dgb .section}
通过设置生命周期转换文件类型或过期删除，是否有最小存储天数限制？

生命周期的文件类型转换没有最小存储天数限制（从Standard转IA、Archive，或从IA转Archive），但是数据过期删除有最小存储天数限制。数据过期删除最小存储天数按删除时文件存储类型来计算，低频存储文件至少保存30天，归档存储文件至少保存60天。

数据过期删除的最小存储天数是指从文件被创建开始到被删除时这段时间。若中间修改了文件，如通过CopyObject覆写、Append追加文件等操作时，存储天数从最后修改时间开始计算。

举例1：一个低频型文件，在创建10天后，通过生命周期转换为归档型。文件的创建时间不会变化，转换后的归档型文件，需再保存至少50天 。



举例2：一个低频型文件，在创建10天后，通过CopyObject覆写，将存储类型转换为归档型时，会产生20天的低频型文件提前删除费用；文件的创建时间会更新，转换后的归档型文件，需再保存至少60天。



请求次数计费逻辑

生命周期的类型转换或过期删除，会产生请求次数。OSS 按照请求次数收取标准费用。例如：

通过设置生命周期， 1000个Object，从标准转成归档，会产生1000次写类别请求次数（POST）。
通过设置生命周期， 1000个Object，过期删除，会产生1000次写类别请求次数（Delete）。 详细收费标准请参见计量计费。
通过生命周期的类型转换、过期删除，是否有日志记录？

通过生命周期的类型转换、过期删除，都有日志记录，日志记录字段如下：

Operation
CommitTransition：类型转换
ExpireObject：过期删除
Sync Request
lifecycle: 生命周期操作
