# Vitest 测试与模拟最佳实践

## 模拟(Mock)技巧

### 模拟顺序很重要
* 变量定义应该在`vi.mock()`调用之前，避免"Cannot access X before initialization"错误
* 对于复杂情况，可以使用变量声明在前，然后在`setup`或`beforeEach`中设置具体值

### 模拟外部依赖
* 直接导入模块并使用`vi.spyOn`来模拟其方法：

```javascript
import * as useIsLogin from '../../../base/composables/utils/useIsLogin';
vi.spyOn(useIsLogin, 'default').mockImplementation(async () => isLogin);
```

* 对于完全模拟的模块，使用`vi.mock`：

```javascript
vi.mock('../../../../../B2C/composables/inquiry/useCreateContacts', () => ({...}));
```

### 状态追踪变量
* 使用对象引用可以在测试中动态修改值：

```javascript
const mockIsSucceeded = { value: true }; // 不是 const mockIsSucceeded = true
```

* 这样在测试中可以通过`mockIsSucceeded.value = false`修改，而不必重新模拟整个函数

### 分离模拟声明和行为
* 在顶层声明模拟变量和基础行为
* 在具体测试中根据需要覆盖特定行为

### 模拟隔离与作用域
* **在每个测试组内重新设置模拟**，而非共享全局模拟，提高测试隔离性：

```javascript
describe('Component - Feature 1', () => {
  let mockFunction;
  
  beforeEach(() => {
    mockFunction = vi.fn().mockReturnValue('test');
    vi.mock('../../path/to/module', () => ({
      default: () => mockFunction(),
    }));
  });
  
  // 测试...
});

describe('Component - Feature 2', () => {
  let mockFunction;
  
  beforeEach(() => {
    mockFunction = vi.fn().mockReturnValue('different value');
    vi.mock('../../path/to/module', () => ({
      default: () => mockFunction(),
    }));
  });
  
  // 测试...
});
```

* 这种方法确保测试间不会相互干扰，即使测试相同的组件功能

### 简化模拟函数
* 优先使用简单的`vi.fn()`而非复杂的`mockImplementation`，提高代码可读性和稳定性：

```javascript
// 简单且足够用的方式
const mockLoad = vi.fn();

// 而非过于复杂的方式
const mockLoad = vi.fn().mockImplementation(() => {
  // 复杂逻辑
});
```

* 简单模拟更易于理解和维护，降低测试脆弱性

## 测试组织结构

### 使用setup函数
* 将通用初始化逻辑封装到`setup`函数中
* 但特殊场景（如未登录测试）可能需要单独配置

### 测试分组
* 使用`describe`按功能或场景分组测试
* 嵌套`describe`用于进一步细分场景
* **按功能逻辑分组而非按实现细节分组**，使测试更清晰：

```javascript
// 好的做法 - 按用户场景分组
describe('ShoppingCart', () => {
  describe('空购物车状态', () => {
    // 测试空状态下的UI和交互
  });
  
  describe('有商品状态', () => {
    // 测试非空状态下的UI和交互
  });
});

// 避免 - 按实现细节分组
describe('ShoppingCart', () => {
  describe('计算方法', () => {});
  describe('UI元素', () => {});
});
```

### 重置模拟状态
* 使用`beforeEach`在每个测试前重置模拟状态：

```javascript
beforeEach(() => {
  vi.resetAllMocks(); // 重置所有模拟
  // 或
  vi.clearAllMocks(); // 仅清除调用信息
});
```

* 考虑测试的隔离性，根据需要使用`afterEach`进行清理

### 等待渲染完成
* 使用`waitFor`确保组件已完全渲染：

```javascript
await waitFor(() => {
  expect(screen.getByText('お問合せ・質問')).toBeInTheDocument();
});
```

* 在`waitFor`中包含断言，确保异步操作完成后才验证

### 异步组件处理
* 使用`Suspense`包装异步组件：

```javascript
template: `
  <div>
    <Suspense>
      <InqMobile />
    </Suspense>
  </div>
`,
```

* 这对于使用`async setup()`或异步组件的Vue组件尤为重要

## 测试各种情况的技巧

### 测试初始渲染
* 检查页面标题、输入表单等静态元素是否存在
* 使用`screen.getByText`或`screen.getByPlaceholderText`等查询方法

### 测试条件分支（如登录/未登录）
* 为不同条件创建不同测试分组
* 根据需要调整模拟行为

### 测试异步流程
* 模拟异步函数行为
* 使用`mockImplementation`定义复杂行为
* 确保使用`await`等待异步操作完成

### 测试错误处理
* 使用`mockRejectedValueOnce`模拟失败情况
* 模拟`console.error`捕获错误输出
* 检查错误是否被正确处理

### 测试导航行为
* 使用`navigateToSpy`监控导航调用
* 验证导航参数，如路径和选项（`{ external: true }`）

### 关注行为而非实现细节
* **测试组件的外部行为而非内部实现**，提高测试的稳定性：

```javascript
// 好的做法 - 测试用户可见的结果
test('显示用户名', async () => {
  // ...渲染组件
  expect(screen.getByText('欢迎，测试用户')).toBeInTheDocument();
});

// 避免 - 过度依赖实现细节
test('调用getUsername方法', async () => {
  const spy = vi.spyOn(component.vm, 'getUsername');
  // ...渲染组件
  expect(spy).toHaveBeenCalled();
});
```

* 这使得测试不易受重构影响，更好地保障功能正确性

## 避免常见错误

