# JavaScript中处理空值的便捷操作

## 1. 逻辑运算符简写

**|| 运算符（默认值设置）**:
```javascript
const value = someVariable || '默认值';
```
如果`someVariable`是假值（如`undefined`、`null`、`''`、`0`、`NaN`或`false`），则使用右侧的默认值

**?? 运算符（空值合并）**:
```javascript
const value = someVariable ?? '默认值';
```
仅当`someVariable`为`null`或`undefined`时才使用默认值，其他假值如空字符串或0会被保留。

## 2. 条件检查简写

**真值检查**:
```javascript
if (variable) {
  // 仅当variable不是假值时执行
}
```

**对象存在检查**:
```javascript
if (object) {
  // 仅当object不是null或undefined时执行
}
```

## 3. 可选链操作符

**?.（访问可能不存在的属性）**:
```javascript
const value = user?.address?.street;
```
如果`user`或`address`是`null`或`undefined`，表达式会返回`undefined`而不是报错。

## 4. 解构赋值中的默认值

```javascript
const { name = '匿名', age = 0 } = user || {};
```
如果`user`不存在，会使用空对象解构，然后为各属性提供默认值。

## 5. 三元运算符

```javascript
const display = username ? username : '游客';
// 或简写为
const display = username || '游客';
```

## 6. 布尔转换

```javascript
const hasValue = !!variable;  // 转换为true或false
```

## 7. Array相关

```javascript
const safeArray = array || [];  // 确保是数组
const firstItem = array?.[0];   // 安全访问第一项
const items = array?.length ? array : defaultArray;  // 检查是否有内容
```
