# Ptrade
Ptrade python自动化交易

* 策略代码：【占坑，定期更新】

* 帮助文档（详见pchm文件）：

![20220610001](https://pic.kaihu51.com/typora/20220610001.png)

* 接口文档

  ![20220610002](https://pic.kaihu51.com/typora/20220610002.png)

* 示例代码

  ```python
  def initialize(context):
      g.security = '600570.SS'
      set_universe(g.security)
      
  def handle_data(context, data):
      security = g.security
      sid = g.security
      
      # 取得过去五天的历史价格
      df = get_history(5, '1d', 'close', security, fq=None, include=False)
      
      # 取得过去五天的平均价格
      average_price = round(df['close'][-5:].mean(), 3)
  
      # 取得上一时间点价格
      current_price = data[sid]['close']
      
      # 取得当前的现金
      cash = context.portfolio.cash
      
      # 如果上一时间点价格高出五天平均价1%, 则全仓买入
      if current_price > 1.01*average_price:
          # 用所有 cash 买入股票
          order_value(g.security, cash)
          log.info('buy %s' % g.security)
      # 如果上一时间点价格低于五天平均价, 则空仓卖出
      elif current_price < average_price and get_position(security).amount > 0:
          # 卖出所有股票,使这只股票的最终持有量为0
          order_target(g.security, 0)
          log.info('sell %s' % g.security)
  ```
  
  
  
* 开通Ptrade

  只要开通指定A股券商账户，入金即可开通，费率股票万一免五，0.1元起步，支持股票，基金ETF，可转债，两融。 (可以提供测试账户，体验量化接口)

  开通后即可免费使用，并有官方技术交流群。
  
  ![](http://xximg.30daydo.com/picgo/ufc200.png)
