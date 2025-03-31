---
title: package.json
published: 2025-03-31
description: ''
image: ''
tags: [包管理]
category: '前端'
draft: false 
lang: 'zh-CN'
---
package.json 是一个用于描述和配置项目的重要文件，其中包含了许多字段和选项，可以影响项目的构建、依赖管理、脚本执行等方面。

# 必须属性

## Name

定义项目的名称，不能以"."和"\_"开头，不能包含大写字母。

## Version

定义项目的版本号，格式为：大版本号.次版本号.修订号。

### 版本号

格式为：`X.Y.Z`，并且 X、Y、Z 均为正整数并且不断递增。X 表示大版本（major）、Y 表示小版本（minor）、Z 表示补丁版本（patch）。

1. 当进行了向后兼容的 bug 修复时，补丁版本 Z 必须增加；

2. 当引入了向后兼容的新功能时，小版本 Y 必须增加，同时 Z 必须重置为 0（小版本里面可能会包含 bug 修复）；

3. 当引入了不兼容的变更时，大版本 X 必须增加，同时 Y、Z 必须重置为 0（大版本里面可能会包含小版本或者补丁版本的改动）；

4. `X.Y.Z` 后面还可以加预发布版本号、构建信息，格式为：`X.Y.Z-pre_lease+build_meta`，比如：`1.0.0-alpha+20151226`、`1.0.0-beta.2+20151230`。

# 描述信息

## Description

项目描述。

## Keywords

项目关键词。

## author

项目作者。

```javascript
"author": "name (https://sytusramlethal.github.io/)"
```

## Contributors

项目贡献者。

## Honepage

项目主页地址。

## Repository

项目代码仓库地址。

## Bugs

项目提交问题的地址。

```javascript
 //提交问题的地址和反馈的邮箱,url通常是Github中的issues页面
"bugs": { 
  "url" : "https://github.com/facebook/react/issues", 
  "email" : "xxxxx@xx.com"
}
```

## Funding

指定项目的资金支持方式和链接。

```javascript
  "funding": {
    "type": "patreon",
    "url": "https://www.patreon.com/my-module"
  }

```

# 依赖配置

## **dependencies**

生产环境的依赖包

如果不使用脱字符（^），安装的版本号固定；如果使用，则能安装当前大版本的最新版本，在package-lock.json中可查看当前实际安装的版本。

## **devDependencies**

开发环境的依赖包，例如webpack、vite、babel、ESLint等。

## **peerDependencies**

对等依赖的作用：

1. 减小打包体积：例如使用 react 开发的组件库，安装 react 是必不可少的，而使用组件库的开发者，本地项目肯定安装了react，因此开发的组件库中不必把react打包进去（期望项目的使用者来提供这些模块的实现）。

2. 版本一致性：使用你的组件库的开发者需要确保他们项目中安装了与你声明的对等依赖版本兼容的包，以确保组件库正常运行。

示例：声明要使用组件库，需在项目中安装大于17.0.1版本的 react

```javascript
  "peerDependencies": {
    "react": ">17.0.1"
  }
```

## **peerDependenciesMeta**

将对等依赖标记为可选，如果用户没有安装对等依赖，npm 不会发出警告。

```javascript
  "peerDependenciesMeta": {
    "react": {
      "optional": true //标记为可选
    }
  }
```

## **bundledDependencies**

声明捆绑依赖项。

## **optionalDependencies**

声明可选依赖项。

## **engines**

声明对npm或node的版本要求：

```javascript
  "engines": {
    "node": ">=8.10.3 <12.13.0",
    "npm": ">=6.9.0"
  }
```

# 脚本配置

## **scripts**

脚本入口。

## **config**

用于定义项目的配置项，例如设置环境变量。

```javascript
  "config": {
    "baseUrl": "https://example.com"
  }
```

# 发布配置

## **private**

防止私有包发布到npm服务器，要发布到npm上设为false。

# 第三方配置

## **eslintConfig**

eslint的配置。

## **babel**

babel的配置。