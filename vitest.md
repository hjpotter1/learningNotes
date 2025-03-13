# Vitest 测试与模拟最佳实践

## 模拟(Mock)技巧

### 模拟顺序很重要
- 变量定义应该在`vi.mock()`调用之前，避免"Cannot access X before initialization"错误
- 对于复杂情况，可以使用变量声明在前，然后在`setup`或`beforeEach`中设置具体值

### 模拟外部依赖
- 直接导入模块并使用`vi.spyOn`来模拟其方法：
  ```javascript
  import * as useIsLogin from '../../../base/composables/utils/useIsLogin';
  vi.spyOn(useIsLogin, 'default').mockImplementation(async () => isLogin);
  ```
- 对于完全模拟的模块，使用`vi.mock`：
  ```javascript
  vi.mock('../../../../../B2C/composables/inquiry/useCreateContacts', () => ({...}));
  ```

### 状态追踪变量
- 使用对象引用可以在测试中动态修改值：
  ```javascript
  const mockIsSucceeded = { value: true }; // 不是 const mockIsSucceeded = true
  ```
- 这样在测试中可以通过`mockIsSucceeded.value = false`修改，而不必重新模拟整个函数

### 分离模拟声明和行为
- 在顶层声明模拟变量和基础行为
- 在具体测试中根据需要覆盖特定行为

## 测试组织结构

### 使用setup函数
- 将通用初始化逻辑封装到`setup`函数中
- 但特殊场景（如未登录测试）可能需要单独配置

### 测试分组
- 使用`describe`按功能或场景分组测试
- 嵌套`describe`用于进一步细分场景

### 等待渲染完成
- 使用`waitFor`确保组件已完全渲染：
  ```javascript
  await waitFor(() => {
    expect(screen.getByText('お問合せ・質問')).toBeInTheDocument();
  });
  ```

### 异步组件处理
- 使用`Suspense`包装异步组件：
  ```javascript
  template: `
    <div>
      <Suspense>
        <InqMobile />
      </Suspense>
    </div>
  `,
  ```

## 测试各种情况的技巧

### 测试初始渲染
- 检查页面标题、输入表单等静态元素是否存在
- 使用`screen.getByText`或`screen.getByPlaceholderText`等查询方法

### 测试条件分支（如登录/未登录）
- 为不同条件创建不同测试分组
- 根据需要调整模拟行为

### 测试异步流程
- 模拟异步函数行为
- 使用`mockImplementation`定义复杂行为
- 确保使用`await`等待异步操作完成

### 测试错误处理
- 使用`mockRejectedValueOnce`模拟失败情况
- 模拟`console.error`捕获错误输出
- 检查错误是否被正确处理

### 测试导航行为
- 使用`navigateToSpy`监控导航调用
- 验证导航参数，如路径和选项（`{ external: true }`）

## 避免常见错误
- **路径错误**：确保导入路径正确，尤其是在不同层级的测试文件中
- **提升(hoisting)问题**：了解`vi.mock`被提升到文件顶部的特性，避免引用未初始化变量
- **异步渲染问题**：使用`Suspense`处理异步组件，避免渲染错误
- **模拟顺序问题**：确保清除/重置模拟，避免测试间互相影响
- **类型问题**：适当使用TypeScript类型注解，如`let navigateToSpy: any;`

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

- `mockClear()`: 清除调用历史记录（如调用次数和参数）
- `mockReset()`: 清除历史记录并删除任何模拟实现
- `mockRestore()`: 完全还原原始实现（仅适用于 `spyOn` 创建的模拟）

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