* **路径错误**：确保导入路径正确，尤其是在不同层级的测试文件中
* **提升(hoisting)问题**：了解`vi.mock`被提升到文件顶部的特性，避免引用未初始化变量
* **异步渲染问题**：使用`Suspense`处理异步组件，避免渲染错误
* **模拟顺序问题**：确保清除/重置模拟，避免测试间互相影响
* **类型问题**：适当使用TypeScript类型注解，如`let navigateToSpy: any;`
* **测试互相影响**：为每个测试或测试组独立设置模拟，避免共享状态导致的失败：

```javascript
// 问题示例 - 共享模拟状态
const mockLoad = vi.fn();
// 所有测试共享这个mockLoad

// 解决方案 - 独立模拟
describe('Test group', () => {
  let mockLoad;
  beforeEach(() => {
    mockLoad = vi.fn();
  });
});
```

## mock方法详解

### mockImplementation
`mockImplementation` 用于完全替换函数的实现。当你需要定义复杂的模拟行为或模拟函数的内部逻辑时非常有用。

```javascript
const mockFunction = vi.fn().mockImplementation((arg1, arg2) => {
  if (arg1 > arg2) {
    return 'Greater';
  } else {
    return 'Less or Equal';
  }
});

// 或者用于异步函数
mockFunction.mockImplementation(async () => {
  await someAsyncOperation();
  return 'Result';
});
```

### mockResolvedValue
`mockResolvedValue` 专门用于模拟返回 Promise 的函数，是一种简写形式。它会创建一个返回已解析 Promise 的模拟函数。

```javascript
// 等价于 mockImplementation(() => Promise.resolve('Success'))
const mockFunction = vi.fn().mockResolvedValue('Success');

await mockFunction(); // 返回 'Success'
```

### 其他常用模拟方法

#### mockReturnValue
为同步函数设置返回值：

```javascript
const mockFunction = vi.fn().mockReturnValue('Default value');
```

#### mockRejectedValue
模拟 Promise 拒绝：

```javascript
const mockFunction = vi.fn().mockRejectedValue(new Error('Async error'));
```

#### mockReturnValueOnce / mockResolvedValueOnce / mockRejectedValueOnce
设置函数在特定调用次数时的返回值：

```javascript
const mockFunction = vi.fn()
  .mockReturnValueOnce('First call')
  .mockReturnValueOnce('Second call')
  .mockReturnValue('Default');

mockFunction(); // 'First call'
mockFunction(); // 'Second call'
mockFunction(); // 'Default'
```


```javascript
const mockAsyncFunction = vi.fn()
  .mockResolvedValueOnce('First result')
  .mockRejectedValueOnce(new Error('Second call fails'))
  .mockResolvedValue('Default result');
```

#### mockClear / mockReset / mockRestore
重置模拟函数的状态：
* `mockClear()`: 清除调用历史记录（如调用次数和参数）
* `mockReset()`: 清除历史记录并删除任何模拟实现
* `mockRestore()`: 完全还原原始实现（仅适用于 `spyOn` 创建的模拟）

#### spyOn
监视对象上的方法调用，可以选择替换其实现：

```javascript
vi.spyOn(console, 'log').mockImplementation(() => {});

// 或用于类方法
vi.spyOn(SomeClass.prototype, 'method').mockImplementation(() => 'Mocked');
```

### 常见模拟模式

#### 根据参数返回不同值

```javascript
mockFunction.mockImplementation((arg) => {
  if (arg === 'special') return 'Special case';
  return 'Normal case';
});
```

#### 模拟链式调用

```javascript
const mockChain = {
  method1: vi.fn().mockReturnThis(),
  method2: vi.fn().mockReturnThis(),
  value: vi.fn().mockReturnValue('result')
};

// 允许: mockChain.method1().method2().value()
```

#### 模拟异步流程

```javascript
// 模拟异步操作序列
const mockAsyncOperation = vi.fn()
  .mockImplementationOnce(async () => {
    await delay(100);
    return { status: 'pending' };
  })
  .mockImplementationOnce(async () => {
    await delay(100);
    return { status: 'processing' };
  })
  .mockImplementationOnce(async () => {
    await delay(100);
    return { status: 'completed' };
  });
```

## 高级测试模式

### 简化测试方法
* **避免过度验证**：专注于关键功能点，避免测试内部实现细节：

```javascript
// 简化前 - 过度关注细节
test('计算总价', () => {
  // 测试前置条件
  expect(component.vm.subtotal).toBe(100);
  expect(component.vm.tax).toBe(8);
  
  // 测试计算方法调用
  const spy = vi.spyOn(component.vm, 'calculateTotal');
  component.vm.updateCart();
  expect(spy).toHaveBeenCalled();
  
  // 测试结果
  expect(component.vm.total).toBe(108);
});

// 简化后 - 只关注关键结果
test('计算总价', () => {
  // 设置输入
  await component.setProps({ items: [{ price: 100, quantity: 1 }] });
  
  // 验证输出
  expect(screen.getByText('总计: ¥108')).toBeInTheDocument();
});
```

* 这种方法提高测试可读性，减少维护成本

### 组件与用户交互测试
* 确保使用`userEvent`而非`fireEvent`模拟更真实的用户交互：

```javascript
// 使用userEvent
const user = userEvent.setup();
await user.click(button);
await user.type(input, 'test');

// 而非直接使用fireEvent
fireEvent.click(button);
```

* userEvent包含更多真实交互细节，如焦点变化、输入延迟等

### 测试覆盖率与代码质量平衡
* 追求合理的覆盖率而非100%覆盖：
  * 确保核心业务逻辑有高覆盖率
  * 边缘情况可适当降低覆盖要求
  * 避免为提高覆盖率而编写无意义的测试

* 关注测试质量而非数量：
  * 一个全面的集成测试可能比多个脆弱的单元测试更有价值
  * 测试应在发现bug时提供有用的反馈，而非仅为覆盖率而存在
