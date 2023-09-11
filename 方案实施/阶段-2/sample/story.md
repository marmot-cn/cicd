## 用户故事

### 1.方案标题：

用户故事编写及其验收标准。

### 2.SOP：

* 目的：为产品提供清晰、明确的功能性和非功能性需求描述，并确保每个需求都有明确的验收标准，符合BDD测试要求。
* 范围：适用于所有新的功能开发和现有功能的改进。
* 流程：
	* 前置条件：产品经理或相关干系人已明确功能和非功能需求。
	* 操作步骤：
		1. 使用模板编写用户故事。例如：“作为 [角色]，我希望 [功能]，以便 [价值或结果]。”
		2. 明确功能性需求，描述用户希望系统实现的具体功能。
		3. 明确非功能性需求，如系统性能、安全性等。
		4. 为每个需求编写对应的验收标准，确保每一项标准都符合BDD测试要求。
* 后续操作：定期审查用户故事，确保其与产品方向和战略保持一致。

### 3.参考资料：

* BDD测试文档和最佳实践
*《用户故事与敏捷开发》

### 4.完成标准：

* 每个用户故事都明确描述了功能性和非功能性需求。
* 每个用户故事都有明确的、符合BDD测试要求的验收标准。

### 5.实施风险：

#### 5.1 需求不明确风险

* 风险描述：用户故事可能由于需求不明确而导致开发和测试团队混淆。
* 应对策略：定期与产品经理和关键干系人进行沟通，确保需求明确。

### 6.参与方：

* `Dev`
* `Test`
* `SM`
* `PO`

### 7.考核结果：

* 考核标准：检查用户故事的完整性和验收标准的准确性。
* 考核方法：团队定期审查用户故事，确保其与产品方向和战略保持一致。
* 反馈与改进：基于审查结果，对用户故事和验收标准进行调整或完善。

### 8.样例

#### 8.1 功能性需求用户故事

**用户故事**：作为在线购物网站的用户，我希望能在商品详情页面直接查看库存，以便我知道是否可以立即购买。

**验收标准**：

- Given 商品详情页面已加载
- When 我查看某一商品
- Then 我应该看到库存数量。

#### 8.2 非功能性需求用户故事

**用户故事**：作为在线购物网站的用户，我希望商品库存信息加载速度快，以便获得更好的购物体验。

**验收标准**：

- Given 商品详情页面已加载
- When 系统加载库存信息
- Then 加载时间不超过1秒。

#### 8.3 Go语言的BDD测试代码

```go
package main

import (
	. "github.com/smartystreets/goconvey/convey"
	"testing"
)

func LoadProduct(id int) *Product {
	// Mock a product load function.
	return &Product{ID: id, Stock: 10}
}

func LoadStockInfo(id int) float64 {
	// Mock the time taken to load stock info. Here we use a fixed value.
	return 0.5
}

type Product struct {
	ID    int
	Stock int
}

func TestProductDetails(t *testing.T) {
	Convey("Given a product details page has loaded", t, func() {
		product := LoadProduct(1)

		Convey("When I view a particular product", func() {
			Convey("Then I should see the stock quantity", func() {
				So(product.Stock, ShouldBeGreaterThanOrEqualTo, 0)
			})

			Convey("And the stock info should load quickly", func() {
				resultTime := LoadStockInfo(product.ID)
				So(resultTime, ShouldBeLessThanOrEqualTo, 1.0)
			})
		})
	})
}
```

### 9.责任人：

指定方案实施、监督和考核的主要负责人。

### 10.修订记录：

* 20230910: 丁克斌初始化