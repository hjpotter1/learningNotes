# Ruby & Rails 语法要点总结

## 1. Data Class vs Struct

### Data Class (Ruby 3.2+)
```ruby
# 不可变对象，提供函数式编程特性
LatestAnswerSummary = Data.define(:correct_count, :incorrect_count)

# 创建实例
summary = LatestAnswerSummary.new(correct_count: 5, incorrect_count: 3)

# 修改需要使用 with 方法，返回新对象
new_summary = summary.with(correct_count: 10)
# 原对象不变
summary.correct_count        # => 5
new_summary.correct_count    # => 10
```

### Struct
```ruby
# 可变对象，传统面向对象风格
LatestAnswerSummary = Struct.new(:correct_count, :incorrect_count, keyword_init: true)

# 创建实例
summary = LatestAnswerSummary.new(correct_count: 5, incorrect_count: 3)

# 直接修改属性
summary.correct_count = 10
summary.correct_count        # => 10
```

### 选择建议
- **Data Class**: 适合函数式编程，需要不可变性的场景
- **Struct**: 适合传统面向对象，需要简单可变对象的场景
- **项目一致性**: 与既存代码保持一致的风格

## 2. Enum 定义

```ruby
class Lms::LatestAnsweringHistory < ApplicationRecord
  # Rails 7+ 语法，使用符号定义
  enum :status, { not_learned: 0, incorrect: 1, correct: 2 }
  
  # 旧版语法
  # enum status: { not_learned: 0, incorrect: 1, correct: 2 }
end
```

## 3. 类方法定义和可见性

```ruby
class ExampleClass
  # 公开类方法
  def self.public_method
    # 实现
  end
  
  # 私有类方法（推荐写法）
  private_class_method def self.private_method
    # 实现
  end
  
  # 另一种私有类方法写法
  def self.another_private_method
    # 实现
  end
  private_class_method :another_private_method
end
```

## 4. ActiveRecord 查询优化

### 避免N+1查询
```ruby
# ❌ N+1查询
users.each do |user|
  user.orders.count
end

# ✅ 预加载
users.includes(:orders).each do |user|
  user.orders.count
end
```

### 使用select优化
```ruby
# 只选择需要的字段
results = where(user: users, main_question_id: main_question_ids)
          .select(:user_id, :status, 'COUNT(*) as answers_count')
          .group(:user_id, :status)
```

## 5. Ruby 集合操作

### each vs each_with_object
```ruby
# 基本迭代
array.each do |item|
  # 处理item
end

# 带累加器的迭代
result = array.each_with_object({}) do |item, hash|
  hash[item.id] = item.value
end

# 等价于
result = array.each_with_object({}) do |item, accumulator|
  accumulator[item.id] = item.value
end
```

### 哈希初始化模式
```ruby
# 为每个用户初始化默认值
answer_summary_by_user_id = users.each_with_object({}) do |user, hash|
  hash[user.id] = LatestAnswerSummary.new(correct_count: 0, incorrect_count: 0)
end
```

## 6. RSpec 测试最佳实践

### 变量命名规范
```ruby
# ❌ 避免魔法数字
let(:user1) { create(:user) }
let(:user2) { create(:user) }

# ✅ 使用描述性命名
let!(:users) { create_list(:user, 2) }

# 使用
users[0]  # 第一个用户
users[1]  # 第二个用户
```

### 测试数据隔离
```ruby
context '特定测试场景' do
  before do
    # 清理数据，确保测试独立性
    described_class.delete_all
    
    # 创建测试数据
    create(:model, attributes)
  end
end
```

### Shared Examples
```ruby
# 定义共享测试
shared_examples_for '进捗内容' do
  it '正确计算进捗' do
    # 测试逻辑
  end
end

# 使用共享测试
context '单章情况' do
  let(:expected_results) { [...] }
  it_behaves_like '进捗内容'
end
```

## 7. Rails 命名约定

### 文件和类名对应
```ruby
# 文件: app/models/lms/latest_answering_history.rb
class Lms::LatestAnsweringHistory < ApplicationRecord
end

# 测试文件: spec/models/lms/latest_answering_history_spec.rb
RSpec.describe Lms::LatestAnsweringHistory, type: :model do
end
```

### 方法命名模式
```ruby
# 查询方法通常使用现在时
def self.learned_count_summaries_of_main_questions
end

# 动作方法使用动词
def self.upsert_from_answering_history
end

# 判断方法使用?结尾
def valid?
end

# 危险方法使用!结尾
def save!
end
```

## 8. 错误处理模式

### 数据库约束处理
```ruby
def self.upsert_from_answering_history(answering_history)
  latest = find_by(user_id: attrs[:user_id], sub_question_id: attrs[:sub_question_id])
  
  if latest.nil?
    begin
      create!(attrs)
    rescue ActiveRecord::RecordNotUnique
      # 处理并发创建冲突
      latest = find_by(user_id: attrs[:user_id], sub_question_id: attrs[:sub_question_id])
      latest.with_lock do
        latest.update!(attrs)
      end
    end
  else
    # 使用悲观锁避免并发更新问题
    latest.with_lock do
      latest.update!(attrs)
    end
  end
end
```

## 9. 性能优化技巧

### 数据库查询优化
```ruby
# ❌ 复杂的窗口函数查询
raw_sql = <<~SQL
  SELECT user_id, main_question_id, sub_question_id, status,
         ROW_NUMBER() OVER (PARTITION BY user_id, sub_question_id ORDER BY created_at DESC) AS latest_number
  FROM answering_histories
  WHERE user_id IN (#{user_ids}) AND main_question_id IN (#{main_question_ids})
SQL

# ✅ 简单的聚合查询 + 预计算表
results = where(user: users, main_question_id: main_question_ids)
          .select(:user_id, :status, 'COUNT(*) as answers_count')
          .group(:user_id, :status)
```

### 分支优化
```ruby
def self.learned_count_summaries_of_main_questions(user, partitioned_main_question_ids)
  # 单章优化分支
  if partitioned_main_question_ids.size == 1
    answer_summary = learned_count_summary_of_main_questions(user, partitioned_main_question_ids[0])
    return [answer_summary]
  end

  # 多章处理逻辑
  # ...
end
```

## 10. 代码组织模式

### 渐进式重构
```ruby
class ExampleClass
  # 既存方法保持不变
  private_class_method def self.calculate_progresses(user, progresses)
    # 旧逻辑
  end

  # TODO: 一时メソッド - 新架构迁移用
  # 目的: 性能改善
  # 删除条件: 全ての依存箇所迁移完成后
  private_class_method def self.calculate_progresses_tmp(user, progresses)
    # 新逻辑
  end
end
```

### 文档化重要决策
```ruby
# 章別の学習進捗を取得する
# @param user [User] 対象ユーザー
# @param partitioned_main_question_ids [Array<Array<Integer>>] 章別に分けられた大設問IDの配列
# @return [Array<LatestAnswerSummary>] 章別の解答統計
def self.learned_count_summaries_of_main_questions(user, partitioned_main_question_ids)
  # 实现
end
```

## 总结

1. **一致性优先**: 与项目既存代码保持风格一致
2. **性能考虑**: 优先使用简单查询，避免复杂SQL
3. **测试完整**: 特别注意边界情况和核心业务逻辑
4. **渐进重构**: 使用临时方法确保安全迁移
5. **文档化**: 重要的设计决策要有清晰的注释
