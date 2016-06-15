# [iOS]UITableView UICollectionView 名詞解析

兩者都有
- cell: 存放一個個data的view
- cell reusable identifier: 利用識別碼可以實現不同cell有不同的配置
- supplementary views: 補充、支援性的view，例如header、footer (optional)

iOS6.0 之前

- `dequeueReusableCellWithIdentifier(identifier: String) -> UITableViewCell?`

> 不需先註冊reuse 識別碼（identifier）

iOS6.0 之後可用新增

- `dequeueReusableCellWithIdentifier(identifier: String, forIndexPath indexPath: NSIndexPath) -> UITableViewCell`

> 須先註冊`registerNib`/`registerClass`

#### UITableView

#### UICollectionView

- decoration view: 裝飾用的view (optional)
- `UICollectionViewLayout`: 組織cell和supplementary view的排列與位置
