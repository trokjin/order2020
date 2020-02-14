# Order 2020
## Order主要属性
### 订单编号
> 订单的身份ID,源自各个平台的数据迁移,如阿里订单号
### 状态
| 项目 | 说明 |
| -| - |
| <span style="color:red">关闭</span>  | 无交易的订单可以关闭,关闭后的订单除非激活,不能进行任何交易 |
| <span style="color:green">活跃</span> | 有[代办事宜](#daibanshiyi)的订单为活跃订单 |
|  - | 进行完所有交易的订单 | 
### 代办事宜<a name="daibanshiyi"></a >
> 订单需要处理的主要代办事宜

| 项目 | 说明 |
| - | - |
| 超卖 | 订单明细存在超卖，需要进行超卖转化或修改 |
| 审单 | 订单未审核,只能进行审核或者关闭处理,或者订单修改后进行审核 |
| 派发 | 订单未授予发货方,分配委托发货方进行发货 |
| 发货 | 发货方未完成发货,发货方进行发货 | 
| 同步 | 订单信息未来同步给下单方 |
| 收货 | 换货过程中等待售后接收退货 |
| 其他 | 特殊订单类型的特殊业务 |

## 使用Order的角色
角色下涉及的相关的Order类型,不同角色拥有不同的订单类型权限
- 审单
- 客服(自营,分销)
- 运营
- 分销
- 唯品会
- 零售
- Boss
- 信息

## Order类型
拥有特殊的属性,以及需要特殊的处理隔离
- 天猫
- 分销
- 奥莱
- 海外
- 家纺
- 唯品入仓
- JIT
- JITX
- 微商城
- 苏宁
- 门店

## Order 模块
| 项目 |
| - |
| [订单信息](#dingdanxinxi) |
| [业务处理](#yewuchuli) |  
| [业务查询](#yewuchaxun) |  
| [定制业务查询](#dingzhiyewuchaxun) |  
| 统计 |

### 订单信息<a name="dingdanxinxi" />
| 项目 | 说明 |
| -| - |
| 查询条件 | 根据查询条件显示符合的订单队列 |
| 订单队列显示 | 用简要的信息显示查询得到的队列列表 |
| 订单详细信息 | 显示订单的详细信息 |
#### 查询条件
##### 常规
大致如下
| 优先级 | 项目 | 说明 |
| -| - | - |
| 1 | 订单编号 | 根据订单号队列查询订单 |
| 2 | 时间 | 范围时间内的订单集合 |
| 3 | 属性过滤 | 根据属性过滤订单 |

##### 指令
> 预置指令 不同的角色查询时候的特殊预置查询条件,例如:

| 项目 | 说明 |
| -| - |
| 代理未发货查询 | 查询未完成的代理订单 |
| 线下发货超时 | 查询超时发货 |

根据查询条件获取的订单队列以及当前的查询条件一并存在于模块中,用2个视图呈现结果.
##### 订单队列显示
符合条件的订单显示在列表中,根据使用角色的不同显示直观重要的数据列,由行可以导航至订单详细信息

##### 订单详细信息
订单详细信息显示了订单的所有信息,每次显示一个订单附加所属列表的导航工具 
定单详细信息主要构成

| 项目 | 说明 |
| -| - |
| **常规属性** | 创建时间,审核时间,平台,数量,金额,收件人信息,快递,发票等等 |
| **订单类型属性** | 海外件运单,下单门店店铺,唯品会时段 |
| **订单明细列表** | 当前订单有效的明细队列 |
| **发货派发情况** | 当前订单委托的发货任务 |
| **出库明细列表** | 发货任务完成后生成的包裹队列|
| **退货明细列表** | 当前订单产生的退货丢件信息 |
| **操作追溯** | 记录了此订单的操作记录,便于客服等查询 |

###### 订单明细
>未产生出库数据的明细可以修改

| 项目 | 说明 |
| -| - |
| **SKU** | 需发的SKU |
| **数量** | 需发数量 |
| **金额** | 金额 |
| **是否赠品** | 金额 |
| **完成度** | 预览当前商品的出库情况 |

>出库跟退货影响完成度

###### 发货派发情况
>无法派发因为快递收件人等问题
> 无法派发因为缺货

列举了派发出去的正在进行中的发货任务
| 项目 | 说明 |
| -| - |
| **发货方** | 物流园,分仓,门店 |
| **通知单** | 派发通知单 |
| **状态** | 出库完成、退单,取消发货 |

###### 出库明细列表

列举了出库包裹
| 项目 | 说明 |
| -| - |
| **运单** | 包裹运单 |
| **通知单** | 派发通知单 |
| **发货方** | 物流园,分仓,门店 |
| **出库时间** | 出库时间 |
| **同步状态** | 是否向下单方同步状态 |
| **拓展** | 第三方快递状态调用 |

###### 退货明细列表

列举了订单的退货
| 项目 | 说明 |
| -| - |
| **运单** | 退货包裹运单 |
| **类别** | 接收,丢件,换货申请 |
| **状态** | 丢件补单,丢件退款,补单,退款,未接收换货申请 |
| **接收时间** | 接收入库时间 |
| **接收方** | 物流园,分仓,门店 |
| **冲突** | 如果产生的收货记录对应的SKU无法匹配订单或者换货申请,则需要售后客服处理退回疑难件,或者进行换货转退货 |


> 退货明细涉及反审，反审流程    
> 丢件涉及丢件处理结果  
> 操作体现在操作记录


###### 操作追溯
记录当前订单的操作日志
| 项目 | 说明 |
| -| - |
| **时间** | 发生时间 |
| **执行者** | 用户,系统 |
| **事件** | 进行的操作说明 |

事件
- 下单
- 审核
- 推送DDDD通知单号至FFFF
- FFFF出库包裹EEEEEEEEE
- NN办理换货申请
- XXXX接收退货[SKU]
- AAAA关闭订单


### 定制业务处理<a name="dingzhiyewuchaxun" />
>不同角色显示其可以处理的业务,比如审单人员显示的是查询得到的未审核订单的业务队列,售后客服显示的是售后丢件处理,或者售后快递商品不匹配异常等  
>派发的发货通知的进度,换货的退货接收等
>主要
| 项目 | 说明 |
| -| - |
| 查询条件 | 根据查询条件显示符合的业务队列 |
| 处理界面 | 显示业务的详细信息 |

主要的业务处理
| 项目 | 说明 |
| -| - |
| 超卖/缺货 | 重新匹配库存占用 |
| 审核 |  |
| 售后冲突 | 串货处理等 |
| 出库资料异常 | 无法出库,需要修改收件人信息,或者快递信息 |


<table>
    <tr><td><input placeholder="order no"/><button>Seach</button></td></td></tr>
    <tr>
        <td>502131231313123123</td>
        <td>审<span>1</span></td>
        <td>天猫</td>
        <td>江苏 南京</td>
        <td>活跃</td>
    </tr>
    <tr>
        <td>502131231313123122</td>
        <td></td>
        <td>JIT</td>
        <td>上海仓</td>
        <td>--</td>
    </tr>
    <tr>
        <td>34456786868686</td>
        <td>超卖<span>1</span></td>
        <td>苏宁</td>
        <td>********</td>
        <td>活跃</td>
    </tr>
    <tr>
        <td>198903213</td>
        <td></td>
        <td>JITX</td>
        <td>********</td>
        <td>关闭</td>
    </tr>
</table>

<table>
    <tr>
        <td>
            <input placeholder="order no"/>
            <button>Seach</button>
        </td>
        <td rowspan="6" style="vertical-align: top;">
            <table style="background-color: honeydew;">
                <tr><td>2020-10-11 00:00:00</td><td>系统</td><td>天猫自动导入</td></tr>
                <tr><td>2020-10-11 00:00:00</td><td>财务</td><td>审核</td></tr>
                <tr><td>2020-10-11 00:00:00</td><td>系统</td><td>派发至物流园</td></tr>
                <tr><td>2020-10-11 00:00:00</td><td>物流园</td><td>发货回传<span style="text-decoration:underline;">SF1220234242</span></td></tr>
                <tr><td>2020-10-11 00:00:00</td><td>物流园</td><td>退回回传<span style="text-decoration:underline;">YT1220234242</span></td></tr>
            </table>
        </td>
    </tr>
    <tr><td style="border: 1px solid gray;"><table><tr><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td></tr></table></td></tr>
    <tr>
        <td>
            <table style="background-color: darkgray;">
                <tr><td>1231334335453</td><td>2020-10-10 00:00:00</td></tr>
                <tr><td>tmall</td><td>导入订单</td></tr>
                <tr><td><span style="color: aquamarine;">OK</span></td><td>1+1</td></tr>
                <tr><td>1,200.00</td><td></td></tr>
                <tr>
                    <td colspan="2">
                        <table style="background-color: aliceblue;">
                            <tr>
                                <td>B0123131231</td>
                                <td>8056</td>
                                <td>165/80</td>
                                <td>1</td>
                                <td>1,200.00</td>
                                <td>100%</td>
                                <td><span style="border: 1px solid black;color: white;background-color: blueviolet;">换货</span></td>
                            </tr>
                            <tr>
                                <td>iphone<span style="color: azure;background-color: blue;border-radius: 20%;font-size: small;">赠</span></td>
                                <td></td>
                                <td></td>
                                <td>1</td>
                                <td>0.00</td>
                                <td>0%</td>
                                <td></td>
                            </tr>
                        </table>
                    </td>
                </tr>
            </table>
        </td>
    </tr>
    <tr>
        <td style="background-color: azure;">
            <table >
                <tr>
                    <td><span style="text-decoration:underline;">DN010100001</span></td>
                    <td>1</td>
                    <td>物流园</td>
                    <td>OK</td>
                </tr>
            </table>
        </td>
    </tr>
    <tr>
        <td style="background-color: rgb(178, 233, 250);">
            <table >
                <tr>
                    <td><span style="text-decoration:underline;">SF1220234242</span></td>
                    <td><span style="border: 1px solid black;color: white;background-color:burlywood;">丢件</span></td>
                    <td><span style="border: 1px solid black;color: white;background-color:burlywood;">换货</span></td>
                </tr>
            </table>
        </td>
    </tr>
    <tr>
        <td style="background-color: rgb(226, 212, 250);">
            <table >
                <tr>
                    <td><span style="text-decoration:underline;">YT1220234242</span></td>
                    <td>B0123131231</td>
                    <td>8056</td>
                    <td>165/80</td>
                    <td>4564643532243242424242</td>
                    <td><span style="border: 1px solid black;color: white;background-color:burlywood;">丢件</span></td>
                    <td><span style="border: 1px solid black;color: white;background-color:burlywood;">撤销</span></td>
                </tr>
            </table>
        </td>
    </tr>
</table>

