---
title: TypeScript
published: 2025-04-03
description: ''
image: ''
tags: [TypeScript]
category: '前端'
draft: false 
lang: 'zh-CN'
---
# useState 自动推导

通常 React 会根据 useState 的默认值来自动推导类型，不需要显式标注类型。

它根据初识值自动进行推断，比较适合有明确的初始值。

# useState 传递泛型参数

useState 本身是一个泛型函数，可以传入具体的自定义类型。

```typescript
type User = {
    name: String
    age: number
}

const [user, setUser] = useState<User>()
```

1. 显示 useState 函数参数的初始值必须满足类型为：User | () => User；

2. 限制 setUser 函数的参数必须满足类型为：User | () => User | undefined；

3. User 状态数据具备 User 类型相关的类型提示。

# useState 初始值为 null

当我们不知道状态的初始值是什么，将 useState 的初始值为 null 是一个常见的做法，可以通过具体类型联合 null 来做显式注解。

```typescript
type User = {
    name: String
    age: number
}

const [user, setUser] = useState<User | null>(null)
```

1. 限制 useState 函数传参的初始值可以是 User | null；

2. 限制 setUser 函数的参数类型可以是 User | null；

3. 为了类型安全，在调用的时候需要写成 user?.name 这种格式。（类型守卫）

# Props 与 TypeScript

## 基础使用

为组件 props 添加类型，本质是给函数的参数做类型注解，可以使用 type 对象类型或者 interface 接口来做注解。

```typescript
interface Props {
  className: string
}

const Button = (props: Props) => {
    const {className} = props
    return <button className={className}>Click Me</button>
}
```

## 为 children 添加类型

Children 是一个比较特殊的 prop，支持多种不同类型数据的传入，需要通过一个内置的 ReactNode 类型来做注解。

```typescript
interface Props {
    className: string
    children: React.ReactNode
}

const Button = (props: Props) => {
    const {className, children} = props
    return (
        <button className={className}>{children}</button>
    )
}
```

注解后，children 可以是多种类型，包括：React.ReactElement、string、number......

## 为事件 prop 添加类型

组件经常执行类型为函数的 prop 实现子传父、这类 prop 重点在于函数参数类型的注解。

```typescript
interface sonProps {
  onGetMsg?: (msg: string) => void
}

const Son = (props: sonProps) => {
  const { onGetMsg } = props
  const handleClick = () => {
    onGetMsg?.('this is msg')
  }
  return <button onClick={handleClick}>sendMsg</button>
}

const Father = () => {
    <Son onGetMsg={(msg) => console.log(msg)}></Son > // this is msg
}
```

1. 在组件内部调用时需要遵守类型的约束，参数传递需要满足需求；

2. 绑定 prop 时如果绑定内联函数直接可以推断出参数类型，否则需要单独注解匹配的参数类型。

# useRef 与 TypeScript

## 获取 dom

获取 dom 的场景，可以直接把要获取的 dom 元素的类型当成泛型参数传递给 useRef，可以推导出 .current 属性的类型。

```typescript
const App = () => {
    const domRef = useRef<HTMLInputElement>(null)
    useEffect(() => {
    domRef.current?.focus()
    }, [])
    
    return (
    <>
        <input type="text" ref={domRef} />
    </>
  )
}
```

## 引用稳定的存储器

当 useRef 当成引用稳定的存储器使用的场景可以通过泛型传入联合类型来做，比如定时器的场景：

```typescript
const App = () => {
    const timeRef = useRef<number | undefined>(undefined)
    
    useEffect(() => {
    timeRef.current = setInterval(() => {
        console.log('1')
    }, 1000)
    
    return () => clearInterval(timeRef.current)
    }, [])
    
    return <></>
}
```