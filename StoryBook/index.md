# StoryBook 安装
> 封装是为了复用，将封装出来的组件或者项目中提取出来的组件可复用的，建议写一个文档和演示调用demo,这就建议用类似StoryBook这个工具，可以更好的管理组件文档和演示demo,更容易的方便复用，从而可以提升开发效率

## 所需资源
- vscode 
- nodeJs
- reactJs

## 先按装react
```shell
yarn global reate-react-app
create-react-app storybook
```

## 按装 StoryBook
```shell
# 按装完成，可以在package.json里看到依赖项
npx sb init
```

### package.json文件

```json
{
  "name": "storybook",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@testing-library/jest-dom": "^5.16.4",
    "@testing-library/react": "^13.3.0",
    "@testing-library/user-event": "^13.5.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-scripts": "5.0.1",
    "web-vitals": "^2.1.4"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject",
    "storybook": "start-storybook -p 6006 -s public",  //自动填加的本地运行方式 npm run storybook
    "build-storybook": "build-storybook -s public" // 自动填加的打包 npm run build-storybook
  },
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ],
    "overrides": [
      {
        "files": [
          "**/*.stories.*"
        ],
        "rules": {
          "import/no-anonymous-default-export": "off"
        }
      }
    ]
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
  "devDependencies": {
    "@storybook/addon-actions": "^6.5.9",    //storybook 所需要的依赖包 begin
    "@storybook/addon-essentials": "^6.5.9",
    "@storybook/addon-interactions": "^6.5.9",
    "@storybook/addon-links": "^6.5.9",
    "@storybook/builder-webpack5": "^6.5.9",
    "@storybook/manager-webpack5": "^6.5.9",
    "@storybook/node-logger": "^6.5.9",
    "@storybook/preset-create-react-app": "^4.1.2",
    "@storybook/react": "^6.5.9",
    "@storybook/testing-library": "0.0.13",  //storybook 所需要的依赖包 end
    "babel-plugin-named-exports-order": "0.0.2",
    "prop-types": "^15.8.1",
    "webpack": "^5.73.0"
  }
}


```


### 运行storybook

```shell
yarn storybook
```

### 访问
- http://localhost:6006/?path=/story/example-introduction--page

