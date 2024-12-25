## README

这是一个使用 github action 发布 npm package 到 github npm registry 的示例。
> 注意 pull github npm registry 需要自己创建`package:read`的 access token，同时添加在 .npmrc 中。

## package.json 配置

在 package.json 中，填写以下字段：  
```json
"publishConfig": {
    "registry": "https://npm.pkg.github.com"
}
```

## 确认 package.json 配置

3. 确认 package.json 中的名字，包含 scope 部分，为第二步的 `NAMESPACE`。
4. 确认 package.json 中的 repository 字段，是对应的 github 仓库地址。

```json
{
    "name": "@<NAMESPACE>/<your-package-name>",
    "repository": {
        "type": "git",
        "url": "<repo>"
    }
}
```

## monorepo

根据[文档](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-npm-registry#authenticating-to-github-packages) 只需要每个 package.json 的 repository 字段都指向 github 仓库地址即可。

## 在项目中拉取 github npm registry 的包

安装包也只需要给根目录或者全局的 .npmrc 文件配置以下内容即可：

```
@NAMESPACE:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

## 注意事项 

仓库默认是 private 的，所以只有有权限的人才能拉取包。但是很神奇的是默认不允许组织内的人可以拉取，那个权限是 internal。
同时，需要先在 org 中的 setting - packages 设置可以调整的权限，默认只有 private，需要手动开放 internal 和 public，然后 org - packages 中才能调整各个 package 的权限。
link 后，package 的读写权限，会自动继承自 link 的 repo。

>注意，不管 package 是否为 public，都需要配置 .npmrc 的 github registry，否则无法拉取。