1.  创建 style.less
2.  npm init
3.  npm install --save-dev less
4.  运行命令
    方法一：
    node_modules/.bin/lessc style.less>style.css
    方法二： 修改 package.json 的 scripts 字段

    ```
    scripts:{
        'test':'lessc style.less>style.css'
    }
    ```

    执行命令：npm run test
